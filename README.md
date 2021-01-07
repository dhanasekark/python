python
======
Hi,


On Thu, Jan 07, 2021 at 02:50:48AM +0530, Dhanasekar Kandasamy wrote:
> Hi,
>
> We have an OpenStack Environment with 5000+ VMs running currently. I want
> to apply some common Security Group to all my running VMs.
>
>    - Common Security Group (SEC_GRP_COMMON) has around 700 rules.
>    - This Security Group (SEC_GRP_COMMON) has been shared to all the

>    OpenStack Projects using Role-Based Access Control (RBAC).
>    - Wanted to apply this Security Group (SEC_GRP_COMMON) to all the

>    running VMs in the Cloud
>
> *Question 1*: With the above scenario, what will happen if I attach this

> Security Group(with 700+ rules) to all the 5000+ VMs? Will there be any
> performance issue/impact for the same (CPU utilization, Memory etc. in the
> Compute Server or Performance issues in application running in the VMs)

It all depends on what plugin and agents You are using. E.g. if You are using
ML2 plugin with openvswitch agents on compute nodes, for sure You will see
issues with performance of agent as it will take some time to apply those rules
to all ports on the compute nodes.
Of course if You have many compute nodes and only few VMs on each of them, then
it should be pretty fast. If You have compute nodes with e.g. 100-200 VMs on one
compute, it can take more than 10 minutes to apply those SG to all ports.

Another question is what firewall driver You are using. In case of ML2/OVS it
can be iptables_hybrid or openvswitch driver and performance of both can be
different.
You can find some comparisons and benchmarks in the Internet. For example [1] or
[2].
IIRC there were also some talks about that on summits so You can look for some
recordings too.

>
> *Question 2*: Is there any recommendations or benchmark data for maximum

> number of rules in the Security Group in OpenStack cloud?
>
>
> Thanks,
>
> Dhana

[1] https://thesaitech.wordpress.com/2019/02/15/a-comparative-study-of-openstack-networking-architectures/
[2] https://software.intel.com/content/www/us/en/develop/articles/implementing-an-openstack-security-group-firewall-driver-using-ovs-learn-actions.html?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%3A+ISNMain+%28Intel+Developer+Zone+Articles+Feed%29


--
Slawek Kaplonski
Principal Software Engineer
Red Hat

Hi,

We have an OpenStack Environment with 5000+ VMs running currently. I want to apply some common Security Group to all my running VMs.
Common Security Group (SEC_GRP_COMMON) has around 700 rules.
This Security Group (SEC_GRP_COMMON) has been shared to all the OpenStack Projects using Role-Based Access Control (RBAC).
Wanted to apply this Security Group (SEC_GRP_COMMON) to all the running VMs in the Cloud
Question 1: With the above scenario, what will happen if I attach this Security Group(with 700+ rules) to all the 5000+ VMs? Will there be any performance issue/impact for the same (CPU utilization, Memory etc. in the Compute Server or Performance issues in application running in the VMs)

Question 2: Is there any recommendations or benchmark data for maximum number of rules in the Security Group in OpenStack cloud?



Thanks,

Dhana

