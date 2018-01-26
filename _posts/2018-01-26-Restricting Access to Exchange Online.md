---
layout: post
#title: Restrict Access to Office365

---
In my capacity as Technical Specialist for Productivity solutions , I meet many customers who want to move their Productivity workloads to cloud but at the same time are concerned about data security and sovereignty. These security concerns lead to requirements around restricted access. Often the underlying need behind such requirements is to mitigate risk of data leakage by ensuring only authorized clients, applications that do not cache data, or devices that can be disabled remotely can get access to resources.

Ideally cloud is meant for anytime, anywhere access so it provides maximum usability and increases productivity but as we know, with this freedom to access data anytime, anywhere comes responsibility of securing the access and data itself and this is a tough balancing act. 

<p align="center"><b>Security, Usability, & Data Sensitivity</b></p>

![](/images/High_Security_Low_Usabality.jpg)![](/images/Balanced_Usability_&_Security.jpg)![](/images/High_Usability_Low_Security.jpg)

Although Default configurations of Office 365 provide secure communication channel but additional configurations are required from data leakage perspective as:
- An authenticated user has access on Office 365 resources he/she has authorization on.
- Office 365 can be accessed anytime and from anywhere i.e. Corpnet or Internet. 
- Office 365 can be accessed anytime from any device(Windows/Mac/Linux based PC's, Windows/iOS/Android based tablet's and Smartphone's).

There are various options available to plug these gaps but approach would depend on the Security governance requirements of organization. Following are few points which can help in taking decision on what kind of restrictions should be applied on access:

1. Access level: What level of access user should have on data i.e. allow/block download, cut, copy, paste operations etc.? 
2. Location: Where is the user located inside/outside the company network?
3. Device status: Is the device trusted/managed?
4. Application Client: Which client is used for accessing application rich client, mobile app or browser?

While restrictions that customers generally ask for are on different workloads including Email, SharePoint, OneDrive etc. but in this article, I will concentrate on restrictions for email access and will cover OneDrive and SharePoint in subsequent articles.

We have solutions for applying restrictions on access of Office 365 content which range from native application level restrictions to ADFS claim rules to applying restrictions using EMS suite. My approach is to suggest the best fit solution post understanding customer requirement.


***Native restrictions***: In addition to allowing or denying access based on specific protocols, IP address, authentication type, user property values, application etc. you can disable downloading of attachments using OWA and ActiveSync. In case of OWA, users will be able to see supported attachment in browser in “Read Only” mode but in case of ActiveSync clients, users will not be able to even open the documents itself. 
This is best suited if requirements around security are simple and customer just wants to restrict access Exchange Online.

***Active Directory Federation Service***: ADFS is generally used by Office 365 customers for Single Sign-on but it can be used to create Access Control Policies that will permit or deny users access based on an incoming claim from specific network, from specific groups, from devices with specific trust levels, with specific claims in the request, And require multi-factor authentication. 
Additionally ADFS can be used for "[Password Change Portal](https://blogs.msdn.microsoft.com/samueld/2015/05/13/adfs-2012-r2-now-supports-password-change-not-reset-across-all-devices/)" for remote users. So all in all ADFS provides more control as compared to the Native controls and can be used in conjunction with the native capabilities to provide control over data access. I recommend using ADFS for access control when requirements are around restricting access for multiple applications in Office 365 and customer needs SSO as well.

***Enterprise Mobility Suite***: EMS is the most flexible of these 3 solutions. It allow access to email content and attachment but restrict Cut, Copy, Paste of email content and attachments, downloading the attachment on device, Saving attachment on 3rd party cloud storage, forwarding the attachment using 3rd party messaging applications, Blocks access from untrusted devices or provides restricted accessing and can enforce MFA in case mails are being accessed from External Networks and block access based on sign-in risk etc. It can place restrictions even on application level for e.g. OWA is blocked but Yammer or SharePoint Online is allowed while all three use browser access. I recommend using EMS when requirements are complex and customer need granular control on the access. 

I have collated various options in following interactive sheet which lets you select solution and check its capabilities or select feature and see which solution can provide it.

<iframe width="1100" height="800" frameborder="0" scrolling="no" src="https://onedrive.live.com/embed?resid=8C8BAC0A56AAF953%21101352&authkey=%21ADO5Mn2wi54kkMs&em=2&ActiveCell='Exchange%20Online'!A2&wdHideGridlines=True&wdHideHeaders=True&wdDownloadButton=True&wdInConfigurator=True"></iframe>

As mentioned earlier, I will be posting another article on restricting access to OneDrive and will update the same Excel sheet.
