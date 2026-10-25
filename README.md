GigTracker: CS 360 Mobile App Development

GigTracker is an Android app (Java, SQLite) for tracking upcoming concerts.

Contents

GigTrackerFinal.zip: the complete Android Studio project 
CS360 GigTracker Launch Plan.docx: the launch plan 
Requirements, goals, and user needs

GigTracker helps concert-goers keep track of the shows they plan to attend. Fans often buy tickets months ahead and then lose track of dates, so the app has three goals. Each person gets a private account. The user can add, view, edit, and delete events in one place. And the app can text a reminder when a show is close. The reminders are optional, and the app has to work completely without them.

Screens, features, and user-centered design

Three screens support the user’s task:

Login: username and password fields (the password is masked), a Log In button, and a Create Account button for first-time users.
Events grid: an add-event form, a table with headers (Artist, Venue, Date, Actions), and Edit and Delete buttons on every row.
SMS settings: a permission request with a plain explanation, Allow and No Thanks choices, a status line, and a test button.

I kept users in mind in several ways. The theme is a dark palette with one green accent. Related fields are grouped in cards. The focus order follows the task (username, then password, then Log In). Every screen uses the same slide transition. Delete buttons are red so they read as destructive, and deleting asks for confirmation. The design works because a first-time user can find the next action on each screen without instructions.

Approach to coding

I split the code into small classes that each do one job: DatabaseHelper (all SQLite reads and writes), Event (the data model and date logic), SmsHelper (permission state and sending texts), UiHelper (shared layout and transition code), and one short activity class per screen. I used consistent naming, comments on every method, input validation, and SHA-256 hashing so passwords are never stored as plain text. Splitting data, logic, and screens makes code easier to test and change, and I can reuse the same structure in future apps.
Innovation and challenges
Environment problems: I recreated the project with the correct Views template, matched the package name and namespace, and cleared the corrupted Gradle download.
Newer Android versions: Android 15 and later enforce edge-to-edge screens, so I wrote a shared helper that applies system-bar insets so content isn’t hidden.
Repeat texts: I added a “notified” flag to the database so a reminder is sent once per event, and it resets if the user changes the date.
Platform policy: Researching for my launch plan, I found that Google Play restricts the SEND_SMS permission to default messaging apps and approved exceptions. The plan names local push notifications as the fallback.
Where I was most successful

The database and permission handling were my strongest components. The database supports full create, read, update, and delete for each user’s events, with hashed passwords and validated dates. The SMS flow checks the permission at runtime, handles both a grant and a denial, and never breaks the rest of the app.
