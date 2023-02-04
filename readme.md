# Instant Canto Node

This script will connect to a server, deploy and state sync a canto node and then setup an Nginx server for this node.The only part you have to do by hand is run 'certbot' to get an ssl key. The result is a fully production ready server in less than 10 minutes.

## Requirements

1) Deploy a Fedora VM with at least 4gb of RAM, 8gb is recomended. Storage isn't relevant, when the disk becomes full delete .canto and run this script again, it will just-reboostrap the node in a few minutes

2) edit `hosts` to contain your intended hostname and the ip address of the target server

3) Run the playbook You'll probably have to install Ansible

```
ansible-playbook -i hosts canto.yml
```

4) now that the playbook has finished login to your server and run the following, follow the prompts to get a certificate, remmeber you need to point your domain name at the servers IP address!

```
certbot --nginx 
```

It may take a few minutes to state-sync you'll probably have your ssl certificate ready before it's done. You can monitor the node status using the command `journalctl -u canto.service --output=cat -f` 

## Enabled RPC

* Port 443 (default) EVM RPC
* Port 8545 EVM RPC
* Port 8546 EVM Websockets
* Port 22657 Cosmos ABCI + Websockets
* Port 9090 Cosmos GRPC
* Port 9091 Cosmos GRPC-web
* Port 1317 Cosmos Legacy API