# Main Azure AD components:

| Concept | Description |
| --- | --- |
| Identity | An object that can be authenticated, user with pass and username or application or server with secret key or certificate. Azure AD is the underlying product providing the identity service.|
| Account | An identity with data associated to it. Account -> Identity |
| Azure AD account | An Azure AD account is an identity that's created through Azure AD or another Microsoft cloud service, such as Microsoft 365. Identities are stored in Azure AD and are accessible to your organization's cloud service subscriptions. The Azure AD account is also called a work or school account.|
| Azure tenant (directory) | a single dedicated and trusted instance of azure AD. you can create multiple instances. |
| Azure subscription | Used to pay for azure cloud services, each tenant is linked to a single tenant, you can have multiple subscriptions. |

# Azure AD vs AD DS
AD DS is the basic on premise Windows server Active directory, the main reason why Azure and Microsoft prefer you switch from AD DS to Azure AD is that AD DS is mainly a directory service while Azure AD is a full identity service and so it is more secure and robust by nature.
The other reason is that the communication protocols used by Azure AD is HTTP and HTTPS based and so it dosen't use the Kerberos authentication protocol, it uses other protocols such as SAML, WS-Federation etc... Azure AD also offers easy integration with federation services that are mostly third party like Facebook.
It also has a Flat structure, that a tree like a LDAP server (OUs and GPOs)
And the most important thing is that it is a managed service, so you are rid of all back end maintenance, deployment and configuration.
# Azure AD editions:
Azure Active Directory comes in four editions: Free, Microsoft 365 Apps, Premium P1, and Premium P2. each having their benefits, it is necessary to consider the company's needs when choosing an edition to put in place [More details on benefits](https://azure.microsoft.com/pricing/details/active-directory).
# Azure AD join:
The join feature basically allows for benefits such as SSO, Entreprise state roaming (synchronise user configuration and settings to joined devices), Access to Microsoft Store for Business (Pre-selected inventory of application), Windows Hello(Accessing work resources securely from joined devices),
Restriction of access (Restrict access to organization apps to only from joined devices), Access to on-premises resources even remotely.
 # Things to consider:
Things to consider when using joined devices

Your organization is interested in using joined devices in their management strategy. As you plan for how to implement the feature, review these configuration points:

- Consider connection options. Connect your device to Azure AD in one of two ways:

- Register your device to Azure AD so you can manage the device identity. Azure AD device registration provides the device with an identity that's used to authenticate the device when a user signs into Azure AD. You can use the identity to enable or disable the device.

- Join your device, which is an extension of registering a device. Joining provides the benefits of registering, and also changes the local state of the device. Changing the local state enables your users to sign into a device by using an organizational work or school account instead of a personal account.

- Consider combining registration with other solutions. Combine registration with a mobile device management (MDM) solution like Microsoft Intune, to provide other device attributes in Azure AD. You can create conditional access rules that enforce access from devices to meet organization standards for security and compliance.

- Consider other implementation scenarios. Although AD Join is intended for organizations that have an on-premises Windows Server Active Directory infrastructure, it can be used for other scenarios like branch offices.
# Azure AD SSPR:
The self-service password reset feature is only managed by a global admin account that always reset his own password, sspr also uses security groups to limit the users who have SSPR privileges, all accounts need a valid licence to use sspr.
When implementing as SSPR you need to consider :
 1. Who can reset their passwords, you have 3 options when enabling the feature and they are None, Selected and All. Selected means the group you have selected.
2. The authentication methods, you are required to include minimum one method, and you have many options such as email notification, text message, security code to phone and security questions.
3. You should combine the methods for stronger security.

