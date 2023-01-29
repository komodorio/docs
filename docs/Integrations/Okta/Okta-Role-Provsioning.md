# Okta Role Provsionining 

## Setup
To facilitate the assignment of Komodor roles via Okta we first need to configure a few things on the organization Okta account.

### Configure a custom attribute
- Navigate to the Profile Editor section under Directory   
<img src="./profile-editor-2.png" width="200">  

- Select the Komodor User profile  
<img src="./profile-editor-komodor.png" width="800">

- Select the + Add Attribute button
<img src="./add-attribute-komodor.png" width="800">

- Fill in the form as specified in the image below and save the changes
<img src="./add-attribute-komodor-profile.png" width="600">

- To complete the process, go to the Applications view  
<img src="./applications.png" width="200">

- Select the Komodor / Komodorio app
<img src="./komodor-app.png" width="700">

- Navigate to the Sign On tab
<img src="./komodor-app-config.png" width="700">

- Under the Settings section, click the Edit button, under the SAML 2.0 section open the Attributes (Optional) section
<img src="./komodor-app-saml-edit.png" width="600">

- Add the following attribute and save the changes
<img src="./komodor-app-saml-settings.png" width="600">

- Everything is now set to assign Komodor roles through Okta

## Adding Roles to a User
- Navigate to the People section  
<img src="./people.png" width="200">

- Select the user you'd like to assign roles to
<img src="./people-select-user.png" width="700">

- In case the Komodor / Komodorio application is not yet assigned to the user: 
    - Click Assign Applications
    <img src="./people-assign-applications.png" width="700">

    - Assign the Komodor / Komodorio application to the user
    <img src="./people-assign-komodor.png" width="600">

    - Add the relevant roles you'd like to assign to the user and save the changes
    <img src="./people-assign-komodor-roles.png" width="550">

- If the Komodor / Komodorio application is already assigned to the user:
    - Edit the Komodor / Komodorio application assignment 
    <img src="./people-edit-komodor.png" width="800">

    - Make the wanted changes and click Save
    <img src="./people-edit-assignment.png" width="550">

## Adding Roles to a Group
- Navigate to the groups section  
<img src="./groups-nav.png" width="200">

- Select the group that you'd like to assign the Komodor app to
<img src="./groups.png" width="800">

- Navigate to the Applications tab
<img src="./groups-assign-applications.png" width="600">

- Click the Assign applications button and Assign the Komodor / Komodorio app
<img src="./groups-assign-app.png" width="600">

- Specify the Roles you'd wish to assign the group with and Save the assignment
<img src="./groups-assign-roles.png" width="600">

### Edit Role Assignent on an existing group
- Go the the relevant group Applications tab and edit the Komodor / Komodorio application assignment  
<img src="./groups-edit-app.png" width="600">

- Modify the assigned role ids and save the changes
<img src="./group-edit-roles.png" width="600">

### Adding Members to a Group
- Navigate to the groups section  
<img src="./groups-nav.png" width="200">

- Click the Assign people button  
<img src="./assign-people.png" width="600">

- Click the + button for each user you'd like to add to the group. Click Done at the end   
<img src="./assign-person.png" width="600">

- Navigate to the Applications section  
<img src="./applications.png" width="200">

- Select the Komodor application and navigate to the Assignments tab  
<img src="./application-assignment.png" width="600">

**Please note:** The Type of the assignment defines whether the Individual or Group roles will take over. 

- To convert the assignment type from Individual to Group, click Convert assignments button   
<img src="./assignment-conversion-button.png" width="600">

- Select the users for whom you'd like to convert the assignment, and click Convert selected (alternatively you can click the Convert all assignments button) 
<img src="./assignment-conversion.png" width="600">

- Going back to the previous screen, you can confirm that the assignment type has changed  
<img src="./assignment-conversion-successful.png" width="600">
