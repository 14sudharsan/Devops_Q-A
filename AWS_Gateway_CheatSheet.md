# ðŸ› ï¸ AWS Gateways â€“ Cheat Sheet  

| **AWS Gateway** | **Purpose / Use Case** | **Azure Equivalent** | **GCP Equivalent** |
|-----------------|------------------------|----------------------|---------------------|
| **Internet Gateway (IGW)** | Enables internet access to resources in a VPC (for public subnets). | Public IP + Azure Internet Gateway (implicit) | Default Internet Gateway (implicit with external IP) |
| **NAT Gateway** | Provides outbound internet access for private subnets, without exposing them to inbound traffic. | NAT Gateway | Cloud NAT |
| **Virtual Private Gateway (VGW)** | Used with AWS Site-to-Site VPN for connecting on-premises networks to AWS VPC. | VPN Gateway | Cloud VPN |
| **Transit Gateway (TGW)** | Central hub for interconnecting multiple VPCs, VPNs, Direct Connect. | Virtual WAN | Network Connectivity Center |
| **Customer Gateway (CGW)** | Represents your on-premises device in a Site-to-Site VPN. | Local Network Gateway | On-Premises Gateway in Cloud VPN/Interconnect |
| **Gateway Load Balancer (GWLB)** | Distributes traffic to 3rd-party virtual appliances (firewalls, IDS/IPS, etc.). | Azure Gateway Load Balancer | No direct equivalent (use External/Internal Load Balancer + Firewall) |
| **Egress-Only Internet Gateway (EOIGW)** | Outbound-only internet access for **IPv6** traffic in a VPC. | IPv6 Outbound-only NAT / No direct service | IPv6 Cloud NAT |
| **PrivateLink / VPC Endpoint Gateway** | Connects VPCs to AWS services privately without internet exposure. | Private Endpoint / Service Endpoint | Private Service Connect |

---

âš¡ **Quick Takeaways**:  
- **Internet-facing?** â†’ IGW (public) or NAT GW (private).  
- **Hybrid Connectivity?** â†’ VGW + CGW (VPN) or TGW (multi-VPC, hybrid).  
- **Service-to-service private connectivity?** â†’ VPC Endpoints (PrivateLink).  
- **Security appliances?** â†’ GWLB.  
- **IPv6 outbound only?** â†’ EOIGW.  