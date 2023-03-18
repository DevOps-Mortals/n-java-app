## Phase 4 - AWS 3-Tier Architecture

### Database (RDS)
- [ ] Deploy Multi-AZ MySQL RDS instance into private subnets
- [ ] Create Security Group allowing port 3306 from App instances and from Bastion Host.

### Tomcat (Backend)
- [ ] Create private facing Network Load Balancer and Target Group.
- [ ] Create Launch Configuration with below configuration.
  + [ ] Tomcat Golden AMI
  + [ ] User Data to deploy .war artifact from JFROG into webapps folder.
  + [ ] Security Group allowing Port 22 from Bastion Host and Port 8080 from private NLB.
- [ ] Create Auto Scaling Group

### NGINX (Frontend)
- [ ] Create public facing Network Load Balancer and Target Group.
- [ ] Create Launch Configuration with below configuration
  + [ ] Nginx Golden AMI
  + [ ] User Data to update proxy_pass rules in nginx.conf file and reload nginx service.
  + [ ] Security Group allowing Port 22 from Bastion Host and Port 80 from Public NLB.
- [ ] Create Auto Scaling Group

---

[Phase 3: Maven Build](/docs/3-maven-build.md)

[Phase 5: App Deployment](/docs/5-app-deployment.md)
