# 3x-srl-nats

An extension of the `3x-srl` project that adds a NATS message broker and a gNMIc telemetry collector. Both the original network and its cloned digital twin publish telemetry to a single NATS service, differentiated by subject prefix.

## Running the lab

```bash
cd 3x-srl-nats
sudo clab deploy --reconfigure
```

## Collecting telemetry

Once the lab is up, gNMIc automatically discovers the SR Linux nodes via the Docker API and subscribes to interface statistics and system performance metrics. Telemetry is published to NATS with the following subject format:

```
<prefix>.<target-name>.<subscription-name>
```

| Network       | Subject prefix | Example subject                              |
|---------------|---------------|----------------------------------------------|
| Original      | `original`    | `original.clab-3x-srl-nats-srl1.srl-if-stats` |
| Cloned (twin) | `twin`        | `twin.clab-gNMIc-action-generated-srl1.srl-if-stats` |

## Connecting to NATS

NATS is exposed on the host at port `4222`. Credentials are in [configs/nats/nats-server.conf](configs/nats/nats-server.conf).

```
address: localhost:4222
username: admin
password: admin123
```

## Cloning the topology

With the lab running, execute the following command to clone the network and deploy a digital twin:

```bash
gnmic --config clone.yaml get --path /system/name --processor clone-topology
```

This introspects the live network via gNMI, generates a matching containerlab topology in `cloned-topology-output/`, and deploys it. The cloned nodes join the shared management network (`3x-srl-nats-mgmt`) so the existing gNMIc instance discovers them automatically and begins publishing their telemetry under the `twin` prefix.

## Tearing down

```bash
# Remove the original lab
sudo clab destroy --cleanup

# Remove the cloned topology (if deployed)
sudo clab destroy -t cloned-topology-output/gnmic.clab.yaml --cleanup
```
