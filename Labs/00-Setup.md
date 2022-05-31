# Environment Setup

- [Part 0 - Environment Setup](00-Setup.md) ( **📍 You are here** )
- [Part 1 - Create a new Teams tab](01-Create_Teams_tab.md)
- [Part 2 - Add Single Sign On feature in your tab](/Labs/02-Create_SSO_Feature.md)
- [Part 3 - Add Microsoft Graph Toolkit TeamsFX Provider and build consent permissions feature](/Labs/03-Initialize_MGT_and_consent_permissions.md)
- [Part 4 - Design your One Productivity Hub using by Microsoft Graph Toolkit components](04-Design_your_tab_using_MGT_components.md)
- [Part 5 - Test One Productivity Hub app on Microsoft Teams](05-Test_your_tab.md)


## 1 - Prepare your Office 365 tenant
---
**⚡ IMPORTANT! ⚡ :** Please sign up for a free [Microsoft 365 Developer Program](https://cda.ms/1Jp) subscription.

---
If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):

* Business Essentials
* Business Premium
* Enterprise E1, E3, and E5
* Developer
* Education, Education Plus, and Education E5

Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

#### Just need a development environment?

If you don't currently have an Office 365 account, you can sign up for a [Microsoft 365 Developer Program](https://cda.ms/1Jp) subscription. It's *free* for 90 days and will continually renew as long as you're using it for development activity. If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription. *See* [Set up a Microsoft 365 developer subscription](https://cda.ms/1Jq).

#### Enable Microsoft Teams for your organization 

If Microsoft Teams has not been enabled for your organization, you'll need to do that first. Take a look at our detailed guidance for [enabling Teams for your organization](https://cda.ms/1Jr).

#### Enable custom Teams apps and turn on custom app uploading

Turn on custom app sideloading for your developer tenant as follows:

1. Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential. 

2. Select **Show All** --> **Teams**. 

---
**📌 NOTE 📌 :** It can take up to 24 hours for the "Teams" option to appear. During interim, you can [Upload your custom app to a Teams environment](https://cda.ms/1Js) for testing and validation.

---

3. Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**  

4. Toggle **upload custom apps** to the **on** position.

That's it! Your test tenant will now allow custom app sideloading.

---
**📌 NOTE 📌 :** It can take up to 24 hours before sideloading is enabled. During interim, you can use **upload for \<your tenant>** to test your app.

---

For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://cda.ms/1Jt) and [Manage app setup policies in Microsoft Teams](https://cda.ms/1Jv).


## 2 - Install Visual Studio Code
The latest Visual Studio Code version is available here: https://code.visualstudio.com/

## 3 - Install Node.js 
Visit https://nodejs.org/ to install Node.js Long Term Support version.

## 4 - Download Microsoft Teams Toolkit 
Microsoft Teams Toolkit extension for Visual Studio Code is available in [Visual Studio Marketplace](
https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).

## References

- [Prepare your Office 365 tenant](https://cda.ms/1J5) 
- Install [Visual Studio Code](https://code.visualstudio.com/)
- Install [Node.js Long Term Support](https://nodejs.org/)
- Download [Microsoft Teams Toolkit extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

## Next Step
> ▶️ **[Part 1 - Create a new Teams tab](01-Create_Teams_tab.md)**
