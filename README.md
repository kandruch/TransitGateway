# Transit Gateway in a Multi-Account Deployment

The Transit GateWay (TGW) feature provides a managed virtual router for AWS VPC customers. Multiple VPCs, VPNs and DX Gateways can be attached to the TGW to perform IP routing between them. Multiple route tables can live inside a single TGW and be routed according to the customer business use case.

Transit Gateway Overview
------------------------

With Transit Gateway, customers can implement policies for how VPCs communicate with each other and with their on-premises networks. Transit Gateway gives customers the ability to simplify interconnectivity within their networks enabling them to scale workloads across a large number of VPCs and across accounts. While enabling connectivity at scale, Transit Gateway also provides stronger operational controls and improved security.

Fundamentally when you connect to a Transit Gateway with your VPC an elastic network interface (ENI) is created within the subnet that you specified. The ENI assumes an IP address from that subnet and the VPC route table can be updated to reflect the desired CIDR range to communicate across the TGW service. The below diagram represents the logical construct of the ENI insertion with a VPC.

![tgw-overview](./transit-gw.png)

AWS Resource Access Manager And Transit Gateway
-----------------------------------------------
In order to use TGW across multiple accounts you need to leverage AWS Resource Access Manager which grants you the ability to share selected resources across your Organization, OU unit or selected accounts.

To enable sharing across the organization you first need to enable the feature. Alternatively you enable automatic resource sharing when you add additional accounts to AWS Organizations using the command below.

```
aws ram enable-sharing-with-aws-organization --region ca-central-1
```

```
aws ram create-resource-share --name TransitGateway --resource-arn arn:aws:ec2:ca-central-1:<account#>:transit-gateway/tgw-xxxxxxxxxxxxxxxxx \
--principals arn:aws:organizations::<account#>:organization/<o-3axxxxxx> \
--tags key=Name,value=TransitGatewayRAM \
--region ca-central-1
```

Transit Gateway CloudFormation
-----------------------------------------------
![tgw-overview](./transitgatewayV2.yml)
