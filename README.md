# skautitvarozna

Project, which connects forms from website skautitvarozna.cz with Google Sheets and Google Calendar.

Hosted on Raspberry Pi 4. 


<h1>Requirements</h1>
Note that this project is even after this not usable for any other website. These requirements are here for reinstalling this project from ground for the same website :).

<h2>Modules</h2>
- install all required modules using: "pip install -r requirements.txt"

<h2>Enviroment variables</h2>

```
ADMIN_EMAIL={Email of the administrator}
DATABASE_PASSWORD={Password for MongoDB database}
DATBASE_LOGIN={Login for MongoDB database} 
EMAIL_LOGIN={Email of noreply account}
EMAIL_PASSWORD={Password for noreply account}
IMAP_SERVER={IMAP server of the noreply account}
SMTP_SERVER={SMTP server of the noreply account}
NOTIFICATION_EMAIL={Email for notifications about registrations and reservations}
```
- variable DATABASE_LOGIN needs to be changed manually on line <a href="https://github.com/NewtonWasTaken/skautitvarozna/blob/master/main.py#L164">164</a>

<h2>Google service account key</h2>
- create a new project in Google Cloud
- enable Google Sheets a Calendar API
- add new <a href="https://cloud.google.com/iam/docs/service-account-overview">service account</a> and create a key for it in JSON format
- name the key "credentials.json" and put it next to main.py

