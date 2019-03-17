# Transit Gateway in a Multi-Account Deployment

Transit Gateway Overview
------------------------
The Transit GateWay (TGW) feature provides a managed virtual router for AWS VPC customers. Multiple VPCs, VPNs and DX Gateways can be attached to the TGW to perform IP routing between them. Multiple route tables can live inside a single TGW and be routed according to the customer business use case.

With Transit Gateway, customers can implement policies for how VPCs communicate with each other and with their on-premises networks. Transit Gateway gives customers the ability to simplify interconnectivity within their networks enabling them to scale workloads across a large number of VPCs and across accounts. While enabling connectivity at scale, Transit Gateway also provides stronger operational controls and improved security.

Fundamentally when you connect to a Transit Gateway with your VPC an elastic network interface (ENI) is created within the subnet that you specified. The ENI assumes an IP address from that subnet and the VPC route table can be updated to reflect the desired CIDR range to communicate across the TGW service. The below diagram represents the logical construct of the ENI insertion with a VPC.

![tgw-overview](./transit-gw.png)

Developing Terraform
--------------------
