https://sadservers.com/scenario/salta

I lost connection to the host before getting the history,
but basically there are some problems:

Mistyped in dockerfile, change 8880 to 8888, serve.js to server.js.
Rebuild docker image.

Port 8888 is listening by nginx, so, stop nginx service then you're all good to go for the test.
