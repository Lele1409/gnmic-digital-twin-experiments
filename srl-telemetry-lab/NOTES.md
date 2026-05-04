# Install gnmic
bash -c "$(curl -sL https://get-gnmic.openconfig.net)"

# Get capabilities from a device
gnmic capabilities -a 172.80.80.11 --skip-verify -u admin -p NokiaSrl1! | less

# Subscribe 
gnmic subscribe --address 172.80.80.11 --username admin --password NokiaSrl1! --skip-verify --path /interface/traffic-rate/in-bps --mode stream --encoding json