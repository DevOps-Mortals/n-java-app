## Maven Build

- [ ] Create EC2 instance using Maven Golden AMI
- [ ] Clone Bitbucket repository to VSCode and update the pom.xml with Sonar and JFROG deployment details.
- [ ] Add settings.xml file to the root folder of the repository with the JFROG credentials and JFROG repo to resolve t>- 
- [ ] Update application.properties file with JDBC connection string to authenticate with MySQL.                        
- [ ] Push the code changes to feature branch of Bitbucket repository                                                   
- [ ] Raise Pull Request to approve the PR and Merge the changes to Master branch.                                      
- [ ] Login to EC2 instance and clone the Bitbucket repository                                                          
- [ ] Build the source code using  maven arguments "-s settings.xml"                                                    
- [ ] Integrate Maven build with Sonar Cloud and generate analysis dashboard with default Quality Gate profile.
