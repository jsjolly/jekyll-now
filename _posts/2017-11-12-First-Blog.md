---
layout: post
title: My First Blog
---

This is my first blog
Using 3rd party DLP with Exchange Online


Although Office 365 comes with a robust built-in DLP for Exchange online, SharePoint Online and OneDrive for Business but still there are customers who want to use 3rd party DLP solution with Exchange online. Reason for this varies from protecting existing investment on DLP to opting Office 365 SKU's which don’t have DLP bundled into them to specific requirements around integration with Network, Endpoint and Web DLP. Whatever might be the reason, if customer decides to use 3rd party DLP solution along with Exchange online, placement of DLP solution and email routing becomes overly critical. Typically, there are 3 possible deployment options/ topologies in which EXO and 3rd party DLP can be integrated.
 
1.	Using existing on-premise DLP server.
2.	Using SaaS based service from DLP providers.
3.	Installing DLP server on IaaS model such as Azure. 
 
 
Option 1: Using existing on-premise DLP server. 
======================================= 
If customer decides to use their existing on-premise DLP solution, then their email routing will look something like depicted in Figure1. This is extremely easy to configure if they have Exchange Hybrid environment as all they need to configure is "Centralized Mail Transport"  but in case they have some other mailing solution even then it is simple as they just need to configure Own email server Connector for email routing from Office 365 to on-premise servers.
 
  
 Figure1: Email routing between Exchange online and On-premise DLP.

 
Option 2: Using SaaS based service from DLP providers.
=============================================
If customer decides to use SaaS based DLP solution, then their email routing will look something like depicted in Figure2. This is same as above as they just need to configure Partner organization Connector for email routing from Office 365 to SaaS based DLP.
 
 
Figure2: Email routing between Exchange online and Hosted DLP. 
 
 
Option 3: Installing DLP server on IaaS model such as Azure. 
================================================
If customer decides to install DLP solution on Azure, then their email routing will look something like depicted in Figure3. This is bit tricky as we know that sending outbound e-mail to external domains directly from an e-mail server hosted in Azure compute services is not supported. Microsoft recommends that Azure customers employ authenticated SMTP relay services such as Exchange Online Protection to send e-mail from Azure VMs or from Azure App Services.
 
In case customer has emails hosted on Office 365 and Azure is being used to host the DLP VM's then we need to configure email routing in such manner that all "Outgoing" emails from Office 365 should be forwarded to DLP on Azure and post DLP has processed the messages, they should be routed back to Office 365. Now if not configured properly, this can cause:
1.	Email Loop between Office 365 and DLP
2.	Excess outgoing traffic from Azure DLP to Office 365 which may have cost implications.

  
Figure3: Email routing between Exchange online and DLP hosted on Azure

To avoid the 2 issues mentioned above, we need conditional email routing which means that we need to configure a Connector pointing to Public IP of VM running DLP solution and configure a Transport Rule invoking the connector and allows EOP to route emails outside if mails are coming from DLP server. 
 
 
Figure4: Connector configuration		 
Figure5: Transport Rule configuration

With these configurations in place, only Outgoing emails will get routed to DLP and back to Office 365.

 






