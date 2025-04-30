# odf_rexec_code

Dockerfiles for a custom rexec broker/server for ODF

## Build

### Broker

Navigate to the `rexec_broker` folder and execute the command:

```bash
sudo docker build -t <docker_account_name>/rexec-broker:latest .
```

### Server

Navigate to the `rexec_server` folder and execute the command:

```bash
sudo docker build -t <docker_account_name>/rexec-server:latest .
```

## Launch

### Launch Broker Container

```bash
sudo docker run -d -p 5659-5661:5659-5661 --net=bridge <docker_account_name>/rexec-broker:latest python rexec_broker.py --client_port 5659 --server_port 5660 --control_port 5661
```

Then get the `network bridge IP address` of the broker with `sudo docker network bridge` (e.g., 172.17.0.2)

### Launch Server Container

```bash
sudo docker run -d --net=bridge <docker_account_name>/rexec-server:latest python rexec_server.py <network bridge IP address> --broker_port 5660
```

## Notes

- If the server breaks down from a bad rexec, kill the existing one and relaunch the server with the above command
