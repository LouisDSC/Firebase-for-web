![Firebase](https://github.com/LouisDSC/Firebase-pour-le_web/blob/main/Img/Img.png)

# Firebase for Web | FirebaseUI FirebaseAuth Firestore
## Features
This programming workshop will allow you to discover the basics of Firebase and use them to create interactive web applications.

## What you will learn
- Authenticate users with [Firebase Authentication](https://firebase.google.com/docs/auth?hl=fr) ;
 and [FirebaseUI](https://firebase.google.com/docs/auth/web/firebaseui?hl=fr);
- Sync data using [Cloud Firestore](https://firebase.google.com/docs/firestore);
- Write [Firebase](https://firebase.google.com/).

## What you'll need
- A browser of your choice, such as Chrome ;
- Access to [stackblitz](http://stackblitz.com/) (no account or sign-in necessary);
- A Google account, like a gmail account. We recommend the email account that you already use for your GitHub account. This allows you to use advanced features in StackBlitz;
- The codelab's sample code. See the next step for how to get the code.

## Get started now !
1. Noted that in this codelab, you build an app using [stackblitz](http://stackblitz.com/), an online editor that has several Firebase workflows integrated into it. Stackblitz requires no software installation or special StackBlitz account.
2. Go to [this URL](https://stackblitz.com/edit/firebase-gtk-web-start).
3. You can modify the file `index.html` as you see fit while leaving the ID and class untouched.
4. Create a Firebase project
   - Sign in to [Firebase](https://firebase.google.com/)
   - In the Firebase console, click Add Project (or Create a project), then name your Firebase project  Codelab-for-firebase-web.
   - On the Google Analytics screen, click "Don't Enable", because you won't be using Analytics for this app.
   - If you want to know more about firebase projects, I advise you to read the [documentation](https://firebase.google.com/docs/projects/learn-more?hl=fr) before continuing.

## Enable and set up Firebase products in the console !
1. Firebase Authentication and Firebase UI to easily allow your users to sign in to your app.
To allow users to sign in to the web app, you'll use the Email/Password sign-in method for this codelab:
   - In the left-side panel of the Firebase console, click Build > Authentication. Then click Get Started. You're now in the Authentication dashboard, where you can see signed-up users, configure sign-in providers, and manage settings.
   - Select the Sign-in method tab and then click Email/Password from the provider options, toggle the switch to Enable, and then click Save.

2. Set up Cloud Firestore
The web app uses Cloud Firestore to save chat messages and receive new chat messages. 
   - In the left-side panel of the Firebase console, click Build > Firestore Database. Then click Create database.
   - Click Create database.
   - Select the Start in test mode option. Read the disclaimer about the security rules. Test mode ensures that you can freely write to the database during development. Click Next.

   ```
   Caution: In the first stages of this codelab, you use test mode. Later in the codelab, though, you'll write Firebase Security Rules to secure your database.
   For your apps, especially production apps, it's very important that you secure your database using security rules. Learn more about security rules in the Firebase documentation.
   ```
   - Select the location for your database (you can just use the default). Note, though, that this location can't be changed later. And then done.

3.  Add and configure Firebase
Now that you have your Firebase project created and some services enabled, you need to tell the code that you want to use Firebase, as well as which Firebase project to use.

For your app to use Firebase, you need to add the Firebase libraries to the app. There are multiple ways to do this, as described in the  [Firebase documentation](https://firebase.google.com/docs/web/setup). For example, you can add the libraries from Google's CDN, or you can install them locally using npm and then package them in your app if you're using Browserify.

To build this app, you use the Firebase Authentication, FirebaseUI, and Cloud Firestore libraries. For this codelab, the following import statements are already included at the top of the index.js file, and we'll be importing more methods from each Firebase library as we go:
```JS
// Import stylesheets
import './style.css';

// Firebase App (the core Firebase SDK) is always required
import { initializeApp } from 'firebase/app';

// Add the Firebase products and methods that you want to use
import {} from 'firebase/auth';
import {} from 'firebase/firestore';

import * as firebaseui from 'firebaseui';
```

4. Add a Firebase web app to your Firebase project
- Back in the Firebase console, navigate to your project's overview page by clicking Project Overview in the top left.
- In the center of your project's overview page, click the web icon web app icon </> to create a new Firebase web app.
- Register the app with the nickname Web App.
- For this codelab, do NOT check the box next to Also set up Firebase Hosting for this app. You'll use StackBlitz's preview pane for now.
- Click Register app.
- Copy the [Firebase configuration object](https://firebase.google.com/docs/projects/learn-more#config-files-objects) to your clipboard. In your JS file `index.js` replace the dotted lines with likee this :
```JS
const firebaseConfig = {
  apiKey: "AIzaSyACNHNPpKGV0Aa3l37-3EF6v2gax9TyWnM",
  authDomain: "codelab-for-firebase-web.firebaseapp.com",
  projectId: "codelab-for-firebase-web",
  storageBucket: "codelab-for-firebase-web.appspot.com",
  messagingSenderId: "1049708353117",
  appId: "1:1049708353117:web:c4ed3ad688e64975b91fb4"
};
```

5. Authenticate your users with Email Sign-In and FirebaseUI
You'll need an RSVP button that prompts the user to sign in with their email address. You can do this by hooking up [FirebaseUI](https://firebase.google.com/docs/auth/web/firebaseui) to an RSVP button.FirebaseUI is a library which gives you a pre-built UI on top of Firebase Auth.

FirebaseUI requires a configuration (see the options in the [documentatoin](https://github.com/firebase/firebaseui-web#example-with-all-parameters-used)) that does two things:
   - Tells FirebaseUI that you want to use the Email/Password sign-in method.
   - Handles the callback for a successful sign-in and returns false to avoid a redirect. You don't want the page to refresh because you're building a single-page web app.

At the top, locate the `firebase/auth` import statement, then add `getAuth` and `EmailAuthProvider`, like so:
```JS
// Add the Firebase products and methods that you want to use
import { getAuth, EmailAuthProvider } from 'firebase/auth';

import {} from 'firebase/firestore';
```

## Here is an analysis of each part of the code:

- The first line of code imports the style.css file, which contains the CSS styles for the application.
- The next few lines of code import the necessary Firebase libraries.
- The `initializeApp()` function initializes the Firebase app.
- The `getAuth()` function gets the FirebaseAuth instance.
- The `getFirestore()` function gets the Firestore instance.
- The `startRsvpButton` variable stores the reference to the RSVP button.
- The `guestbookContainer` variable stores the reference to the guestbook container.
- The `form` variable stores the reference to the form.
- The `input` variable stores the reference to the input field in the form.
- The `guestbook` variable stores the reference to the guestbook element.
- The `numberAttending` variable stores the reference to the element that displays the number of attendees.
- The `rsvpYes` variable stores the reference to the RSVP yes button.
- The `rsvpNo `variable stores the reference to the RSVP no button.
- The `rsvpListener` variable stores the listener for RSVP updates.
- The `guestbookListener` variable stores the listener for guestbook updates.
- The `db variable` stores the Firestore database instance.
- The `auth` variable stores the FirebaseAuth instance.
- The `main()` function is the entry point for the application.

```JS
// Import stylesheets
import './style.css';

// Firebase App (the core Firebase SDK) is always required
import { initializeApp } from 'firebase/app';

// Add the Firebase products and methods that you want to use
import {
  getAuth,
  EmailAuthProvider,
  signOut,
  onAuthStateChanged,
} from 'firebase/auth';

import {
  getFirestore,
  addDoc,
  collection,
  query,
  orderBy,
  onSnapshot,
  doc,
  setDoc,
  where,
} from 'firebase/firestore';

import * as firebaseui from 'firebaseui';

// Document elements
const startRsvpButton = document.getElementById('startRsvp');
const guestbookContainer = document.getElementById('guestbook-container');

const form = document.getElementById('leave-message');
const input = document.getElementById('message');
const guestbook = document.getElementById('guestbook');
const numberAttending = document.getElementById('number-attending');
const rsvpYes = document.getElementById('rsvp-yes');
const rsvpNo = document.getElementById('rsvp-no');

let rsvpListener = null;
let guestbookListener = null;

let db, auth;

async function main() {
  // Add Firebase project configuration object here
  const firebaseConfig = {
    apiKey: '....',
    authDomain: '....',
    projectId: '....',
    storageBucket: '....',
    messagingSenderId: '....',
    appId: '....',
  };
  // initializeApp(firebaseConfig);
  initializeApp(firebaseConfig);
  auth = getAuth();
  db = getFirestore();

  // FirebaseUI config
  const uiConfig = {
    credentialHelper: firebaseui.auth.CredentialHelper.NONE,
    signInOptions: [
      // Email / Password Provider.
      EmailAuthProvider.PROVIDER_ID,
    ],
    callbacks: {
      signInSuccessWithAuthResult: function (authResult, redirectUrl) {
        // Handle sign-in.
        // Return false to avoid redirect.
        return false;
      },
    },
  };
  // const ui = new firebaseui.auth.AuthUI(auth);

  // Initialize the FirebaseUI widget using Firebase
  const ui = new firebaseui.auth.AuthUI(auth);
  // Listen to RSVP button clicks
  // Called when the user clicks the RSVP button
  startRsvpButton.addEventListener('click', () => {
    if (auth.currentUser) {
      // User is signed in; allows user to sign out
      signOut(auth);
    } else {
      // No user is signed in; allows user to sign in
      ui.start('#firebaseui-auth-container', uiConfig);
    }
  });
  // Listen to the current Auth state
  onAuthStateChanged(auth, (user) => {
    if (user) {
      startRsvpButton.textContent = 'LOGOUT';
      // Show guestbook to logged-in users
      guestbookContainer.style.display = 'block';
      // Subscribe to the guestbook collection
      subscribeGuestbook();
      // Subcribe to the user's RSVP
      subscribeCurrentRSVP(user);
    } else {
      startRsvpButton.textContent = 'RSVP';
      // Hide guestbook for non-logged-in users
      guestbookContainer.style.display = 'none';
      // Unsubscribe from the guestbook collection
      unsubscribeGuestbook();
      // Unsubscribe from the guestbook collection
      unsubscribeCurrentRSVP();
    }
  });
  // Listen to the form submission
  form.addEventListener('submit', async (e) => {
    // Prevent the default form redirect
    e.preventDefault();
    // Write a new message to the database collection "guestbook"
    addDoc(collection(db, 'guestbook'), {
      text: input.value,
      timestamp: Date.now(),
      name: auth.currentUser.displayName,
      userId: auth.currentUser.uid,
    });
    // clear message input field
    input.value = '';
    // Return false to avoid redirect
    return false;
  });
  // Listen to guestbook updates
  function subscribeGuestbook() {
    const q = query(collection(db, 'guestbook'), orderBy('timestamp', 'desc'));
    guestbookListener = onSnapshot(q, (snaps) => {
      // Reset page
      guestbook.innerHTML = '';
      // Loop through documents in database
      snaps.forEach((doc) => {
        // Create an HTML entry for each document and add it to the chat
        const entry = document.createElement('p');
        entry.textContent = doc.data().name + ': ' + doc.data().text;
        guestbook.appendChild(entry);
      });
    });
  }
  // Unsubscribe from guestbook updates
  function unsubscribeGuestbook() {
    if (guestbookListener != null) {
      guestbookListener();
      guestbookListener = null;
    }
  }
  // Listen to RSVP responses
  rsvpYes.onclick = async () => {
    // Get a reference to the user's document in the attendees collection
    const userRef = doc(db, 'attendees', auth.currentUser.uid);

    // If they RSVP'd yes, save a document with attendi()ng: true
    try {
      await setDoc(userRef, {
        attending: true,
      });
    } catch (e) {
      console.error(e);
    }
  };
  rsvpNo.onclick = async () => {
    // Get a reference to the user's document in the attendees collection
    const userRef = doc(db, 'attendees', auth.currentUser.uid);

    // If they RSVP'd yes, save a document with attending: true
    try {
      await setDoc(userRef, {
        attending: false,
      });
    } catch (e) {
      console.error(e);
    }
  };
  // Listen for attendee list
  const attendingQuery = query(
    collection(db, 'attendees'),
    where('attending', '==', true)
  );
  const unsubscribe = onSnapshot(attendingQuery, (snap) => {
    const newAttendeeCount = snap.docs.length;
    numberAttending.innerHTML = newAttendeeCount + ' people going';
  });
  // Listen for attendee list
  function subscribeCurrentRSVP(user) {
    const ref = doc(db, 'attendees', user.uid);
    rsvpListener = onSnapshot(ref, (doc) => {
      if (doc && doc.data()) {
        const attendingResponse = doc.data().attending;

        // Update css classes for buttons
        if (attendingResponse) {
          rsvpYes.className = 'clicked';
          rsvpNo.className = '';
        } else {
          rsvpYes.className = '';
          rsvpNo.className = 'clicked';
        }
      }
    });
  }
  function unsubscribeCurrentRSVP() {
    if (rsvpListener != null) {
      rsvpListener();
      rsvpListener = null;
    }
    rsvpYes.className = '';
    rsvpNo.className = '';
  }
}
main();
```

## Congrats !

You've used Firebase to build an interactive, real-time web application!

- What we've covered
- Firebase Authentication
- FirebaseUI
- Cloud Firestore
- Firebase Security Rules

You can read my article about it here
