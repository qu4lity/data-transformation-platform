FROM nodered/node-red:latest-12-minimal
COPY --chown=node-red:node-red ./data/flows.json /data/flows.json
RUN npm install node-red-contrib-amqp-ack
