
**How to configure Cloud Sync in Active Directory**

**Source1: Settings on the server side** - [here](https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-install)

**Source2: Settings on Microsoft Entra ID portal** - [here](https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-configure)

Before proceeding with installation. To ensure that your users are sync with the correct domain to M365 portal.
If your exsting AD domain name is different from your Microsoft 365 domain, you may need to perform the following steps to add the M365 UPN as a trust domain.
Step: Login to DC > Server Manager > Tools > AD Domains and trusts
Right-click on the AD Domains and Trusts on the left pane > Select Properties > Add the exact M365 domain here and OK

![image](https://github.com/user-attachments/assets/89a3d328-1c14-49f8-b775-609bdba3bcff)

   
**Step 1**: Download and install "Provisioning Agent" [here](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/~/GetStarted?Microsoft_AAD_IAM_legacyAADRedirect=true)

**Step 2**: Configure the Provisioning agent on AD.
![image](https://github.com/user-attachments/assets/e30d5659-851b-4135-8e65-c333255a3806)

1. **Select Extension**: Select HR-driven provisioning and Next
   ![image](https://github.com/user-attachments/assets/1f20d1a7-3fdd-4130-93e8-af6b4283bb29)

2.**Connect Microsoft Entra ID** Authenticate to your Entra with admin creds
  
3.**Configure Service Account**: Create a group managed service account(gMSA) to manage your synchronization from Active directory.

  ![image](https://github.com/user-attachments/assets/87858145-28f6-4d76-959d-5d031eeda020)

4. **Connect Active Directory**: Verify the configured domain is correct and click Next.
   ![image](https://github.com/user-attachments/assets/f425e12f-c830-402a-b7d8-6f03bd18d9ab)
   
6. **Confirm to complete installation**
![image](https://github.com/user-attachments/assets/2b4e5972-ac4a-404e-99e4-13968abc2316)

Exit after the installation

**Step 2** Login to Entra ID portal > Identity > Show more > Hybrid management > Microsoft Entra connect > Cloud Sync.
On the **Configurations** tab, select **New configuration** > **AD to Microsoft Entra ID sync**
Verify your domain name is listed under active agents > Check box to enable password hash sync and create.
On the next page is where you configure, test and deploy your sync setup using the steps below.

1. **Add scoping filters (optional)** : I'll be syncing a users in a test OU I have created in the AD. Locate the OU and right-click to open its properties > Attribute Editors > Copy the Distinguished name of OU. Select "Selected organizational units" and paste the distinguished name, then save it.

   ![image](https://github.com/user-attachments/assets/625ac91a-d9d1-48c4-b902-0ec3dcce50eb)
   ![image](https://github.com/user-attachments/assets/6f2b5c2f-6b0a-4cd2-be3c-dc6bf764e1e0)

2. **Map attributes**: Configure the if necessary.

3. **Test (recommended)** Select a user from your on-premises environment to provision. Back to the DC, find a test user and copy their distinguished name and paste the space to provision.
   ![image](https://github.com/user-attachments/assets/5cb59bcf-b286-4a49-b488-9b85d700ffc6)

**Note** : You may run into an MFA error similar to below.
![image](https://github.com/user-attachments/assets/9c4d0886-ee67-4b00-82ed-7d5c46ac6c43)
**Fix**: This usually happens if there is conditional access policy that enforced MFA on all users, if that is the case you'll need to exclude this syncronization account from that policy. The account is **On-Premises Directory Synchronization Service Account**. Try to provision the user again.

4. **Set properties (optional)**: Modify as needed, provide notification email.

5.**Enable your configuration (required)**: Enabling will sync users and groups that are in scope.
**Note**: The Object scope filters may still reflect as All users even after OU was selected in the scope. This may be a bug from Microsoft and you can ignore be rest assured the sync is only going to affect the selected OU.
![image](https://github.com/user-attachments/assets/e42fee56-173c-41a7-a8e1-3fda704a0e8c)




