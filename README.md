# skautitvarozna

Project, which connects WP Forms from website skautitvarozna.cz with Google Sheets and Google Calendar.

Hosted on Raspberry Pi 4. 


<h1>Requirements</h1>
Note that this project is even after this hardly usable for any other website. These requirements are here for reinstalling this project from ground for the same website :).

<h2>Modules</h2>

- install all required modules using: "pip install -r requirements.txt"

<h2>Enviroment variables</h2>

```
ADMIN_EMAIL=[Email of the administrator]
DATABASE_PASSWORD=[Password for MongoDB database]
EMAIL_LOGIN=[Email of noreply account]
EMAIL_PASSWORD=[Password for noreply account]
IMAP_SERVER=[IMAP server of the noreply account]
SMTP_SERVER=[SMTP server of the noreply account]
NOTIFICATION_EMAIL=[Email for notifications about registrations and reservations]
```
- you will need to change the whole login link on line <a href="https://github.com/NewtonWasTaken/skautitvarozna/blob/master/main.py#L164">164</a> in main.py (just leave the DATABASE_PASSWORD variable)

<h2>Google service account key</h2>

- create a new project in Google Cloud
- enable Google Sheets a Calendar API
- add new <a target="_blank" href="https://cloud.google.com/iam/docs/service-account-overview">service account</a> and create a key for it in JSON format
- name the key "credentials.json" and put it next to main.py
- you need to share every file and calendar with this service account using the email of the service account

<h2>MongoDB database</h2>

- You will need to setup MongoDB database called "skautitvarozna" and collection named "forms"
- For every form you would like to connect you need to create a new document in "form" collection in following format:

```json
{
"form_id": [Form ID in WP Forms],
"sheet_id":[Google Sheet ID],
"list_name":[Name of Google Sheet list]
}
```

<h2>WP Forms</h2>

- In WP Forms, setup an email notification:
  - Set sender as "tvarozna@skaut.cz" (this can be changed on line <a href="https://github.com/NewtonWasTaken/skautitvarozna/blob/master/main.py#L99">99</a> in main.py)
  - Send reciever as your noreply account
  - To Subject add {form-id}
  - To content add {form-id} and on next line {all-fields}

