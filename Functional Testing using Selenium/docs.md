
### Observations and Notes
1. Login not strictly enforced: In this Docker deployment, it is possible to perform actions like creating a project or enumeration without logging in. This is unusual behavior and would be considered a functional/security issue in a real deployment.
2. Selenium automation successfully navigates through all administrative and functional pages.
3. Status messages in the script confirm actions were completed.

### Functional Issues Identified
While performing Selenium testing, the following functional issues were noted:
1. Actions allowed without login: Creating projects or enumerations works without authentication.
2. Navigation delays: Some pages like Workflow and Custom Fields load slowly due to container setup.
3. Tracker issue: While creating a new tracker, the drop down does not show any default status to choose from. As a result, we cannot make a tracker and assign it to a project. The following error line appears on the screen: Default status cannot be blank. As a result, we cannot effectively add ISSUES.

### Test Cases 
  # Redmine Functional / UI Test Cases

| TC ID | Name | Description | Expected Results | Actual Results | Status |
|-------|------|-------------|-----------------|----------------|--------|
| TC01 | Login functionality | Verify that a user can log in with valid credentials | User is logged in and redirected to the dashboard | User logged in successfully | Pass |
| TC02 | Login functionality | Verify that a user cannot log in with invalid credentials | An error message is displayed stating the invalid entry used | Error message displayed | Pass |
| TC03 | Project Creation | Verify that a new project can be created | New project is created and listed | New project created successfully | Pass |
| TC04 | Projects Without Login | Verify that creating a project without login is blocked | User is prompted to login | Project creation is possible without login | Fail |
| TC05 | Users Page Access | Verify that Users page can be accessed | Users page is displayed | Users page opened | Pass |
| TC06 | Groups Creation | Verify that a new group can be created | Group is created and listed | Group created successfully | Pass |
| TC07 | Roles & Permissions | Verify access to Roles and Permissions & Permissions Report | Roles and permissions are displayed; report opens | Report opened successfully | Pass |
| TC08 | Enumerations Creation | Verify that a new enumeration can be added | Enumeration is created and listed | Enumeration created successfully | Pass |
| TC09 | Enumerations without Name | Verify validation when creating an empty enumeration | Error message prevents creation | Error message is displayed | Pass |
| TC10 | Tracker Creation | Verify tracker creation functionality | Tracker is created and can be assigned to a project | Default status cannot be blank error appears; cannot create tracker | Fail |
