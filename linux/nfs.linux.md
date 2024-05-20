



mkdir /remote
mount /dev/sdc1 /remote/

vi /etc/exports
/remote         192.168.10.10(rw,sync,no_subtree_check)

systemctl restart nfs-kernel-server
systemctl enable --now rpcbind nfs-server
firewall-cmd --add-service={nfs3,mountd,rpc-bind} --permanent
firewall-cmd --reload




