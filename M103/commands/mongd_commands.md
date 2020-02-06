# start mongod daemon
mongod

# killing mongod daemon through PID
ps -ef | grep mongod
kill <pid>

## added useful flags
--port arg      - specify port number - 27017 by default
--bind_ip arg   - comma separated list of ip addresses to listen on - localhost by default
--dbpath arg    - directory for datafiles - defaults to /data/db
--logpath arg   - log file to send write to instead of stdout - has to be a file, not directory
--fork          - fork server process (ie make mongod a daemon instead of shell process)
--auth          - run with security
--config arg    - location of config file with these options pre-set

see: https://docs.mongodb.com/manual/reference/program/mongod/
for config file options see: https://docs.mongodb.com/manual/reference/configuration-options/

# creating a user
mongo admin --host localhost:27000 --eval '
  db.createUser({
    user: "m103-admin",
    pwd: "m103-pass",
    roles: [
      {role: "root", db: "admin"}
    ]
  })
'