# System Design Example: URL Shortener

This is a walkthrough of how to design a URL shortening service like bit.ly, TinyURL, or goo.gl.

## 1. Requirements Clarification

### Functional Requirements
- Given a long URL, generate a shorter, unique URL
- When users access the short URL, redirect them to the original URL
- Users should optionally be able to pick a custom short URL
- Links will expire after a standard default timespan (configurable)
- Analytics to track click rates and user demographics

### Non-Functional Requirements
- Highly available - the system should be available at all times
- Minimal latency - redirection should happen in real-time with minimal delay
- The system should scale to handle millions of redirections
- The shortened links should not be guessable

### Constraints
- Traffic estimates: 
  - 100 million URLs generated per month
  - 10:1 read-to-write ratio (10 billion redirections per month)
- Storage estimates: 
  - Each entry is ~1KB (URL, timestamp, user info, etc.)
  - 100 million URLs per month × 1KB = 100 GB/month
  - For 5 years, we need approximately 6 TB of storage

## 2. High-Level Design

### API Endpoints

#### URL Shortening
```
POST /api/shorten
Request: {
  "long_url": "https://example.com/very/long/url/that/needs/shortening",
  "custom_alias": "optional_custom_string",
  "expiration_time": 86400 // optional, in seconds
}

Response: {
  "short_url": "https://tinyurl.com/abc123",
  "expiration_time": "2023-04-01T15:00:00Z"
}
```

#### URL Redirection
```
GET /{short_url_code}

Response: HTTP 302 redirect to the original URL
```

### Main Components

1. **Web Servers**: Handle incoming API requests
2. **Application Service**: Core logic for URL shortening and redirection
3. **Database**: Store mappings between short and long URLs
4. **Cache**: Store frequently accessed URLs to reduce database load
5. **Analytics Service**: Track URL usage statistics

## 3. Detailed Design

### URL Shortening Algorithm

Two main approaches:

1. **Hash-based approach**:
   - Apply MD5 or SHA-256 hash to the long URL
   - Take first 6-8 characters of the hash as the short URL code
   - Handle collisions by appending a counter or using a different portion of the hash

2. **Counter-based approach**:
   - Maintain a global counter
   - For each new URL, increment the counter
   - Convert the counter to base62 (a-z, A-Z, 0-9) to generate the short URL code

### Database Schema

**URL Table**:
```sql
CREATE TABLE urls (
    id BIGSERIAL PRIMARY KEY,
    short_code VARCHAR(10) UNIQUE,
    original_url TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    expires_at TIMESTAMP,
    user_id VARCHAR(128) -- if user authentication is required
);

CREATE INDEX idx_short_code ON urls(short_code);
```

**Analytics Table**:
```sql
CREATE TABLE clicks (
    id BIGSERIAL PRIMARY KEY,
    url_id BIGINT REFERENCES urls(id),
    clicked_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_agent TEXT,
    ip_address VARCHAR(45),
    referrer TEXT
);

CREATE INDEX idx_url_id ON clicks(url_id);
```

### Caching Strategy

- Use Redis or Memcached to cache frequently accessed URL mappings
- Cache eviction policy: LRU (Least Recently Used)
- Cache TTL: Align with URL expiration or use a standard value like 24 hours

## 4. Bottlenecks and Optimizations

### Potential Bottlenecks

1. **Database I/O**: High-volume redirection requests could overwhelm the database
2. **Hash Collisions**: Multiple long URLs could hash to the same short code
3. **Hotspots**: Extremely popular URLs could cause cache server overload

### Optimizations

1. **Database Partitioning**:
   - Shard the database based on the short code to distribute load
   - Use consistent hashing for partition management

2. **Caching Layer**:
   - Multi-level caching (application-level and CDN)
   - Cache warming for anticipated high-traffic URLs

3. **Analytics Processing**:
   - Use a separate write-optimized database for analytics
   - Implement asynchronous processing via message queues

4. **Expiration Handling**:
   - Background job to clean up expired URLs
   - Lazy deletion: mark as expired first, delete later

## 5. Additional Considerations

### Security
- Rate limiting to prevent abuse
- Check for malicious URLs
- HTTPS for all communications

### Monitoring and Scaling
- Monitor redirection latency and success rates
- Set up alerts for abnormal traffic patterns
- Auto-scaling for web tier based on traffic

### Internationalization
- Support for Unicode in URLs
- Consider regional compliance requirements (like GDPR)

## System Diagram

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Client    │────▶│  API Gateway│────▶│ Load Balancer│
└─────────────┘     └─────────────┘     └──────┬──────┘
                                                │
                                                ▼
┌─────────────┐     ┌─────────────┐     ┌──────┴──────┐
│  Analytics  │◀───▶│  URL Service│◀───▶│  Web Servers │
│   Service   │     │             │     └──────┬──────┘
└─────────────┘     └─────────────┘            │
                           │                   │
                           ▼                   ▼
                    ┌─────────────┐     ┌─────────────┐
                    │    Cache    │     │   Database   │
                    │             │     │             │
                    └─────────────┘     └─────────────┘
```