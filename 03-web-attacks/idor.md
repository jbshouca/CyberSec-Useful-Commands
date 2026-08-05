# IDOR (Insecure Direct Object Reference)

## Testing

```bash
# Change the ID in the URL
/api/users/123 → /api/users/124

# Change ID in POST body
{"user_id": 123} → {"user_id": 124}

# Change ID in cookie
Cookie: user_id=123 → user_id=124

# Enumerate valid IDs with ffuf
ffuf -u "http://TARGET/api/users/FUZZ" -w <(seq 1 1000) -b "session=YOUR_COOKIE" -fs DEFAULT_SIZE
```

## Bypass Techniques

```bash
# Encoded IDs — base64 or MD5
echo -n "124" | base64                        # decode and re-encode
echo -n "124" | md5sum                        # hash-based IDs

# Different HTTP methods
GET /api/users/124 → 403
PUT /api/users/124 → 200                      # method not checked

# Different API versions
/api/v2/users/124 → 403
/api/v1/users/124 → 200                       # old version lacks auth
```
