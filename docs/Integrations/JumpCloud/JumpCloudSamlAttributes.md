# Configure SAML Attributes for JumpCloud SSO
- This tutorial is based on [this article][1] from JumpCloud.
- After configuring youre JumpCloud SAML connection to Komodor,
  you can assign RBAC roles to users based on your account's Komodor roles.

## Add Komodor Roles to a user from the JumpCloud Admin Portal:
- Login to the Admin Portal: https://console.jumpcloud.com/.
- Go to **User Management > Users**.
- Click the green + symbol at the top-left to create a new user,
  or select an existing user for the User Details Panel. click **details** on the right-hand column of an existing user.
- Go to **Custom Attributes**.
- Click **Add New Custom Attribute**.
- For **Attribute Name**, enter `komodorRoles`
- For **Attribute Value**, enter a comma-separated list of roleIds.
  - For example: `role-id-1,role-id-2`
  - No spaces and quotes are allowed.
  - You can find the roleIds in the Komodor UI by going to Settings > Roles.
- Click **Save**.

### Groups
- You can also assign roles to groups.
- Go to **User Management > User Groups**.
- Choose a group -> Details -> Custom Attributes -> Add New Custom Attribute.
- For **Attribute Name**, enter `komodorRoles`
- For **Attribute Value**, do the same as for users
- Click **Save**.
- Now, all users in this group will have the roles you specified.
- If a user in this group has a different set of roles, the user's roles will override the group's roles.

[1]: https://support.jumpcloud.com/support/s/article/custom-user-attributes-2019-08-21-10-36-47
