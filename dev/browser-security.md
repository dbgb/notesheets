# Firefox Browser Security

## Enable HTTPS Everywhere

## Disable WebRTC

## Enable DNS over HTTPS

### Cloudflare

#### Firefox

- (Options > General > Network Settings)
- Check "Enable DNS over HTTPS". This will automatically throw two switches in about:config.
  - `network.trr.mode = 2`
  - `network.trr.uri = https://mozilla.cloudflare-dns.com/dns-query`
- about:config
  - Set `network.trr.bootstrapAddress = 1.1.1.1`
  - Set `network.security.esni.enabled = true`

Check that all tests pass at <https://www.cloudflare.com/ssl/encrypted-sni/> and
<https://ipleak.net/>

#### Quad9

re: <https://web.archive.org/web/20190808004200/>

re: <https://www.ghacks.net/2018/04/02/configure-dns-over-https-in-firefox/>

In Settings, you can modify 3 items related to the Trusted Recursive Resolver
(aka `network.trr`):

`network.trr.mode` - controls when and how DoH should be used. By default it is
set to 0, meaning it is disabled.

- `0 — Off (default)`. To use operating system resolver.
- `1 — Race native against TRR`. Do both in parallel and go with the one that
  returns a result first. Most likely the native one will win.
- `2 — First`. Use TRR first, and only if the secure resolution fails use the
  operating system resolver.
- `3 — Only`. Only use TRR. Never use the native (after the initial setup).
- `4 — Shadow`. Runs the TRR resolves in parallel with the native for timing and
  measurements but uses only the native resolver results.
- `5 — Off by choice` This is the same as 0 but marks it as done by choice and
  not done by default.

We recommend trr.mode of ‘2’ so it will fall back to the default resolver if the
connection to the DoH server fails. If you only ever want to use DoH you can set
it to 3 – You will be unable to resolve DNS names if your DoH server goes down
and you won’t have a back-up using your system resolver.

`network.trr.uri` - is where you specify the resolver you want to use

`network.trr.bootstrapAddress` - you can forego setting this and it will use the
native system resolver for the initial query for
<https://dns.quad9.net/dns-query>

You can check out the logs by typing `about:networking#dns` into your browser
bar. Look for TRR ‘true’ entries to see what is being looked up via DNS over
HTTPS.

#### More DNS-over-HTTPS options

<https://github.com/curl/curl/wiki/DNS-over-HTTPS>
