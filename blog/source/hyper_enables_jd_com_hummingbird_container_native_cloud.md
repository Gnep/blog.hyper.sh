title: How Hyper’s technology enables JD.com to build "Hummingbird", a Container-native Cloud
date: 2017-04-14 21:00:00 +0800
author: hyper
tags:
    - Docker
    - JD.com
    - Container
    - Container hosting

preview: JD.com, China's second largest online retailer have chosen to use Hyper tech for their Docker cloud offering JCloud Hummingbird!

---

[JD.com](https://jd.com) is a Chinese e-commerce giant. It is one of the largest online B2C retailers in China by transaction volume and revenue, second only to Alibaba. Since 2015, JD.com has offered a public cloud service, called JCloud. Similar to other public clouds, JCloud offers both traditional IaaS and PaaS.

### Container-native Cloud
In 2017, JCloud's goal is to provide greater value to its customers, as well as differentiate itself from other competitors. In the e-commerce market, a single discount event or holiday program will bring in unimaginable traffic and transactions to merchants. As an example, during the ***2016 JD.com 6.18 Carnival Day*** annual sales event, over 100 million orders were placed. Such volume spikes lead to huge cloud resource needs, and as such, the provisioning speed becomes a significant bottleneck and pain point.

To **speed up resource provisioning** and **reduce deployment overhead**, JCloud decided to work with Hyper to build a new container-native IaaS product: JCloud Hummingbird. Put simply, Hummingbird is a Docker hosting service, in which the container replaces the VM as the base compute instance, just like [Hyper.sh](https://hyper.sh/) itself. While that might sound similar to other Container-as-a-Service (CaaS) offerings in the market, the platform's uniqueness is that the containers are completely isolated from one another, meaning that multiple tenants' containers are safe to run over shared infrastructure, without worrying about having to add a secure boundary.

The major side benefit of the strong container isolation is that developers don't have to provision VM instances before deploying containers. Instead, they simply launch containers as they normally would launch VMs. In other words, **(isolated) containers become the new infrastructure**. This change brings very significant benefits:

- **5-second Provisioning**: Compared with the slow boot performance of VMs, containers are provisioned in seconds. Resulting in an improved developer experience and higher productivity.
- **Super Elastic**: Fast provisioning speeds enables auto-scaling to take place “just-in-time”. No more over-provisioning.
- **Cost Effective**: The combination of per-second billing and super fast provisioning, makes Hummingbird extremely cost effective.
- **Docker Image Workflow**: Containers replace VMs as the infrastructure building block and deliverable artefact meaning that developers who are used to Docker can get started quickly.
- **Cattle vs Pets**: Without a long-running VM cluster, there are no ‘pets’ in infrastructure that need nursing. Everything can be treated like cattle! Disposable, and easy to reproduce. 
- **Immutable Infrastructure**: Container infrastructure is inherently immutable, eliminating the headache of VM configuration drift.

### Under the hood
The secret sauce behind Hummingbird is Hyper's secure Docker runtime technology called [runV](https://github.com/hyperhq/runv). Different from runC, which is based on Linux containers, runV containers are powered by virtualization. It creates a VM instance that boots a minimized Linux kernel, and loads Docker images as "rootfs", then the kernel launches [HyperStart](https://github.com/hyperhq/hyperstart), a tiny init service, which runs applications specified in `CMD` and `ENTRYPOINT` flags. That entire process takes less than 100ms to complete, which is orders of magnitude faster than traditional VMs and almost as fast as regular Linux containers. Combined with other techniques, runV is able to match runC, in both features and boot-performance. All of this makes runV operate like a container, but with the benefits of [hardware-enforced](https://en.wikipedia.org/wiki/X86_virtualization) VM security. 

Combining the best of VMs and Containers opens up interesting new opportunities. The base of the Hummingbird stack is bare metal, outfitted with the Hyper container engine for provisioning and container management, and using Kubernetes for container orchestration. Other cloud functions are controlled by components taken from OpenStack, including Keystone, for identity management and authentication; Neutron, for network management; and Cinder/Ceph, for storage volume management.

### Summary
Since the beta release in January, Hummingbird has seen 300% month on month growth and the service is being continually expanded to meet the needs of [JD.com’s](http://www.jd.com/) developers and customers. Lijing Guo, Head of Product Management of JCloud, told us: "With Hummingbird, we are able to provide a way for our customers to provision containers in a simple, fast, secure, and cost-effective manner. Development speed is 3x to traditional IaaS, but with 50% cost reduction. The project is a great success!"

We’re thrilled to see a company the size of JD.com taking advantage of the same ease of use that Hyper.sh customers have been enjoying since August 2016 and look forward to working with them further as they expand.
