By running get --path /system/name --processor clone-topology, you are doing the following:

- Fetching a single piece of telemetry data (/system/name) via a one-off get request.
- Forcing that data to go through the clone-topology processor (using --processor).
- As soon as the processor receives that single event, its event-trigger fires off the sequence of automated actions (chassis -> lldp -> read_config -> etc.) defined in your file.
