<img width="1169" height="540" alt="image" src="https://github.com/user-attachments/assets/2fad7705-b86b-4a2a-9377-983fd75be900" />


I created a custom VPC with a /16 CIDR block, giving the network 65,536 available IP addresses. I chose to build the VPC manually rather than using the "VPC and more" wizard so I could understand each component individually and have full control over the network design.


<img width="1291" height="525" alt="image" src="https://github.com/user-attachments/assets/221d3829-222e-449f-be32-ac9c3ef05cc4" />

I enabled DNS hostnames on the VPC so that EC2 instances automatically receive public DNS names alongside their public IPs. This is required for the Application Load Balancer to function correctly.



<img width="1356" height="343" alt="image" src="https://github.com/user-attachments/assets/759c6975-0865-4a19-889c-3a6ed499f8c5" />


I created and attached an Internet Gateway to the VPC. The IGW is what allows resources in the public subnets to communicate with the internet. Without it, the VPC is completely isolated — no inbound or outbound internet traffic is possible regardless of any other settings.


<img width="1363" height="380" alt="image" src="https://github.com/user-attachments/assets/2235ef2b-22cb-4d72-bc3f-858e25e33151" />


I created four subnets split across two Availability Zones — two public and two private. Public subnets host resources that need internet access (EC2 instances and the ALB). Private subnets host the RDS database, which should never be directly reachable from the internet. Spanning both AZs from the start means the architecture has no single point of failure at the network level.


<img width="1339" height="456" alt="image" src="https://github.com/user-attachments/assets/f04e10b5-b5a6-4f4c-9992-51bef368e745" />


I created a public route table with a route sending all internet-bound traffic (0.0.0.0/0) to the Internet Gateway. This route is what actually makes a subnet public — the name alone means nothing. Associated both public subnets to this table so EC2 instances and the ALB can reach and be reached from the internet.




<img width="1342" height="404" alt="image" src="https://github.com/user-attachments/assets/888209e9-7df4-4777-add3-43872c257a73" />


I created a private route table with no internet route , only the default local VPC route exists. Associating the private subnets to this table means RDS has no path to or from the internet at the network level. This is a deliberate architectural decision: even if a security group were misconfigured in the future, the database still cannot be reached from outside the VPC.


<img width="1349" height="467" alt="image" src="https://github.com/user-attachments/assets/359c3466-006c-4434-9556-dcddbe5a06ac" />

I created a dedicated security group for the Application Load Balancer that accepts HTTP traffic from anywhere on the internet. The ALB is the only resource in the architecture with a public-facing inbound rule — everything behind it is locked down to only accept traffic from the ALB itself.

<img width="1353" height="452" alt="image" src="https://github.com/user-attachments/assets/c7d75c3d-276a-4542-8225-9c284fbfd933" />

I created the EC2 security group with two inbound rules. HTTP traffic is only accepted from the ALB security group — not from the internet directly. This means even if someone discovers an EC2 instance's public IP, they cannot reach it. SSH is restricted to my IP only to prevent brute-force login attempts, which are extremely common on port 22 when left open to the world.


<img width="1347" height="460" alt="image" src="https://github.com/user-attachments/assets/29972ab1-7a99-4099-b1fc-f7edf81d5284" />

Created the RDS security group allowing MySQL connections on port 3306 from the EC2 security group only. The database is only queryable by the web servers — not by the load balancer, not from my laptop, not from anywhere else. This is the least-privilege principle applied at the database tier: grant only the minimum access necessary and nothing more.


