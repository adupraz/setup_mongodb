FROM mongo:7


# we take over the default & start mongo in replica set mode in a background task
ENTRYPOINT mongod --port $MONGO_REPLICA_PORT --replSet rs0 --bind_ip localhost & MONGOD_PID=$!; \
# we prepare the replica set with a single node and prepare the root user config
INIT_REPL_CMD="rs.initiate({ _id: 'rs0', members: [{ _id: 0, host: '$MONGO_REPLICA_HOST:$MONGO_REPLICA_PORT' }] })"; \
#INIT_CREATE_CMD="use datas"; \
#INIT_USER_CMD="db.createUser({user: '$MONGO_INITDB_ROOT_USERNAME', pwd: '$MONGO_INITDB_ROOT_PASSWORD', roles:[ 'dbAdmin'] })"; \
# we wait for the replica set to be ready and then submit the command just above
until (mongosh admin --port $MONGO_REPLICA_PORT --eval "$INIT_REPL_CMD"); do sleep 5; done; \
#until (mongosh admin --port $MONGO_REPLICA_PORT --eval "$INIT_CREATE_CMD"); do sleep 5; done; \
#until (mongosh admin --port $MONGO_REPLICA_PORT --eval "$INIT_USER_CMD"); do sleep 5; done; \
# we are done but we keep the container by waiting on signals from the mongo task
echo "REPLICA SET ONLINE"; wait $MONGOD_PID;


##db.createUser({user: "mongoIB", pwd: "pass", roles:[ 'dbAdmin'] })
##db.createUser({ user: "mongoIB", pwd: "pass", roles: [ { role: "dbAdmin", db: "admin" } ]
##docker exec -it mongoIB mongosh --eval 'db.createUser({ user: "mongoIB", pwd: "pass", roles: [ { role: "dbAdmin", db: "admin" } ] })'
