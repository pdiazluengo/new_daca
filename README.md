1. Resource Group
Resource Group Name: cms

3. SQL Database
DB name: cms
Server: cms1234.database.windows.net
DB region: us-east
Admin login: cmsadmin
Admin password: CMS4dmin
Resource group: cms
DB workload env: Development
DB compute + storage: DTU - Basic
Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes".
Set everything else to default
Run SQL queries in sql_scripts/ directory after completion, starting from the users table. Don't forget to take screenshots.

5. Storage Account
Resource group: cms
Storage account name: images11 (needs to be unique)
Advanced - Allow enabling anonymous access on individual containers: Enable
Advanced - Access tier: Cool
Network access: Enable public access from all networks (the default)
Create container named "images". Set its access level to Container.
From Security + networking > Access keys:
Blob Storage key: s4oh+l0lJfe+oTMpA16rcp89oS6yP/US9bUpjipea+sEsHW1xz+AU4NerX16dq9CWZKlsm1IniHr+AStIgwqig==

6. Microsoft Entra ID
4.1. App Registration
Name: cmsEntraID
Who can use? "Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)"
4.2. Secret Creation
Secret description: test
Secret Key: fc24e8ab-4aee-4484-a094-5914ed1aea45
Client Secret: SjC8Q~dj4xl2zBrPVvkOpcR.QUrXUz4KS2LxEc8T
Application (client) ID: a17e804c-5bce-43b2-9489-ee8be0b2bca2

8. Application
Pick either of the following two options for setting up your application. Once you have set up the application successfully, you may begin to work on the OAuth2 login feature.
5.2. OPTION 2: Web App (easier)
Name: udacitycms123.azurewebsites.net
Runtime stack: Python 3.10
Pricing Plan: Free F1
If you are getting a "Validation failed for a resource" error, pick a different region.
After creation:

Settings -> Environment variables - Add the following variables (sample values are included, replace them with your values):
BLOB_ACCOUNT: images11
BLOB_CONTAINER: images
BLOB_STORAGE_KEY: s4oh+l0lJfe+oTMpA16rcp89oS6yP/US9bUpjipea+sEsHW1xz+AU4NerX16dq9CWZKlsm1IniHr+AStIgwqig==
SQL_SERVER: cms1234.database.windows.net
SQL_DATABASE: cms
SQL_USER_NAME: cmsadmin
SQL_PASSWORD: CMS4dmin
CLIENT_SECRET: SjC8Q~dj4xl2zBrPVvkOpcR.QUrXUz4KS2LxEc8T
SECRET_KEY: fc24e8ab-4aee-4484-a094-5914ed1aea45
CLIENT_ID: a17e804c-5bce-43b2-9489-ee8be0b2bca2
Deployment Center
Source: GitHub
Pick the repo that contains the starter files.

6. Setting up OAuth2
At this point, your application should already be running. You should already be able to log in with username admin and password pass and you can create new posts or update existing ones.

The next part is getting the OAuth2 login to work.

Go to Microsoft Entra ID > App Registrations, click on the App Registration created earlier, and then pick Authentication from the left sidebar.

6.1. Microsoft Entra ID - Authentication - Add a Platform - Web
Redirect URIs: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/getAToken
logout URL: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/login
