# `sed`

## Convert all links in a file to HTTPS, in-place

```shell
sed -i -e 's|http:\/\/|https:\/\/|g' package-lock.json
```
