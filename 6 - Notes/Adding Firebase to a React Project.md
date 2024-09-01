#### Created: 2024-08-21
#### Tags: [[React]] [[Firebase]]
#### Links: 
[[React Project Setup - Overview]]
[Firebase Console](https://console.firebase.google.com/)
# Adding Firebase to a React Project

1. Go to the [Firebase Console](https://console.firebase.google.com/).

2. Click "Add project" and follow the prompts to create a new Firebase project.

3. In the project overview, click "Add app" and choose the web platform (</>).

4. Register your app with a nickname (e.g., "My React App").

5. Copy the Firebase configuration object provided.

6. Install Firebase in your project:
```bash
npm install firebase
```

7. Create a new file `src/firebase.js` and paste the Firebase configuration:
   ```javascript
   import { initializeApp } from 'firebase/app';

   const firebaseConfig = {
     // Paste your Firebase configuration object here
   };

   const app = initializeApp(firebaseConfig);
   export default app;
   ```

8. Run the Firebase initialization command:
   ```bash
   firebase init
   ```

9. Choose the services you need. If asked for a public directory, set it to "dist" for Vite or "build" for Create React App.

10. Configure as a single-page app: Choose "Yes" when prompted.

Adding Firebase provides powerful backend services to your React application.