# Prerequisites

Install clab and gNMIc:

## Installing clab
To install the latest version of Containerlab (clab), use the official installation script:

```bash
bash -c "$(curl -sL https://get.containerlab.dev)"
```

For more details, visit the [Containerlab installation guide](https://containerlab.dev/install/).

## Installing gNMIc
To install the latest version of gNMIc, use the official installation script:

```bash
bash -c "$(curl -sL https://get-gnmic.openconfig.net)"
```

For more details, visit the [gNMIc installation guide](https://gnmic.openconfig.net/install/).

# Recommended vscode plugin

It is recommended to use the containerlab plugin to allow for visualizations of the configuration and/or deployments of containerlab topologies. 

# Projects

## 3x-srl

[3x-srl/README.md](3x-srl/README.md)

> 3x-srl is an environment containing three srl switches (as the name suggests) and aims at evaluating gNMIc's capabilities in cloning a topology for further use as a digital twin

## srl-telemetry-lab

[srl-telemetry-lab/README.md](srl-telemetry-lab/README.md)

> srl-telemetry-lab is an existing clab topology which comes with gnmic, prometheus, and grafana preconfigured. We use this topology by expanding it with our own NATS message broker, to test outputting telemetry from gnmic to NATS

## 3x-srl-nats

[3x-srl-nats/README.md](3x-srl-nats/README.md)

> 3x-srl-nats extends 3x-srl with a NATS broker and a gNMIc telemetry collector. Both the original network and the cloned digital twin publish telemetry to a single NATS service, using the subject prefixes `original` and `twin` to differentiate them. gNMIc uses the Docker API to discover nodes dynamically, so the cloned topology is picked up automatically after deployment.
