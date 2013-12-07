# NEWS

0.8.3 - 2014/12/05
------------------

- add: support redirection in async responses
- improve
  [hackney_url:make_url/3](https://github.com/benoitc/hackney/commit/a545d266106c0557374a8b9b13caa63ce89e86f2)
- fix: handle case where the response is already done in async responses

0.8.2 - 2014/12/05
------------------

- fix: trap exits in hackney_manager

0.8.1 - 2014/12/04
------------------

service release with a new feature and some minor improvements

- added the support for [socks5
  proxies](https://github.com/benoitc/hackney#socks5-proxy)
- improvment: integer and atom can now be passed in url params or forms
  values.
- breaking change: differentiate connect/recv timeout, now connect
  timeout return `{error, connect_timeout}`

0.8.0 - 2013/12/02
------------------

major release. With this release the API will not evolve much until the
1.0 release sometimes in january.

- breaking change: hackney now return a reference instead of an opaque record. The
  information is maintained in an ETS table. The same reference is now
used for async response requests.
- breaking change: `stream_body_request/2` and `stream_multipart_request/2` functions has
  been renamed to `send_body/2` and `send_multipart_body/2` .
- breaking change: remove `hackney:close_stream/1` function. You only need to
  use `hackney:close/1` now.
- breaking change: rename `hackney:raw/1` function to
  `hackney:cancel_request/1`.
- breaking change: the hakney pool handler based on dispcount is now
  available in its [own repository](https://github.com/benoitc/hackney_disp) so hackney doe  not depends on dispcount.
- fix: canceling and closing a request now make sure the async response
  process is killed.
- fix: make sure we pass a `Transfer-Encoding: chunked` header when we
  send a body without content-length.
- fix: make sure the client is correcly reconnected when we reuse a
  reference.

0.7.0 - 2013/11/22
------------------

- add new Loadbalance pool handler based on dispcount
- allows to set the pool handler
- breaking change: remove `hackney:start_pool/2` and
  `hackney:stop_pool/1`, use instead `hackney_pool:start_pool/2` and
  `hackney_pool:stop_pool/1`
- breaking change: A pool is now used by default
- breaking change: The `hackney_form` module has been removed. You can
  now encode/parse a form using the functions in the `hackney_url` module.
- deprecate `pool_size` and replace it by `max_connections`
- fix: apply applications defaults to the pool


0.6.1 - 2013/11/21
------------------

- doc: Fix the asynchronous response example in the readme
- add hackney_url:make_url/3, hackney_url:qs/1, hackney_url:parse_qs/1 functions

0.6.0 - 2013/11/21
------------------

- add the possibility to get an asynchronous response
- add support for the "Expect: 100-continue" header
- add hackney:controlling_process/2 to pass the control of an hackney context to another process

0.5.0 - 2013/11/06
------------------

- fix: proxied connections
- fix: correct the path passed to a request
- fix: multipart forms
- fix: Make sure that the controller process of the socket is the pool process when the socket is in the pool
- fix: auth header when when the user is not given

0.4.4 - 2013/08/25
------------------

- fix: doc typos
- fix: dialyzer errors
- fix: add mimetypes to the list of loaded applications
- fix: test.ebin example

0.4.3 - 2013/08/04
------------------

- removed parse_transform, the REST API is now available at the compilation.
fix: fix file upload content type
- doc: fix typos

0.4.2 - 2013/06/10
------------------

- handle `identity` transfert encoding. When the connection close return
  latest buffer.

0.4.1 - 2013/06/10
------------------

- Body can be passed as a
  [function](https://github.com/benoitc/hackney/commit/efd877f52733ccecf0ba1b5ed10783fe29d49b74)
- Add recv_timeout option
- Fix HEAD request (don't stream the body)
- Don't pass the Port to the Host header if it's default (http, https)
- Set the connection timeout
- Make sure sendfile correctly handle chunked encoding
- Add support for partial file uploads
- Return received buffer when no content lenght is given (http 1.0)
- Instead of returning `{error, closed}`, return `{error, {closed,
  Buffer}}` when you receive the body, so you can figure what happened
and maybe use the partial body.

0.4.0 - 2012/10/26
------------------

- Allows to stream a multipart request
- Add `insecure` option to connect via ssl without verifying an SSL
  certificate
- Handle empty headers values
- Add `force_redirect` option
- Add expm support
- Fix body streaming
- Fix SSL handling
- Fix hackney:request/3 (no more loop)


0.3.0 - 2012/09/26
------------------

- Add Multipart support
- Add HTTP Proxy tunneling support
- Fix Chuncked Response decoding

0.2.0 - 2012/07/18
------------------

- Allows the user to use a custom function to stream the body
- Add the possibility to send chunked requests
- Add an option to automatically follow a redirection
- Allows the user to force hackney to use the default pool

0.1.0 - 2012/07/16
------------------

- initial release
