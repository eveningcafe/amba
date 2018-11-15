```
sudo -i
```
```
nano /etc/ssh/sshd_config
sua PermitRootLogin yes
service ssh reload
```

```
echo "192.168.2.53    node1.bd" >> /etc/hosts
echo "192.168.2.194    node2.bd" >> /etc/hosts
```

```
apt-get install ambari-agent
```

Sửa ambari-agent.ini:
```
nano /etc/ambari-agent/conf/ambari-agent.ini
[server]
hostname=node1.bd
url_port=8440
secured_url_port=8441
```
Start the agent on every host in your cluster.

```
ambari-agent start
```
<!--```-->
<!--sudo -i-->
<!--ssh-keygen -t rsa-->
<!--cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys-->
<!--chmod og-wx ~/.ssh/authorized_keys -->
<!--ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.2.194-->
<!--```-->

