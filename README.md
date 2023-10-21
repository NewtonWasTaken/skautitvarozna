# skautitvarozna

Python code, which connects WP Forms from website <a href="https://www.skautitvarozna.cz">skautitvarozna.cz</a> with Google Sheets and Google Calendar.

Hosted on Raspberry Pi 4. 


<h1>What does it do?</h1>
It is a service that needs to be running 24/7. I decided to host it on my Raspberry Pi 4 using <a href="https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units">systemctl</a>.

<h2>Main function</h2>

- The program connects all required WP Forms with Google Sheets

<h2>Custom functions</h2>
Both these functions can be simply turned off by deleteing the ifs on lines <a href="https://github.com/NewtonWasTaken/skautitvarozna/blob/master/main.py#L179">179</a> and <a href="https://github.com/NewtonWasTaken/skautitvarozna/blob/master/main.py#L185">185</a> and changing the elif on line <a href="https://github.com/NewtonWasTaken/skautitvarozna/blob/master/main.py#L225">225</a> to if in main.py.

- Sends an additional email notification with custom design when specific form is filled
- Used for reservation system, connects one specific form with Google Calendar

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
  - To Content add {form-id} and on next line {all-fields}

