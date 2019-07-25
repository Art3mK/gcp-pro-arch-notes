# CDN

- option for HTTP(S) LBs
- cache contents from backends
    - instance groups
    - CS buckets
- cache miss/cache fill/cache key
    - cache key: identifier for cached content, must have exact match
        - by default in form of complete URL (https://example.com/url/example.jpg)
        - how to customize:
            - remove unneeded URL aspects: company domain, protocol, part of query string
