# Auto Assign Reporting Tag Zoho Books
Automatically creates and assigns a Reporting Tag to an Invoice Line Item, if there is an associated Project. Can be adapted to work on other modules.

## Configuration
This function relies heavily on the Zoho Books API. To access this API, we need to create a Custom Connection to Zoho Books. Here are the steps you need to take to create this Custom Connection:
### Create API Credentials: Gives you a Client ID and Client Secret to use in the next step.
1. Go to the [Zoho API Console](https://api-console.zoho.com/)
2. Click **Add Client** and select **Server-based Applications**
3. Fill in the following fields:
   * **Client Name** -> `Zoho Books API`
   * **Homepage URL** -> `https://books.zoho.com`
   * **Authorized Redirect URIs** -> `https://deluge.zoho.com/delugeauth/callback`
4. Click **Update**
5. Notice the *Client ID* and *Client Secret* here. You will need these in the next step, so keep this tab open.
  
### Create Custom Connection
1. Go to [Zoho Books](https://books.zoho.com)
2. Click **Settings**, select the **Automation** tab, then choose **Custom Functions**.
3. Select **+ New Custom Function** and give it a random name and module. We will only use this function for a simple test.
4. Choose **Connections** on the right hand side, then **Go To Connections**.
5. Click **Add Connection**. Choose **Custom Service**.
6. Fill in the following fields (This has to be very exact):
   * **Service Name** -> `Zoho Books`
   * **Service LinkName** -> `zoho_books`
   * **Authentication Type** -> `oAuth2`
   * **Param Type** -> `Header`
   * **Grant Type** -> `Authorization Code`
   * **Client ID** -> `[YOUR_CLIENT_ID]`
   * **Client Secret** -> `[YOUR_CLIENT_SECRET]`
   * **Authorize URL** -> `https://accounts.zoho.com/oauth/v2/auth?`
   * **Access Token URL** -> `https://accounts.zoho.com/oauth/v2/token?`
   * **Refresh Token URL** -> `https://accounts.zoho.com/oauth/v2/token?`
   * **Connection Name** -> `Zoho Books`
   * **Connection LinkName** -> `zoho_books`
   * **Scope** -> `ZohoBooks.fullaccess.all` (Note: Be sure to click the **'+'** for the scope)
   * **Use credentials of login user** -> `UNCHECKED`
7. Click **Create and Connect**. If asked to authenticate, enter your login details.

### Test the Connection
1. Go to the custom function you previously created.
2. Input the following:
    ```
    organizationId = organization.get("organization_id");

    response = invokeUrl [
      url : "https://books.zoho.com/api/v3/invoices?organization_id=" + organizationId
        type : GET
        connection : "zoho_books"
    ];

    info response;
    ```
3. Run the script and make sure you receive a response that is not an error.
  
     
     
  
  

    

