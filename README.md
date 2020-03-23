# Setup Kubernetes Cluster with KOPS 
Currently this has been tested on AWS in later section we will be creatig for other providers
like Google Azure and VMWare ESXI and hyper-V

#### Step # 1 Clone Repo 
``bash
[root@ip-10-0-0-118 ~]# git clone https://github.com/mansurali901/kuberneteswithkops.git
[root@ip-10-0-0-118 ~]# cd kuberneteswithkops/
```
#### Step # 2 Start the installer
```bash
[root@ip-10-0-0-118 kuberneteswithkops]# sh installer
```
#### Step # 3 Provide IAM Keys
```bash
Enter AWS Key ID :  IAMKEYS
Enter AWS Secret Access : IAMSECRETACCESSKEYS
```
#### Step # 4 Supply AWS Region

```bash
Enter Default Region : us-east-1
```
OutPut :
```bash
      Name                    Value             Type    Location
      ----                    -----             ----    --------
   profile                <not set>             None    None
access_key     ****************KWHJ shared-credentials-file
secret_key     ****************Z0jS shared-credentials-file
    region                us-east-1      config-file    ~/.aws/config
````
#### Step # 5 Supply internal Route53 Domain for kubernetes cluster
```bash
Enter domain for kubernetes cluster : demo.upworks
```
#### Suuply S3 Bucket to host KOPS configuration
```bash 
Bucket Name : demo-upworks-east1
```
#### Supply Regions for cluster to spawn in for demo we are using one you can specify multiple *(us-east-1a,us-east-1b)
```bash
Availability Zone for Cluster : us-east-1a
```
#### Supply VPC ID 
```bash
Enter VPC ID to launch cluster : vpc-0555f5dde8e3faf95
```
#### OutPut: 
```bash 
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
/root/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:Vwf4Ucz/Jd1MJYHYe+Y4L9HxcnUXBcISYnlKv8GAp80 root@ip-10-0-0-118.ec2.internal
The key's randomart image is:
+---[RSA 2048]----+
|       .o..*o==o=|
|      ..=.= =ooo.|
|       * * o.o.=o|
|      . E +.o.= X|
|        S .o * +*|
|         .. + + +|
|             + o |
|            . .  |
|             .   |
+----[SHA256]-----+

......



I0323 16:23:47.435245    3851 context.go:249] hit maximum retries 1 with error file does not exist
I0323 16:23:47.484339    3851 context.go:249] hit maximum retries 1 with error file does not exist
I0323 16:23:47.639558    3851 dns.go:94] Private DNS: skipping DNS validation
I0323 16:23:47.973242    3851 executor.go:103] Tasks: 0 done / 89 total; 47 can run
I0323 16:23:48.792248    3851 vfs_castore.go:729] Issuing new certificate: "etcd-clients-ca"
I0323 16:23:49.840966    3851 vfs_castore.go:729] Issuing new certificate: "etcd-manager-ca-events"
I0323 16:23:49.884886    3851 vfs_castore.go:729] Issuing new certificate: "apiserver-aggregator-ca"
I0323 16:23:50.060512    3851 vfs_castore.go:729] Issuing new certificate: "etcd-peers-ca-main"
I0323 16:23:50.577268    3851 vfs_castore.go:729] Issuing new certificate: "ca"
I0323 16:23:50.919569    3851 vfs_castore.go:729] Issuing new certificate: "etcd-manager-ca-main"
I0323 16:23:50.961240    3851 vfs_castore.go:729] Issuing new certificate: "etcd-peers-ca-events"
I0323 16:23:51.394118    3851 executor.go:103] Tasks: 47 done / 89 total; 22 can run
I0323 16:23:51.726000    3851 vfs_castore.go:729] Issuing new certificate: "kube-scheduler"
I0323 16:23:52.142713    3851 vfs_castore.go:729] Issuing new certificate: "kube-controller-manager"
I0323 16:23:52.413771    3851 vfs_castore.go:729] Issuing new certificate: "master"
I0323 16:23:52.884105    3851 vfs_castore.go:729] Issuing new certificate: "apiserver-aggregator"
I0323 16:23:53.288681    3851 vfs_castore.go:729] Issuing new certificate: "kube-proxy"
I0323 16:23:53.908123    3851 vfs_castore.go:729] Issuing new certificate: "kops"
I0323 16:23:53.955404    3851 vfs_castore.go:729] Issuing new certificate: "apiserver-proxy-client"
I0323 16:23:54.295366    3851 vfs_castore.go:729] Issuing new certificate: "kubelet-api"
I0323 16:23:54.344199    3851 vfs_castore.go:729] Issuing new certificate: "kubecfg"
I0323 16:23:54.347346    3851 vfs_castore.go:729] Issuing new certificate: "kubelet"
I0323 16:23:54.639279    3851 executor.go:103] Tasks: 69 done / 89 total; 18 can run
I0323 16:23:55.223374    3851 executor.go:103] Tasks: 87 done / 89 total; 2 can run
I0323 16:23:55.834567    3851 executor.go:103] Tasks: 89 done / 89 total; 0 can run
I0323 16:23:55.834689    3851 dns.go:155] Pre-creating DNS records
I0323 16:23:56.559207    3851 update_cluster.go:294] Exporting kubecfg for cluster
W0323 16:23:56.619555    3851 create_kubecfg.go:76] Did not find API endpoint for gossip hostname; may not be able to reach cluster
kops has set your kubectl context to demo.upworks

Cluster is starting.  It should be ready in a few minutes.

Suggestions:
 * validate cluster: kops validate cluster
 * list nodes: kubectl get nodes --show-labels
 * ssh to the master: ssh -i ~/.ssh/id_rsa admin@api.demo.upworks
 * the admin user is specific to Debian. If not using Debian please use the appropriate user based on your OS.
 * read about installing addons at: https://github.com/kubernetes/kops/blob/master/docs/addons.md.
 ```
Step # Validate Cluster 
```bash
[root@ip-10-0-0-118 kuberneteswithkops]# export KOPS_STATE_STORE=s3://demo-upworks-east1
````
```bash
[root@ip-10-0-0-118 kuberneteswithkops]# kops validate cluster
Using cluster from kubectl context: demo.upworks

Validating cluster demo.upworks

INSTANCE GROUPS
NAME			ROLE	MACHINETYPE	MIN	MAX	SUBNETS
master-us-east-1a	Master	t3.medium	1	1	us-east-1a
nodes			Node	t3.large	2	2	us-east-1a

NODE STATUS
NAME				ROLE	READY
ip-10-0-51-0.ec2.internal	node	True
ip-10-0-51-219.ec2.internal	node	True
ip-10-0-51-37.ec2.internal	master	True

Your cluster demo.upworks is ready
```
