# User accounts:
## Types of user accounts:
Azure Active Directory (Azure AD) supports three types of user accounts.

| User account | Description |
| --- | --- |
|Cloud identity| only defined in azure AD, icludes admins and users managed as part of org, can be for users defined in your Azure AD org or an external one, When deleted from primary directory, the account is deleted.|
| Directory synchronized identity | User accounts that are defined in an on-premises AD, they are brought to Azure using Azure connect, The source for these accounts are Windows Server Active Directory. |
| Guest user | Defined outside of Azure, like from other cloud providers. Invited users and are useful for when external entities need access to your Azure resources |

### What to consider when choosing the type:
- Consider where users are defined, meaning within your Azure AD org or external Azure AD instances or external to your org.
- Consider outside contributors by using the guest user type, you can delete the account when their usage is over.
- Consider a combination of user accounts to meet your business requirements.
## Cloud identity accounts:
- Main type used, You can create it using the Portal, 365 Admin center, Intune admin console or AzureCLI.
- The admin can create or invite a user. necessary and unchangable information include the display name and user account name.
- Information and settings of a user account are stored in the user account profile.
- Global admin or User admin can preset info for new users.
- Non-admin can change some of their profile data.
### Considerations:
When creating a new user account we need to consider:
- Consider allowing users to set informations for their accounts.
- Consider restore options for deleted accounts, max 30 days to be restored.
- Consider gathering account data for audit and analytics.
## Bulk operations:
Includes bulk creation and deletion of accounts.
### Creation:
- only global admin or user admin can do it.
- mainly use csv files for user accounts data.
- templates of operations can be downloaded through the portal.
- Lists of users can be downloaded.
#### Considerations:
Think about what user account conventions and processes might be required by your organization.
- Naming conventions, for user account names, display names and aliases for consistency.
- Using initial passwords.
- Strategize to minimize errors: Download bulk operation results file to view errors. (mainly already created or duplicated) best practice is to upload smaller lists and troubleshoot.
# Group accounts:
## Types : 
- Security groups:
	Manage access to shared resources.
- Microsoft 365 groups:
	Shared mailbox, calendar, files and SharePoint site.
## Best practices:
- Use security groups to add permissions to groups of users at the same time instead of adding to each one individuallly. They can be implemented only by the Azure AD admin.
- Microsoft 365 groups enable group access for guest users, and they can be used by both admins and normal users.
## Ways to add users to groups:
| Access rights |	Description |
| --- | --- |
Assigned 	| Add specific users as members of a group, where each user can have unique permissions.
Dynamic user 	| Use dynamic membership rules to automatically add and remove group members. When member attributes change, Azure reviews the dynamic group rules for the directory. If the member attributes meet the rule requirements, the member is added to the group. If the member attributes no longer meet the rule requirements, the member is removed.
Dynamic device 	| (Security groups only) Apply dynamic group rules to automatically add and remove devices in security groups. When device attributes change, Azure reviews the dynamic group rules for the directory. If the device attributes meet the rule requirements, the device is added to the security group. If the device attributes no longer meet the rule requirements, the device is removed.

# Administrative units:
Administrative units is basically seperating the administrative jobs and permissions accross the admins according to their respective responsabilities and so building a more robust, clear and secure infrastructure. Basically restrict administrative scope by using administrative units.
## Considerations:
- Management tools: Portal, scripts ...
- Role requirements: plan your strategy. Only global admin or privileged role admins can manages AUs.
- Scope of AUs.