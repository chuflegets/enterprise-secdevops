docker build --tag <name>:<release> --file Dockerfile context
docker run --rm -p <guest_port>:<host_port> <name>:<release>
