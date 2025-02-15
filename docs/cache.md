For incremental processing of tasks, `leakrfc` uses a global cache to track task results. If a computed cache key for a specific task (e.g. sync a file, extract an archive) is already found in cache, running the task again will be skipped. This is implemented very granular and applies to all kinds of operations, such as [crawl](./crawl.md), [make](./make.md) and the adapters (currently [aleph](./sync/aleph.md))

`leakrfc` is using [anystore](https://docs.investigraph.dev/lib/anystore/cache/) for the cache implementation, so any supported backend is possible. Recommended backends are redis or sql, but a distributed cloud-backend (such as a shared s3 bucket) can make sense, too.

Per default, an in-memory cache is used, which doesn't persist.

## Configure

Via environment var:

```bash
LEAKRFC_CACHE__URI=redis://localhost

# additional config
LEAKRFC_CACHE__DEFAULT_TTL=3600  # seconds
LEAKRFC_CACHE__BACKEND_CONFIG__REDIS_PREFIX=my-prefix
```
