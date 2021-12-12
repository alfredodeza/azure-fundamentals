LP: https://docs.microsoft.com/en-us/learn/paths/az-900-describe-core-azure-services/

## Azure Compute Services

### Virtual Machines (VMs)

Definition: Emulate physical machines. These provide IaaS.

### Virtual machine scale sets

Definition: Deploy and manage set of identical VMs. Supports autoscale

### Containers and K8s

Definition: Azure compute resources that you can use to deploy+manage containers. Quickly create, scale, and stop dynamically.

### Azure App Service

Definition: a Paas that allows to build, deploy, and scale web/mobile/API apps on any platform.

Types:

* Web apps
* API apps
* Webjobs (for background tasks)
* Mobile apps

Service handles:

* Deployment and management 
* Can secure endpoints
* Scaling of sites
* Built-in load balancing and traffic manager

### Azure Functions

Definition: Serverless code that does not require managing the underlying platform.

Use them for

* Running on a timer
* Trigger over HTTP
* With queues.

### When to use VMs

* Total control of the OS
* To use custom Software 
* Custom hosting configurations

Example scenarios:

* In testing/development
* When extending your datacenter to the cloud
* For disaster recovery (quickly provisioning VMs)


### Azure Batch

Definition: Allows large-scale parallel and high-performance computing (HPC) batch jobs. Can scale to thousands of VMs

Batch can:

* Start a pool of compute
* Install apps + stage data
* Run jobs 
* Identify failures
* Reque work
* Scale down

### Azure Logic Apps

Definition: It executes workflows, designed to automate business scenario from predefined logic blocks

Similar to Functions. Both can get triggered with logic based on event.

Workflows are persisted in JSON. 

Declarative and stateful. Runs only in the cloud.

### Azure Virtual Desktop

Definition: A Windows desktop virtualization service in the cloud. 

Works across devices like Windows, Mac, iOS, Android, and Linux. Including most browsers

Use it because:

* Provides flexibility (supported across devices)
* Enhanced security. Data+apps are separate from the local hardware

* **Simplified management**: with Azure AD + RBAC
* **Performance management**: Can load balance on VM host pools
* **Multi-session**: Allows concurrent users on Windows 10

Reduce costs by bringing your own licenses. Available with no extra costs for existing MSFT 365 license.
Save on compute by buying 1 or 3 year Azure reserved virtual machine instances.

## Azure Virtual Network fundamentals

* Isolate
* Communicate over the internet
* Communicate between Azure resources
* Communicate with on-premise
* Route+filter traffic
* Connect virtual networks

**Internet communications**: VMs can connect to the internet _by default_
**Communicate between Azure resources**: with Virtual networks, or service endpoints (from an Azure resource)
**Communicate with on-premise**: 
 * via Point-to-site (typical VPN)
 * Site-to-site (everything appears on the same network)
 * Azure ExpressRoute: dedicated private connection to Azure (not over the internet)
 
**Route Network traffic**
* Route tables: defines rules for directing network traffic
* Border Gateway Protocol: (BGP) Propagate on-premises BGP to Azure virtual networks

**Connect virtual networks**: With network peering. Peering allows connecting virtual networks together.

## Azure VPN gateway fundamentals


### VPN Gateway 

Definition: A type of virtual network gateway.

They enable:

* Connecting on-premise datacenter to virtual networks (site-to-site)
* Connecting individual devices to virtual networks (point-to-site)
* Connect virtual networks to other virtual networks (network-to-network)

**Only 1 VPN gateway per virtual network**

Supports two types:

**Policy-based**
* IKEv1 only
* Static-routing: Combinations of address prefixes control traffic. Source+destination are declared in policy (**not** in routing tables)
* Mainly used for compatibility with legacy VPN

**Route-based**
Use it for:
* point-to-site, connections between virtual networks, multisite, coexistence with Azure ExpressRoute
* IKEv2 support
* Wildcard (any-to-any) traffic selectors
* Dynamic routing protocols. Source/Destination networks don't need to be statically defined. Supports Border Gateway Protocol (BGP)

**Gateway sizes**
* Basic (does not support Border Gateway Protocol)
* VpnGw1
* VpnGw2
* VpnGw3

**Required Azure resources**
* Virtual Network
* Gateway subnet
* Public IP 
* Local network gateway
* Virtual network gateway
* Connection resource

### HA for VPN gateways

**Active/Standby**: By default VPN gateways are deployed as two instances. Automatic failover. Connections can be interrupted
**Active/Active**: Use with Border Gateway Protocol, create each VPN with unique IPs but separate tunnels from on-premise device.
**ExpressRoute Failover**: If an ExpressRoute connection fails, connectivity can fail over to traffic over the internet with the VPN
**Zone-redundant gateways** For regions that support AZs, VPNs can be deployed with zone-redundancy. Requires a Standard public IP (not a **basic** IP)


## Azure ExpressRoute Fundamentals