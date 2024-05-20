


##  vmware.esxi.cli.network.define.md
```
esxcli network vswitch standard add -v vSwitch0
esxcli network vswitch standard add -v vSwitch1

esxcli network vswitch standard portgroup add -p VLAN100-SALES -v vSwitch1
esxcli network vswitch standard portgroup set -p VLAN100-SALES -v 100

esxcli network vswitch standard portgroup add -p VLAN101-Trust -v vSwitch1
esxcli network vswitch standard portgroup set -p VLAN101-Trust  -v 101

```


## change name of a vswitch

```
configstorecli config current get -c esx -g network_vss -k switches > vswitch.json
```
### edit and save
```
configstorecli config current set -c esx -g network_vss -k switches -i vswitch.json --overwrite

```



###  esxi.ssl.cert.trust.linux   GENERATE with FQDN


esxcli system hostname set --fqdn=MY_SUBDOMAIN.MYDOMAIN.LOCAL
cd /etc/vmware/ssl
/sbin/generate-certificates
/etc/init.d/hostd restart && /etc/init.d/vpxa restart
scp -o PubkeyAuthentication=no  root@x.y.z.w:/etc/vmware/ssl/castore.pem .
sudo cp  castore.pem /etc/pki/ca-trust/source/anchors
sudo update-ca-trust extract


###  esxi.ssl.cert.trust.linux   ONLY TRUST
scp x.y.z.w:/etc/vmware/ssl/castore.pem .
sudo cp castore.pem  /etc/pki/ca-trust/source/anchors/
update-ca-trust


### very busy server
/etc/init.d/hostd restart && /etc/init.d/vpxa restart


### vm.add.poweron.vm.nic
vim-cmd vmsvc/devices.createnic 1 e1000 InternalPG-VLAN11


