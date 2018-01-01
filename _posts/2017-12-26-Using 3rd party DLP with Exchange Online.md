---
layout: post
#title: Using 3rd party DLP with Exchange Online

---
Although Office 365 comes with a robust built-in DLP for Exchange Online, SharePoint Online and OneDrive for Business, yet there are customers who have invested in 3rd party DLP solutions and would want to use them with Exchange Online. Reason for this varies from protecting existing investment on DLP to opting Office 365 SKU's which don’t have DLP bundled into them or specific requirements around integration with Network, Endpoint and Web DLP. Whatever might be the reason, if customer decides to use 3rd party DLP solution along with Exchange Online, placement of DLP solution and email routing becomes overly critical.

Typically, there are 3 possible deployment options/ topologies in which Exchange Online and 3rd party DLP can be integrated. 

1. Using existing on-premise DLP server.
2. Using SaaS based service from DLP providers.
3. Installing DLP server on IaaS model such as Azure.

### Option 1: Using existing on-premise DLP server.
For an existing on-premise DLP solution, the email routing will look like [Figure1]. This is extremely easy to configure if you have Exchange Hybrid environment as all you need to configure is [Centralized Mail Transport](https://technet.microsoft.com/en-us/library/jj659055(v=exchg.150).aspx). In case you have some other mailing solution even then it is simple as you just need to configure [Own email server Connector](https://technet.microsoft.com/en-us/library/jj659055(v=exchg.150).aspx) for email routing from Office 365 to on-premise servers.

![](/images/Figure1.jpg)

 
### Option 2: Using SaaS based service from DLP providers.
For a SaaS based DLP solution, the email routing will look like Figure2. This is similar to option 1 as you just need to configure [Partner organization Connector](https://technet.microsoft.com/en-us/library/dn751021(v=exchg.150).aspx) for email routing from Office 365 to SaaS based DLP.

![](/images/Figure%202.jpg) 
 
### Option 3: Installing DLP server on IaaS model such as Azure. 
For a DLP solution installed on Azure, the email routing will look like Figure3. This is bit tricky as we know that *[sending outbound e-mail to external domains directly from an e-mail server hosted in Azure compute services is not supported](https://blogs.msdn.microsoft.com/mast/2017/11/15/enhanced-azure-security-for-sending-emails-november-2017-update/).* 
Microsoft recommends that Azure customers use authenticated SMTP relay services such as [Exchange Online Protection](https://products.office.com/en-us/exchange/exchange-email-security-spam-protection) to send e-mail from Azure VMs or from Azure App Services.

In case the customer has emails hosted on Office 365 and Azure is being used to host the DLP VM's then you will need to configure email routing in such manner that all "Outgoing" emails from Office 365 should be forwarded to DLP on Azure and post DLP has processed the messages, they should be routed back to Office 365. Now if not configured properly, this can cause:

1. Email Loop between Office 365 and DLP
2. Excess outgoing traffic from Azure DLP to Office 365 which may have [cost implications](https://azure.microsoft.com/en-in/pricing/details/bandwidth/).

![](/images/Figure%203.jpg)

To avoid the 2 issues mentioned above, you will need conditional email routing which means that you need to configure a Connector (Figure4) pointing to Public IP of VM running DLP solution and configure a Transport Rule (Figure5)  invoking the connector and allows EOP to route emails outside if mails are coming from DLP server.
 
![](/images/Figure%204.jpg)
		 

![](/images/Figure%205.jpg)


With these configurations in place, only Outgoing emails will get routed to DLP and back to Office 365.

As you see above, configuring 3rd Party DLP solutions with Office 365 Exchange Online is remarkably simple but requires some thoughtful planning and execution. 
