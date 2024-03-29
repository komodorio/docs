# Azure AD Role Provisioning

To assign Komodor roles to Azure AD users we'll be utilizing the App Roles capability.

For each Komodor role we'd wish to assign to users in Azure AD, we'll have to create a corresponding Azure AD App Role.

> Prerequisites:
>
> - Integrate Azure AD with Komodor using SAML. [Link to guide.](./Azure-SAML-Integration.md)

## Creating App Roles

To create app roles, follow the steps below:

Go to "App registrations":
<img src="./img/app-registrations.png">

Pick "All applications", and then click the Komodor app:
<img src="./img/pick-app-registration.png">

Next, navigate to "App roles":
<img src="./img/app-roles.png">

Click, "Create app role":
<img src="./img/create-app-role.png">

Fill in the form as below.
<img src="./img/role-1.png">

Note that the value must be the role ID as it appears in Komodor:
<img src="./img/komodor-roles.png">

Finally, click "Apply". Repeat this for all the roles you wish to add, and you should see them added in the portal, like so:
<img src="./img/created-app-roles.png">

## Assigning Roles to a User

Now that we have created the Komodor app roles, we move on to assign them to a user.

Go back to "Enterprise applications" (explained above), and then pick the Komodor app:
<img src="./img/komodor-app.png">

Once there, we click on "Assign users and groups":
<img src="./img/assign-users-and-groups.png">

Click "Add user/group":
<img src="./img/add-user-group.png">

This will allow you to assign a role to a user (or a group, covered below). Simply pick a user:
<img src="./img/add-assignment.png">

Next, select a role:
<img src="./img/select-role.png">

Finally, click "Assign".

## Assigning Roles to a Group

Just like we assigned a role to a user, we can assign a role to a group. To that end, we click "Add user/group", and simply pick a group rather than a user this time. We then select a role, and click "Assign".

Having done that, we should see the group with the role assigned to it (we can also see the user who was assigned a role above):
<img src="./img/assigned-roles.png">

Note that members of a group automatically get assigned the roles that are assigned to the group. It means that since "Alon Glatter" is a member of "Group-1", he will be assigned both "Role-2" and "Role-1" (which was assigned to him via "Group-1").

## Sending Role Assignments Over SAML Response

We go to the "Single sign-on" page where we configured the SAML connection to Komodor ([here](./Azure-SAML-Integration.md)), and click "Edit" on "Attributes & Claims":
<img src="./img/attributes-and-claims.png">

We click on "Add new claim":
<img src="./img/add-new-claim.png">

We then fill in the form like below, and then finally click "Save":
<img src="./img/manage-claim.png">

That's it! Next time the user logs in to Komodor via Azure AD, they will have been assigned the roles in Komodor which are respective to the roles they have been assigned in Azure.
