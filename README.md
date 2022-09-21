# Sish

Serve local endpoints through a proxy server. Similar to ngrok.

# Configure

Configure docker-compose.yml settings.
```
    environment:
      # Make local endpoint http://192.168.1.254:80/ available on http://marks-router-t1234gea4.test-proxy.dot.pm/
      - PROXY_NAME=marks-router-t1234gea4
      - PROXY_HOST=192.168.1.254
      - PROXY_PORT=80
      - PROXY_SERVER_HOST=test-proxy.dot.pm
      - PROXY_SERVER_PORT=2222
      - PROXY_SERVER_PASS=PASSWORD_HERE
```

Env:
- `PROXY_NAME` is the subdomain that the public available site will have.
- `PROXY_HOST` is the local hostname that you want to serve publicly, example your router IP.
- `PROXY_PORT` is the port that the local endpoint that you wanna serve is using, for example the port used for your router interface.
- `PROXY_SERVER_HOST` is the sish server, also the main domain. I have prepared a server on `test-proxy.dot.pm` that you may use.
- `PROXY_SERVER_PORT` is the sish server port that is used to connect to the server. On my server, this is `2222`.
- `PROXY_SERVER_PASS` is the sish server password. Message me for it.

# Use
```
docker-compose up
```

There you should see something like:
```
❯ docker-compose up
[+] Running 2/2
 ⠿ Container sish-example-dockerbased-website-1  Recreated                                                                                                                                                               0.1s
 ⠿ Container sish-example-router-1               Recreated                                                                                                                                                               0.1s
Attaching to sish-example-dockerbased-website-1, sish-example-router-1
sish-example-router-1               | Pseudo-terminal will not be allocated because stdin is not a terminal.
sish-example-dockerbased-website-1  | Pseudo-terminal will not be allocated because stdin is not a terminal.
sish-example-router-1               | Warning: Permanently added '[test-proxy.dot.pm]:2222,[146.190.236.72]:2222' (ED25519) to the list of known hosts.
sish-example-dockerbased-website-1  | Warning: Permanently added '[test-proxy.dot.pm]:2222,[146.190.236.72]:2222' (ED25519) to the list of known hosts.
sish-example-router-1               | Press Ctrl-C to close the session.
sish-example-router-1               |
sish-example-router-1               | Starting SSH Forwarding service for http:80. Forwarded connections can be accessed via the following methods:
sish-example-router-1               | HTTP: http://marks-router-t1234gea4.test-proxy.dot.pm
sish-example-router-1               | HTTPS: https://marks-router-t1234gea4.test-proxy.dot.pm
sish-example-router-1               |
sish-example-dockerbased-website-1  | Press Ctrl-C to close the session.
sish-example-dockerbased-website-1  |
sish-example-dockerbased-website-1  | Starting SSH Forwarding service for http:80. Forwarded connections can be accessed via the following methods:
sish-example-dockerbased-website-1  | HTTP: http://dockerbased-website-ge98ut3ge.test-proxy.dot.pm
sish-example-dockerbased-website-1  | HTTPS: https://dockerbased-website-ge98ut3ge.test-proxy.dot.pm
sish-example-dockerbased-website-1  |
```

The important parts are:
```
sish-example-router-1               | HTTP: http://marks-router-t1234gea4.test-proxy.dot.pm
sish-example-dockerbased-website-1  | HTTP: http://dockerbased-website-ge98ut3ge.test-proxy.dot.pm
```
Where you can see that it's serving your endpoints.
> PLEASE NOTE THAT MY SERVER DOES NOT SERVE HTTPS, so use HTTP endpoint to test it.

When accessing http://marks-router-t1234gea4.test-proxy.dot.pm (if you updated the IP to be your router IP) then it will serve your router UI.

When accessing http://dockerbased-website-ge98ut3ge.test-proxy.dot.pm, it will show `Bad Gateway` and in the terminal you should see the following:
```
sish-example-dockerbased-website-1  | connect_to localhost port 8002: failed.
sish-example-dockerbased-website-1  | ssh: rejected: connect failed (Connection refused)
```

# Goal
Make it possible to serve the Docker container from another project in our sish proxy.
