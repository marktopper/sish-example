FROM debian

RUN apt update
RUN apt install -y sshpass openssh-server curl

CMD sshpass -p ${PROXY_SERVER_PASS} ssh -p ${PROXY_SERVER_PORT} -R ${PROXY_NAME}:80:${PROXY_HOST}:${PROXY_PORT} -o StrictHostKeyChecking=accept-new ${PROXY_NAME}@${PROXY_SERVER_HOST}