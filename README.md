# amba

### Tổng quan:


Ambari là công cụ cho provisioning, managing, monitoring và securing Apache Hadoop clusters. Là một phần của Hortonworks Data Platform (HDP), nó sẽ deploy cluster dựa trên các packages từ các hortonworks repo.

Trong quá trình deploy HDP cluster, nó sẽ dùng 3 repo :
- Ambari: Chứa package của ambari server , ambari agent và các packages khác cho monitor cluster
- HDP: Chứa Hadoop "stack" packages: như hadoop, pig, hive, oozie, hbase, zookeeper...
- HDP-UTILS: Chứa các packages bổ trợ, vd Nagios and Ganglia.

![](../images/ambari_repo.png)

Trong quá trình cài HDP cluster, bao giờ ta cũng thực hiện tuần tự:
- Add repo ambari, cài ambari server cho node monitor, ambari agent cho các node khác
- Thiết lập HDPHDP-UTILS repo cho ambari server . cụm dùng các package bổ trợ trong này
- Thiết lập HDP repo cho ambari server, các node khác trong cụm sẽ biết để dùng các repo này để tải hadoop về
Theo defaut, các repo này đặt của tại domain hortonworks.com
Ta nên dùng local repo triển khai, giúp giảm độ trễ khi download package ở xa, không bị phụ thuộc các kho khác 

### Các tạo các local repo và thiết lập ambari dùng local repo

1) Tạo local repo:
- Xác định HDP repository gốc mà sẽ download package về
<br/> HDP có danh sách repo từ 2.2->2.5 tại đây:
<br/>https://docs.hortonworks.com/HDPDocuments/Ambari-2.4.2.0/bk_ambari-installation/content/hdp_stack_repositories.html<br/>
<br/> Ambari version pike có thể deploy là 2.4 và 2.5. danh sách tại đây:
<br/> https://docs.hortonworks.com/HDPDocuments/Ambari-2.4.2.0/bk_ambari-installation/content/ambari_repositories.html<br/>
- Dowload các package trong các repo về máy 
Ví dụ môi trường ubuntu 14.04 và Ambari plugin 2.4 ( cũng là cluster sahara có thể tạo ra trong bản pike) . Dowload:
```
cd ~
wget http://public-repo-1.hortonworks.com/ambari/ubuntu14/2.x/updates/2.4.2.0/ambari-2.4.2.0-ubuntu14.tar.gz
wget http://public-repo-1.hortonworks.com/HDP/ubuntu14/2.x/updates/2.5.3.0/HDP-2.5.3.0-ubuntu14-deb.tar.gz
wget http://public-repo-1.hortonworks.com/HDP-UTILS-1.1.0.21/repos/ubuntu14/HDP-UTILS-1.1.0.21-ubuntu14.tar.gz
```
Tổng 3 file tầm 10GB
- Tạo local repo:

https://github.com/trananhkma/Local-Repository

2) Thiết lập ambari dùng local repo

3) Chọn vào dùng local repo khi tạo cluster bằng ambari

### Ref
https://www.slideshare.net/hortonworks/ambari-using-a-local-repository
https://github.com/trananhkma/Local-Repository
