# Echoprint Ansible Playbooks

## Ansible Playbooks to install echoprint-server on CentOS 6.

## What does this do?

Automatically provisions a server with the neccessary dependencies and software for the Echoprint server.

## Why?

Setting up an echoprint server is complicated. I've repeated the process at least 5 times and wanted to make it faster so I could get on and make cool stuff.

## Dependencies

* Python 2.7
* Ansible 1.4+
* VirtualBox/Vagrant (Optional, if you want to run on a VM)

## Usage

1. Create a cloud server. I reccommend DigitalOcean or Rackspace. **Don't cheap out on the RAM**, this stuff is memory intensive.
2. Login to the server you've created and add your public key to `~/.ssh/authorized_keys`. (You can try and use ansible with a plain text password, but that's naughty.)
3. Add the IP address to `Inventory` and from your local machine run `ansible-playbook -i Inventory ansible/main.yml -u root`.
4. Make yourself a cup of tea.
5. Login to the server and run `ttservctl start` to start TokyoTyrant.
6. Also run `nohup java -Dsolr.solr.home=/opt/echoprint/vendor/server/solr/solr/solr -Djava.awt.headless=true -jar start.jar > output.log 2>&1 &` from `/opt/echoprint/server/solr/solr`. For some reason, ansible doesn't manage to start it properly.
7. Enjoy your newly provisioned server.
8. You can also run the `ansible/ingest.yml` playbook to ingest all of the public data from the Echoprint website. This is a bit buggy at the moment and requires loads of memory. *Don't even try with a 512MB DigitalOcean instance.*