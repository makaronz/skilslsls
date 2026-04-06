# CDN Optimization

Maximize content delivery performance with CDN configuration, caching strategies, and edge computing.

---

## CDN Architecture

### How CDNs Work

```
User → Nearest Edge Server (PoP) → [Cache Hit?]
  Yes → Serve from edge (fast)
  No  → Fetch from origin → Cache at edge → Serve to user
```

### CDN Provider Comparison

| Feature | CloudFront | Cloudflare | Fastly | Akamai |
|---------|-----------|------------|--------|--------|
| Global PoPs | 450+ | 300+ | 70+ | 4,000+ |
| Edge compute | Lambda@Edge | Workers | Compute@Edge | EdgeWorkers |
| Free tier | Yes (limited) | Generous | No | No |
| DDoS protection | Shield | Built-in | Built-in | Kona |
| Custom SSL | Yes | Yes (free) | Yes | Yes |
| Purge speed | ~seconds | ~seconds | ~150ms | ~5 seconds |
| Best for | AWS ecosystem | All-in-one security | Real-time purge | Enterprise |

---

## Caching Configuration

### Cache Policy by Content Type

| Content Type | Cache Duration | Cache-Control Header | CDN TTL |
|-------------|---------------|---------------------|---------|
| Static assets (JS/CSS with hash) | 1 year | `public, max-age=31536000, immutable` | 1 year |
| Images | 30 days | `public, max-age=2592000` | 30 days |
| HTML pages | 0-5 min | `public, max-age=300, s-maxage=300` | 5 min |
| API responses | 0-60 sec | `public, s-maxage=60` | 60 sec |
| User-specific data | No cache | `private, no-store` | N/A |
| Fonts | 1 year | `public, max-age=31536000` | 1 year |

### Cache Key Configuration

Customize what makes a unique cache entry:

| Factor | Include? | Notes |
|--------|----------|-------|
| URL path | Always | Primary cache key |
| Query string | Selective | Whitelist relevant params only |
| Accept-Encoding | Yes | Serve correct compressed version |
| Accept-Language | If multi-language | Separate cache per language |
| Cookie | Rarely | Only for personalization CDNs |
| Device type | If adaptive serving | Mobile vs. desktop assets |

---

## Performance Optimization

### Asset Optimization

| Optimization | Impact | Implementation |
|-------------|--------|----------------|
| Brotli compression | 15-25% smaller than gzip | Enable at CDN edge |
| Image optimization | 40-60% size reduction | WebP/AVIF auto-conversion |
| Minification | 10-30% reduction | Build step for JS/CSS |
| HTTP/2 push | Reduced round trips | Configure priority hints |
| HTTP/3 (QUIC) | Better mobile performance | Enable at CDN level |
| Preconnect hints | Faster DNS/TLS | `<link rel="preconnect">` |

### Image CDN Strategies

Transform images on the fly at the edge:
```
https://cdn.example.com/images/hero.jpg?w=800&h=600&fmt=webp&q=80
```

**Parameters:**
- `w`, `h`: Width and height (auto-crop or fit)
- `fmt`: Format conversion (webp, avif)
- `q`: Quality (60-85 for photos, 80-90 for graphics)
- `dpr`: Device pixel ratio support

---

## Cache Invalidation

### Purge Strategies

| Method | Speed | Use Case |
|--------|-------|----------|
| Single URL purge | Instant | Fix specific page/asset |
| Wildcard purge | Seconds | Update section of site |
| Tag-based purge | Seconds | Related content group |
| Full purge | Seconds-minutes | Major deployment |
| TTL expiry | Wait for TTL | Normal content refresh |

### Deployment Strategy with CDN

1. **Versioned assets**: `/static/app.abc123.js` — never purge, immutable
2. **HTML pages**: Short TTL (5 min) + purge on deploy
3. **API responses**: `stale-while-revalidate` for seamless updates
4. **Emergency purge**: Instant purge capability for critical fixes

---

## Edge Computing

### Use Cases

| Use Case | Benefit | Example |
|----------|---------|---------|
| A/B testing | No origin round-trip | Route users to variants at edge |
| Authentication | Faster token validation | Validate JWT at edge |
| Geolocation | Instant geo-routing | Show local pricing/content |
| Bot detection | Early blocking | Block bad bots before reaching origin |
| URL rewriting | Flexible routing | Redirect, rewrite at edge |
| Header manipulation | Security + routing | Add security headers, modify requests |

---

## Monitoring and Analytics

### Key CDN Metrics

| Metric | Target | Alert Threshold |
|--------|--------|-----------------|
| Cache hit ratio | > 90% | < 80% |
| Origin requests | < 10% of total | > 20% |
| Edge latency (p50) | < 50ms | > 100ms |
| Error rate (5xx) | < 0.1% | > 1% |
| Bandwidth saved | > 80% | < 70% |
| SSL/TLS handshake | < 100ms | > 200ms |
