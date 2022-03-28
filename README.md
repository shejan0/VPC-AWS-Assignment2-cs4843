# Assignment 2
## By Shejan Shuza
### Cloud Computing


For most businesses, it is required that your entire business internet presence exists on one consistent Domain name, this can be extremely challenging when the nature of your software may need to exist across multiple machines to run effectively and these systems are physically not in the same place, or need to be separeted, this also can cause concerns for security where if the database which your software stack uses is mounted to the same address as your domain name, it maybe possible to push database commands through the public internet, and critical data maybe shared.

To replicate such a situation, availabilty zones on Amazon Web Services are used to replicate distanted systems, of which are in a VPC, or a Virtual Private Cloud network, which conjoins the entire infrastructure into one colloquial net, this way a single domain name can be used. 

## Files

- [Network](network.yaml)
- [Servers and security system](server&#32;and&#32;security.yaml)
- [Storage and Database system](storage&#32;and&#32;database.yaml)

These 3 files specify an architecture that has 2 subnets in 2 availability zones.

In each availability zone, there is one public and private subnet. 

In the public subnet of each availability zone, which is attached directly to a Internet Gateway, there exists one EC2 instance that is meant to be used as a jumperbox (to access the private subnet systems) and a NAT Gateway for the private subnet in the availability zone. There is also set up for EIP and Routing Tables within this subnet which is used for effectively routing the public subnet's data.

In the private subnet of each availabilty zone, which is attached to the NAT Gateway of the public subnet, there exists two EC2 instances. One with a installation of Apache2 webserver to host a website, and one with a installation of MySQL Server and 10GB of EBS storage attached. There also exists routing tables for going through the NAT gateway, and passing traffic into the public subnet.

The idea of the architecture is that the public webserver on each availability zone can get into Database server through the NAT Gateway, and can commit mySQL transactions to the database EC2 instance. 

![Diagram](Diagram.drawio.png)

