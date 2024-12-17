# SecureScore

## **I know this is blank im still working on it. Here is the idea**

A React-based web application that integrates with **Microsoft Graph API** to display **Secure Score** and improvement recommendations for an organization. The application allows Global Admin users to log in, view their Secure Score metrics, and track steps to improve their security posture.

---

## **Features**

1. **Azure AD Authentication**  
   - Log in securely using Azure AD credentials as a Global Admin.
   - Authentication handled using `@azure/msal-react`.

2. **Secure Score Visualization**  
   - Displays the current Secure Score with a **speedometer** gauge using `react-d3-speedometer`.

3. **Improvement Steps**  
   - Fetches actionable steps to improve Secure Score from Microsoft Graph API.
   - Dynamically displays them in a roadmap-style interface.

4. **Logout Functionality**  
   - Users can log out via the settings page.

5. **Error Handling and Timeout**  
   - If the Secure Score or improvement steps fail to load within 5 seconds, an error message prompts the user to retry.

---

## **Tech Stack**

- **Frontend**: React.js  
- **Authentication**: Microsoft Authentication Library (`@azure/msal-react`)  
- **Data Fetching**: Microsoft Graph API  
- **Styling**: CSS, Flexbox, Custom Animations  
- **UI Components**:  
   - `react-d3-speedometer` for the Secure Score gauge  
   - Custom roadmap component for steps display  

---

## **Setup Instructions**

### **1. Prerequisites**

- **Node.js** (v16+ recommended)
- An **Azure AD Application Registration**:
   - `Client ID` (Application ID)
   - `Tenant ID` (Directory ID)
   - Redirect URI (e.g., `http://localhost:3000`)
   - API Permissions:
     - `SecurityEvents.Read.All`
     - `SecureScores.Read.All`
     - `SecureScoreControlProfiles.Read.All`

---

### **2. Clone the Repository**

```bash
git clone https://github.com/your-username/secure-score-dashboard.git
cd secure-score-dashboard
```

---

### **3. Install Dependencies**

Install the required packages:

```bash
npm install
```

---

### **4. Configure the App**

Create a new file `src/msalConfig.js` and add the following configuration:

```javascript
export const msalConfig = {
  auth: {
    clientId: "YOUR_CLIENT_ID", // Replace with Azure AD Application Client ID
    authority: "https://login.microsoftonline.com/YOUR_TENANT_ID", // Replace with Tenant ID
    redirectUri: "http://localhost:3000", // Replace with your app's redirect URI
  },
  cache: {
    cacheLocation: "localStorage",
    storeAuthStateInCookie: true,
  },
};

export const loginRequest = {
  scopes: ["https://graph.microsoft.com/.default"],
};
```

---

### **5. Run the Application**

Start the development server:

```bash
npm start
```

The application will be available at `http://localhost:3000`.

---

## **Usage**

1. Log in using your **Global Admin credentials**.
2. View your current **Secure Score** on the dashboard.
3. Review the **steps to improve Secure Score** in the roadmap section.
4. Use the **Settings** page to log out.

---

## **API Endpoints**

The app uses the following Microsoft Graph API endpoints:

1. **Fetch Secure Score**:
   ```http
   GET https://graph.microsoft.com/v1.0/security/secureScores
   ```

2. **Fetch Improvement Steps**:
   ```http
   GET https://graph.microsoft.com/v1.0/security/secureScoreControlProfiles
   ```

---

## **Error Handling**

- If the data fails to load within **5 seconds**, an error message will prompt the user to retry.
- Users can reload the page or log in again to refresh the data.

---

## **Dependencies**

- `@azure/msal-browser` (Microsoft Authentication Library)
- `@azure/msal-react` (React bindings for MSAL)
- `axios` (HTTP requests)
- `react-d3-speedometer` (Gauge visualization)
- `react-router-dom` (Routing)

Install dependencies with:

```bash
npm install @azure/msal-browser @azure/msal-react axios react-d3-speedometer react-router-dom
```

---

## **Screenshots**

### Secure Score Dashboard
![Secure Score](screenshots/secure-score.png)

### Steps to Improve Secure Score
![Steps Roadmap](screenshots/roadmap.png)

---

## **License**

This project is licensed under the MIT License.

---

## **Contributing**

Contributions are welcome! Please submit a pull request or open an issue to improve this project.

---

## **Acknowledgments**

- [Microsoft Graph API](https://docs.microsoft.com/en-us/graph/overview)
- [React](https://reactjs.org/)
- [MSAL for React](https://github.com/AzureAD/microsoft-authentication-library-for-js)
- [react-d3-speedometer](https://github.com/palerdot/react-d3-speedometer)

---

## **Future Improvements**

1. Add data caching to improve performance.
2. Include visualizations for historical Secure Score trends.
3. Allow role-based access for multiple user types.
