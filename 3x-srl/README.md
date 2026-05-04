# Running this lab

To run this lab, you simply need to cd into the folder and run clab deploy

# Cloning the topology

To clone the topology we simply run the gnmic command as described in the [documentation](https://gnmic.openconfig.net/user_guide/actions/actions/#clone-a-network-topology-and-deploy-it-using-containerlab)

```bash
gnmic --config clone.yaml get --path /system/name --processor clone-topology
```

This will run gnmic with our custom [config.yaml](config.yaml) which we also took from the [documentation](https://gnmic.openconfig.net/user_guide/actions/actions/#clone-a-network-topology-and-deploy-it-using-containerlab). This will produce the specifications for the topology purely based on the config data provided by the switches themselves, which is passed through the processors which we defined in the config.

If everything worked as expected, the topology will now be running twice, the second using a different prefix.
