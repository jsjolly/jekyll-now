---
layout: post
#title: Restrict Access to Office365

---
In my capacity as Modern Workplace TSP, I meet many customers who want to move their Productivity workloads to cloud but at the same time are concerned about data security and sovereignty. These security concerns lead to requirements around restricted access. Often the underlying need behind such requirements is to mitigate risk of data leakage by ensuring only authorized clients, applications that do not cache data, or devices that can be disabled remotely can get access to resources.

Ideally cloud is meant for anytime, anywhere access so it provides maximum usability and increases productivity but as we know, with this freedom to access data anytime, anywhere comes responsibility of securing the access and data itself and this is a tough balancing act. 

<p align="center"><b>Security, Usability, & Data Sensitivity</b></p>
<p align="center"><img src="/images/Balanced_Usability_&_Security.jpg"></p>
![](/images/High_Security_Low_Usabality.jpg)![](/images/High_Usability_Low_Security.jpg)


Although Default configurations of Microsoft's cloud-based productivity solution, Office 365 provide secure communication channel but leave gaps from data leakage perspective as:
- An authenticated user has access on Office 365 resources he/she has authorization on.
- Office 365 can be accessed anytime and from anywhere i.e. Corpnet or Internet. 
- Office 365 can be accessed anytime from any device(Windows/Mac/Linux based PC's, Windows/iOS/Android based tablet's and Smartphone's).

There are various options available to plug these gaps but approach should depend on the Security governance requirements of organization. Following are few points which can help in taking decision on what kind of restrictions should be applied:

1. Access level: What level of access user should have on data i.e. allow/block download, cut, copy, paste operations etc.? 
2. Location: Where is the user located inside/outside the company network?
3. Device status: Is the device trusted/managed?
4. Application Client: Which client is used for accessing application rich client, mobile app or browser?

While restrictions that customers generally ask for are on different workloads including Email, SharePoint, OneDrive etc. but in this article, I will concentrate on restrictions for email access and will cover OneDrive and SharePoint in subsequent articles.

We have solutions for applying restrictions on access of Office 365 content which range from native application level restrictions to ADFS claim rules to applying restrictions using EMS suite. Depending on what customer requirement is, we can suggest the best fit solution.


***Native restrictions***: In addition to allowing or denying access to specific protocols such as OWA, ActiveSync, POP3/IMAP, MAPI etc. we can disable downloading of attachments using OWA and ActiveSync. In case of OWA, users will be able to see supported attachment in browser in “Read Only” mode but in case of ActiveSync clients, users will not be able to even open the documents itself. 
This is best suited if requirements around security are simple and customer just wants to restrict access on attachments outside corpnet.

***Active Directory Federation Service***: ADFS is generally used by Office 365 customers for Single Sign-on but it can be used to create Access Control Policies that will permit or deny users access based on an incoming claim from specific network, from specific groups, from devices with specific trust levels, with specific claims in the request, And require multi-factor authentication. 
Additionally ADFS can be used for "Password Reset Portal" for remote users. So all in all ADFS provides more control as compared to the Native controls and can be used in conjunction with the native capabilities to provide control over data access. We recommend using ADFS for access control when requirements are around restricting a type of access for e.g. browser access or thick client access etc.

***Enterprise Mobility Suite***: EMS is the most flexible of these 3 solutions. It allow access to email content and attachment but restrict Cut, Copy, Paste of email content and attachments, downloading the attachment on device, Saving attachment on 3rd party cloud storage, forwarding the attachment using 3rd party messaging applications, Blocks access from untrusted devices or provides restricted accessing and can enforce MFA in case mails are being accessed from External Networks and block access based on sign-in risk etc. It can place restrictions even on application level for e.g. OWA is blocked but Yammer or SharePoint Online is allowed while all three use browser access. We recommend using EMS when requirements are complex and customer need granular control on the access. 

<iframe width="900" height="650" frameborder="0" scrolling="no" src="https://onedrive.live.com/embed?resid=8C8BAC0A56AAF953%21101352&authkey=%21ADO5Mn2wi54kkMs&em=2&ActiveCell='Exchange%20Online'!A2&wdHideGridlines=True&wdHideHeaders=True&wdDownloadButton=True&wdInConfigurator=True"></iframe>
