# Pet Management Application User Guide

The Pet Management Application is a B2C (Business-to-Consumer) application that allows users to easily register and manage their pets. Users can enter vital information such as their pets' basic information and vaccination records into the app. They can then set up email alerts for their pets' upcoming vaccination dates. 

There are two ways that you can run this sample application

- [Using Cloud Deployment](#using-cloud-deployment)
- [Run Locally](#run-locally)

# Using Cloud Deployment

This guide will show you how to use [Asgardeo](https://wso2.com/asgardeo/), WSO2's SaaS Customer IAM (CIAM) solution to secure user authentication to the web application and add CIAM features to your web application. Also to use [Choreo](https://wso2.com/choreo/) to expose a service endpoint as a REST API and safely consume the API from a web application.
---

&nbsp;<br>
# Step 1: Configure Asgardeo

## Step 1.1: Configure Asgardeo to integrate with your web application

1. Access **Asgardeo** at https://console.asgardeo.io/ and log in. 
2. Click **Applications** in the left navigation menu.
3. You can see the application you have created before.
4. Click the `New Application` and select `Single-Page Application`. Provide the name and Authorized redirect URLs as follows.
&nbsp;<br>
Name: `Pet Management App` &nbsp;<br>
Authorized redirect URLs: https://localhost:3000 (This will be updated with the App hosted URL in a future step)&nbsp;<br>
5. Click the **Protocol** tab.
6. Scroll down to the **Allowed grant types** and tick **Refresh Token** and **Code**.
7. Tick **Public client** on the next section.
8. Use **Web App URL** in the step 3.3 as the **Authorized redirect URLs** and **Allowed origins**.
9. Keep the rest of the default configurations and click **Update**.
10. Go to the **User Attributes** tab.
11. Tick on the **Email** section.
12. Expand the **Profile** section.
13. Add a tick on the Requested Column for the **Full Name** and click **Update**.
14. Then go to the **Sign-In Method** tab.
15. Configure **Google login** as described in https://wso2.com/asgardeo/docs/guides/authentication/social-login/add-google-login/
16. As shown in the below, add **Username & Password** as an **Authentication** step.

![Alt text](readme-resources/sign-in-methods.png?raw=true "Sign In Methods")

## Step 1.2: Enable features in Asgardeo

1. [Branding and theming](https://wso2.com/asgardeo/docs/guides/branding/configure-ui-branding/)
    - On the **Asgardeo Console**, click **Branding** in the left navigation menu.
    - Enable the **Branding** toggle on top.
    - Go to **General** tab and enter the **site title** as `Pet Management App`.
    - You can provide values to **Copyright Text** and **Contact Email**.
    - Go to the **Design** tab and choose layout as **Centered**.
    - Choose the **Light** theme.
    - Go to **Theme preferences > Images** and enter logo url: https://user-images.githubusercontent.com/35829027/230538511-a546d36d-0b4e-4422-ae96-888c512a5984.png
    - Enter **Logo Alt Text** as `Pet Management App Logo`.
    - Enter **Favicon url**: https://user-images.githubusercontent.com/35829027/230538759-d27652d4-1b50-4664-946b-3a69389c42b7.png
    - Go to **Color Pallet** and choose primary color as **#4AD6DB**
    - Keep other options as default
    - Click **Save**.
    
2. [Configure password recovery](https://wso2.com/asgardeo/docs/guides/user-accounts/password-recovery/)
    - On the **Asgardeo Console**, click **Account Recovery** in the left navigation menu.
    - Go to **Password Recovery**.
    - Click **Configure** to open the Password Recovery page.
    - Turn on **Enabled** to enable this configuration.
    
3. [Self registration](https://wso2.com/asgardeo/docs/guides/user-accounts/configure-self-registration)
    - On the **Asgardeo Console**, click **Self Registration** in the left navigation menu.
    - Click **Configure**.
    - **Enable** self registration toggle.
    - Tick **Account verification** and then click the **Update** button.
    
4. [Configure login-attempts security](https://wso2.com/asgardeo/docs/guides/user-accounts/account-security/login-attempts-security/#enable-login-attempts-security)    
    - On the **Asgardeo Console**, click **Account Security** in the left navigation menu.
    - Click **Configure** to open the **Login Attempts** page.
    - Turn on **Enabled** to enable this configuration.
    
&nbsp;<br>
# Step 2: Consume the Pet Management Application
    
1. Use **Web App URL** in **step 3.3** to access the Pet Management web application. 

![Alt text](readme-resources/landing-page.png?raw=true "Landing Page")

2. Click on the **Get Started** button.
3. You will get a **Sign In** prompt.
4. You can create an **account** by giving an email address or use a **Google** account to login into the Pet Management application. After login successfully you will redirect to the home page:

![Alt text](readme-resources/home-page.png?raw=true "Home Page")

5. To add a new pet, Click on the **+** button next to `My Pets` in the home page.
6. Provide a name, breed and date of birth.
7. Then click on the **Save** button.
8. Click on the created card and you can see an **overview** of the pet.
9. Click on the **edit** button to update details of the pet. You will get an Update view for the pet.
10. In there you can edit the name, breed and date of birth of the pet.
11. Furthermore, you can add **vaccination details** for your pet.
    - Go to the Vaccination Details section.
    - Give the vaccination name, last vaccination date and next vaccination date.
    - Click on the + button.
    - You can check the enable alerts checkbox if you wish to receive alerts for the next vaccination date.
    - Click on the **Save** button.
    &nbsp;<br>

12. You can update the **image** of your pet in the update details prompt.
    - Click on the Choose a file button.
    - Select a photo from your local device.
    - Click on the **Update** button.
13. Also you can **enable/disable** alerts from the **settings**.
    - Click on the user menu on the top right corner in the home page.
    - Click **Settings**.
    - Toggle the switch to **enable alerts**.
    - Provide an email address.
    - Click **Save**.

# Step 3: Create and publish a Service

In this step, you will play the role of the API developer. You will create and publish the Service that the web application needs to consume. Before you proceed, sign in to [**Choreo Console**](https://console.choreo.dev/).

## Step 3.1: Create the Service

Let's create your first Service.
1. On the **Home** page, click on the project you created.
2. To add a new component, select **Components** from the left-side menu and click **Create**.
3. Click **Create** in the **Service** card.
4. Enter a unique name and a description for the Service. For example, you can enter the name and the description given below:

    | Field | Value |
    | -------- | -------- |
    | Name | Pet Management Service |
    | Description | Manage your pets |

5. Click **Next**.
6. To allow Choreo to connect to your GitHub account, click **Authorize with GitHub**.
7. If you have not already connected your GitHub repository to Choreo, enter your GitHub credentials, and select the repository you created by forking https://github.com/wso2/samples-is to install the Choreo GitHub App.
8. In the Connect Repository dialog box, enter the following information:

    | Field | Value |
    | -------- | -------- |
    | GitHub Account | Your account |
    | GitHub Repository | samples-is|
    | Branch | main |
    | Build Preset | Click **Ballerina** because you are creating the REST API from a Ballerina project and Choreo needs to run a Ballerina build to build it. |
    | Path | /b2c-apps/pet-care-app/pet-management-service |

9. Click **Create** to initialize a Service with the implementation from your GitHub repository.

The Service opens on a separate page where you can see its overview.

## Step 3.2: Deploy the Service

For the Service to be invokable, you need to deploy it. To deploy the Service, follow the steps given below:
1. Navigate to the **Choreo Console**. Verify that you are logged into the **organization** you used for Asgardeo. Otherwise, select the appropriate **organization** by clicking on the organization menu at the top.
You will be viewing an overview of the Pet Management Service.
2. In the left pane, click **Deploy**, and then click **Configure & Deploy**.
3. In the **Configure & Deploy** pane, you will be asking to enter values for the **Defaultable Configurables**.
    - You can setup a **Mysql database** to store the service's data. This is **optional**, and if you do not specify database values, the service will save the data in memory. 

      <details><summary>If you are setting up <b>Mysql Database</b> click here</summary>
      <p>
      
      - Create a Mysql Database using the following database schema.
      
          ```sql
          CREATE DATABASE IF NOT EXISTS PET_DB;

          CREATE TABLE PET_DB.Pet (
              id VARCHAR(255) PRIMARY KEY,
              name VARCHAR(255) NOT NULL,
              breed VARCHAR(255) NOT NULL,
              dateOfBirth VARCHAR(255) NOT NULL,
              owner VARCHAR(255) NOT NULL
          );

          CREATE TABLE PET_DB.Vaccination (
              id INT AUTO_INCREMENT PRIMARY KEY,
              petId VARCHAR(255) NOT NULL,
              name VARCHAR(255) NOT NULL,
              lastVaccinationDate VARCHAR(255) NOT NULL,
              nextVaccinationDate VARCHAR(255),
              enableAlerts BOOLEAN NOT NULL DEFAULT 0,
              FOREIGN KEY (petId) REFERENCES Pet(id) ON DELETE CASCADE
          );

          CREATE TABLE PET_DB.Thumbnail (
              id INT AUTO_INCREMENT PRIMARY KEY,
              fileName VARCHAR(255) NOT NULL,
              content MEDIUMBLOB NOT NULL,
              petId VARCHAR(255) NOT NULL,
              FOREIGN KEY (petId) REFERENCES Pet(id) ON DELETE CASCADE
          );

          CREATE TABLE PET_DB.Settings (
              owner VARCHAR(255) NOT NULL,
              notifications_enabled BOOLEAN NOT NULL,
              notifications_emailAddress VARCHAR(255),
              PRIMARY KEY (owner)
          );
          ```
        
      - Make sure your database is publicly accessible and that your database service allows Choreo IP addresses. Please refer the guide [Connect with Protected Third Party Applications](https://wso2.com/choreo/docs/reference/connect-with-protected-third-party-applications/#connect-with-protected-third-party-applications) for more information.

      - Configure the following **Defaultable Configurables** after setting up the database.   

        | Field      |  Value |
        | ---------- | -------- |
        | dbHost     | Database Host. eg: mysql–instance1.123456789012.us-east-1.rds.amazonaws.com  |
        | dbUsername | Database username |
        | dbPassword | Database password |
        | dbDatabase | Database name. eg: PET_DB  |
        | dbPort     | Database port. eg: 3306|

      </p>
      </details>

    &nbsp;<br>
    - The Pet Management Service sends email to the users. This is **optional**, and if you specify email configurations here, it will use to send emails to the users. 

      <details><summary>If you are setting up <b>email</b> click here</summary>
      <p>
            
      - In order to send emails to the users, you need to create a client for the SMTP server. Here is a guide for setting up a SMTP client for the **GMail**.
        - You can generate a password for the email username using [https://myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords).
        - Configure the following **Defaultable Configurables** for the email configuration.   

          | Field      |  Value |
          | ---------- | -------- |
          | emailHost     | SMTP Host. eg: smtp.gmail.com  |
          | emailUsername | Email address |
          | emailPassword | Email password (The app password generated in the above.) |
      
      </p>
      </details>

    &nbsp;<br>
4. Click **Next** on the **Defaultable Configurables** to deploy the service.
5. Click **Deploy**.

## Step 3.3: Update runtime settings

If you are not connecting the service to a MySQL database and storing the service's data in memory, then you must follow the steps below to ensure that only one container is running for the service.

1. Navigate to the **DevOps** section in the component and click **Runtime**.
2. Make the Min replicas and Max replicas count to **1** and click **Update**.
3. Click **Redeploy Release** button.

## Step 3.4: Update API settings

1. Navigate to the **Manage** section in the component.
2. Click **Settings**.
3. Under API Settings click **Edit**.
4. Toggle the **Pass Security Context To Backend** to pass the security context details to backend and click **Save**.
5. In the **Apply to Development** pane that opens on the right-hand side of the page, enter a meaningful message. Then click **Apply**.

## Step 3.5: Test the Service

Let's test the Pet Management Service via Choreo's Open API Console by following the steps given below:
1. Navigate to the **Test** section in the component and click **OpenAPI Console**. This will open up the Open API definition of the service.
2. Expand the **POST** method and click **Try it out**.
3. Update the request body as below:
    ``` 
    {
      "breed": "Golden Retriever",
      "dateOfBirth": "03/02/2020",
      "name": "Cooper",
      "vaccinations": [
        {
          "enableAlerts": true,
          "lastVaccinationDate": "03/01/2023",
          "name": "vaccine_1",
          "nextVaccinationDate": "07/17/2023"
        }
      ]
    }
    ```

4. Click **Execute**.
5. Check the Server Response section. On successful invocation, you will receive the **201** HTTP code.
Similarly, you can expand and try out the other methods.

## Step 3.6: Publish the Service

Now that yourService is tested, let's publish it and make it available for applications to consume.

1. Navigate to the **Manage** section of the channel service and click **Lifecycle**.
2. Click **Publish** to publish the Service to the **Developer Portal**. External applications can subscribe to the API via the Developer Portal.
3. To access the Developer Portal, click **Go to DevPortal** in the top right corner.
4. The Pet Management Service will open in the Developer Portal.

&nbsp;<br>
# Step 4: Consume the Service from Developer Portal

## Step 4.1: Enable Asgardeo Key Manager

You can skip this step if you are new to Choreo. If not, follow the below steps to **Enable Asgardeo Key Manager**.

1. Go to the **Choreo Console**, click **Settings**, and then click **API Management**.
2. On the API Management page, click **Enable Asgardeo Key Manager**.

![Alt text](readme-resources/enable-km.png?raw=true "Enable Asgardeo Key Manager")

## Step 4.2: Create an application

An application in the Developer Portal is a logical representation of a physical application such as a mobile app, web app, device, etc.
Let's create the application to consume the Pet Management Service by following the steps given below:
1. Go to the **Developer Portal**.
2. In the top menu of the Developer Portal, click **Applications**.
3. Click **Create**.
4. Enter a name for the application (for example, **Pet Management App**) and click **Create**.

Your Application will open on a separate page.

## Step 4.3: Subscribe to the Service

To consume the Service, the `Pet Management App` application needs to subscribe to it. To subscribe your application to the Service, follow the steps given below:
1. In the left navigation menu, click **Subscriptions**.
2. Click **Add APIs**.
3. Find your Service and click **Add**.

Now your application has subscribed to the `Pet Management Service` Service.

## Step 4.4: Generate Credentials for the Application

To consume the Service, you need to use the application keys. The below steps specify how you can generate keys for the application.
1. In the left navigation menu, click **Production** on **Credentials**.
2. Click **Generate Credentials**.

Now you have generated keys for the application.

&nbsp;<br>

# Step 5: Deploy the Pet Management Web application

## Step 5.1: Enable Web Application Creation feature

You can skip this step if you are new to Choreo. If not, follow the below steps to **Enable Web Application Creation feature**.

1. Navigate to **Choreo Console**.
2. Click on the **User Profile** in the top right corner.
3. Click on the **Feature Preview** in the user menu.
4. Toggle the **Web Application Creation** Switch.

![Alt text](readme-resources/feature-preview.png?raw=true "Feature Preview")

## Step 5.2: Configure the front-end application

In this step, you are going to deploy the pet management front-end application in Choreo.

1. Navigate to **Choreo Console**.
2. Navigate to the **Components** section from the left navigation menu.
3. Click on the **Create** button.
4. Click on the **Create** button in the **Web Application** Card.
5. Enter a unique name and a description for the Web Application. For example you can provide the following sample values.

    | Field | Value |
    | -------- | -------- |
    | Name | Pet Management Web App |
    | Description | Web application for managing your pets. |

6. Click on the **Next** button.
7. To allow Choreo to connect to your **GitHub** account, click **Authorize with GitHub**.
8. In the Connect Repository dialog box, enter the following information:

    | Field | Value |
    | -------- | -------- |
    | GitHub Account | Your account |
    | GitHub Repository | samples-is |
    | Branch | main |
    | Build Preset | Click **React SPA** since the frontend is a React application built with Vite |
    | Build Context Path | /b2c-apps/pet-care-app/pet-management-webapp |
    | Build Command | npm install && npm run build|
    | Build Output |dist|
    | Node Version |18|

10. Click on the **Create** button.
11. The Web Application opens on a separate page where you can see its overview.

## Step 3.3: Configure the front-end application

In this step, you are adding the configurations needed for the web app to successfully invoke thePet Management Service REST API. These configurations need to be updated for each environment you deploy the web app. Here you will be updating the configurations for the development environment.

To configure the front-end application, follow the steps given below.
1. While on the web application component page. Click and expand **Dev Ops** in the left menu.
2. Select **Configs and Secrets** sub menu.
3. Select **+Create**.
4. Select the below mount configuration options and click **Next**.
   | **Field** | **Description** |
   | -------- | -------- |
   | Config Type | Config Map |
   | Mount Type | File Mount |
5. Provide the below values for mount configuration
   | **Field** | **Description** |
   | -------- | -------- |
   | Config Name | webapp-configs |
   | Mount Path | **/usr/share/nginx/html/config.js**. Every config that needs to be exposed through the web server should be placed inside /usr/share/nginx/html/ |
6. Copy the config details as a JSON file as shown below into the text area.
   ```
   window.config = {
    baseUrl: "https://api.asgardeo.io/t/<your-org-name>",
    clientID: "<asgardeo-client-id>",
    signInRedirectURL: "<web-app-url>",
    signOutRedirectURL: "<web-app-url>",
    resourceServerURL: "<pet-management-service-url>"
    };
   ```
 7. Fill the placeholders with the values you copied from the previous steps as follows.
    - baseUrl
        - Open the **application**(`Pet Management App`) you created previously via **Developer Portal**.
        - Click **Production** Keys in the left navigation menu.
        - Go to the **Endpoints** section.
        - Copy and paste the **Token Endpoint** value and remove `/oauth2/token` part from the url. eg: https://api.asgardeo.io/t/{organization_name}

    - clientID
        - Open the **application**(`Pet Management App`) you created previously via **Developer Portal**.
        - Click **Production** Keys in the left navigation menu.
        - Copy and paste the value of the **Consumer Key**.
      
    - resourceServerURL
        - Open the **API** you created previously via **Developer Portal**.
        - In the **Overview** section of the API, you can find the **Endpoint(s)**.
        - Copy and paste the value of On the **Endpoint(s)** section.

    - signInRedirectURL and signOutRedirectURL
      - You will receive values for signInRedirectURL and signOutRedirectURL in the next sections. For now keep the default values for those configurations.
8. Click **Create**.

## Step 3.4: Deploy the front-end application

1. Navigate to **Build and Deploy** section on the left navigation menu.
2. Click **Deploy Manually** on the **Build Area**.
3. When the application is deployed successfully you will get an url in the section **Web App URL**.
4. Copy and paste the url as the **SIGN-IN-REDIRECT-URL** and **SIGN-OUT-REDIRECT-URL** in the config.js in **step 3.2**.
5. Click **DevOps** section in the component and click **Configs & Secrets**.
6. On the secret, webapp-configs you created, click the **edit icon** on the right side corner.
7. Provide the config.js content and click **Save**.

&nbsp;<br>

# Run Locally

## Prerequisites:

- Node.js (version 10 or above).

### Configure the Sample

Update configuration file `src/config.js` with your registered app details.

**Note:** You will only have to paste in the `client ID` generated for the application you registered.

Read more about the SDK configurations [here](../../README.md#authprovider).

```js
{
    "clientID": "<ADD_CLIENT_ID_HERE>",
    "baseUrl": "https://api.asgardeo.io/t/<org_name>",
    "signInRedirectURL": "http://localhost:3000",
    "signOutRedirectURL": "http://localhost:3000",
    "scope": ["profile","openid","email"],
    "resourceServerURL": "<API-ENDPOINT-OF-PET-MGT-SERVICE>",
    "billingServerURL": "<API-ENDPOINT-OF-BILLING-MGT-SERVICE>"
}
```

### Run the Application

```bash
npm install && npm start
```
The app should open at [`http://localhost:3000`](http://localhost:3000)
