---
title: "Email Automation"
excerpt: "Google Apps Script, Google Sheets, & HTML, Oh My!"
author: James Malloy
draft: true
date: '2022-03-21'
slug: []
categories: [learn with me, automation]
tags: [learn with me, automation]
---

## TL;WR

I'm trying automate an email using Google Apps Script & Google Sheets. I was able to get my script to run but the it still needs some work. If you can offer me some tips on Google Apps Script/JavaScript/HTML (or just simply want to know what I'm doing) feel free to keep reading. Thanks!

## The Task

I want to automate a weekly email that is sent to my students. The content of the email is an html table with scholarship information for my students to apply to. Because the primary data source at my organization is Google, I want the automation to be accessible (physically and conceptually) to anyone after I leave. That's why I've decided to go with Google Apps Script & Sheets. Unfortunately, I've never worked with Apps Script, JavaScript, or HTML before this, so I'm out of my element. Try not to judge my code too bad (I'm sure its unsightly). Your feedback is welcome. Here's a play-by-play of my work thus far:

## My Attempt

First, I created this function in Google Apps script.


```js
function sendScholarshipEmail() {

/// SEND EMAIL FUNCTION
GmailApp.sendEmail(recipient, subject, body, cc, bcc)
}
```


<script type="text/javascript">
function sendScholarshipEmail() {

/// SEND EMAIL FUNCTION
GmailApp.sendEmail(recipient, subject, body, cc, bcc)
}
</script>

### Email Recipients

My email recipients are myself (`recipient`), my colleagues (`cc`), and my students (`bcc`). The email addresses are being fetched from [a Google Sheet](https://docs.google.com/spreadsheets/d/1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc/edit?usp=sharing).


```js
function sendScholarshipEmail() {

// RECIPIENTS
let recipient = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("A2").getValues()
let cc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("B2:B5").getValues().toString()
let bcc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("C2:C11").getValues().toString()

/// SEND EMAIL FUNCTION
GmailApp.sendEmail(recipient, subject, body, cc, bcc)
}
```


<script type="text/javascript">
function sendScholarshipEmail() {

// RECIPIENTS
let recipient = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("A2").getValues()
let cc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("B2:B5").getValues().toString()
let bcc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("C2:C11").getValues().toString()

/// SEND EMAIL FUNCTION
GmailApp.sendEmail(recipient, subject, body, cc, bcc)
}
</script>

### Email Subject

I want the email subject to read something like "Weekly Scholarship Email: March 21, 2022". So far, I've only been able to get the date formatted with numbers like this: "Weekly Scholarship Email: 03-21-2022."


```js
function sendScholarshipEmail() {

// RECIPIENTS
let recipient = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("A2").getValues()
let cc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("B2:B5").getValues().toString()
let bcc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("C2:C11").getValues().toString()

// SUBJECT
let date = Utilities.formatDate(new Date(), "EST", "MM-dd-YYYY")
let subject = "Weekly Scholarships Email: " + date

/// SEND EMAIL FUNCTION
GmailApp.sendEmail(recipient, subject, body, cc, bcc)
}
```


<script type="text/javascript">
function sendScholarshipEmail() {

// RECIPIENTS
let recipient = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("A2").getValues()
let cc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("B2:B5").getValues().toString()
let bcc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("C2:C11").getValues().toString()

// SUBJECT
let date = Utilities.formatDate(new Date(), "EST", "MM-dd-YYYY")
let subject = "Weekly Scholarships Email: " + date

/// SEND EMAIL FUNCTION
GmailApp.sendEmail(recipient, subject, body, cc, bcc)
}
</script>

### Email Body (Where I need the most help)

My Google Sheet includes a second tab with the [scholarship data](https://docs.google.com/spreadsheets/d/1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc/edit?usp=sharing). I want the script to filter through the table and send scholarship information conditional on the open and close date of the scholarship. I also want the table within the email to have a nice format. Thanks to this video on YouTube by Shine Vision[^1] I was able to copy-paste my way to partially successful completion of this task. 

[^1]: https://www.youtube.com/watch?v=IQltwJVzo10&t=12s


```js
function sendScholarshipEmail() {

// RECIPIENTS
let recipient = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("A2").getValues()
let cc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("B2:B5").getValues().toString()
let bcc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("C2:C11").getValues().toString()

// SUBJECT
let date = Utilities.formatDate(new Date(), "EST", "MM-dd-YYYY")
let subject = "Weekly Scholarships Email: " + date

//BODY
let data = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getSheetByName("scholarships").getDataRange().getValues()

let body = '<html><body> Hi, Scholars <br> <br> Here is your weekly list of scholarships. Please look carefully through each one and apply to those for which you are eligible. Be sure to add the information to your Scholarship Tracker. And, as always, keep your CRC and College Advisor in the loop. <br> <br> Best, <br> <br> The Senior Team <br> <br> <br> Hola, estudiantes <br> <br> Aquí está su lista semanal de becas. Lee detenidamente cada uno de ellos y solicite aquellos para los que seas elegible. Asegúrate de agregar la información a su Rastreador de Becas. Y, como siempre, mantén informados a tu CRC y College Advisor. <br> <br> Atentamente, <br> <br> The Senior Team <br> <br> <table style = border-collapse; border= 1 cellpadding = 5><tr>';
for (var row=0; row<data.length;++row){
  for (var col = 0; col<data[0].length;++col)
  {
    if (row==0)
    {body+=',<th>'+data[row][col]+'</th>'}
    else{
      body+=',<td>'+data[row][col]+'</td>'
    }
  }
  body+='</tr><tr>'
}

body += '</tr></table></body></html>'

/// SEND EMAIL FUNCTION
GmailApp.sendEmail(recipient, subject, body, cc, bcc)
}
```


<script type="text/javascript">
function sendScholarshipEmail() {

// RECIPIENTS
let recipient = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("A2").getValues()
let cc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("B2:B5").getValues().toString()
let bcc = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getRange("C2:C11").getValues().toString()

// SUBJECT
let date = Utilities.formatDate(new Date(), "EST", "MM-dd-YYYY")
let subject = "Weekly Scholarships Email: " + date

//BODY
let data = SpreadsheetApp.openById("1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc").getSheetByName("scholarships").getDataRange().getValues()

let body = '<html><body> Hi, Scholars <br> <br> Here is your weekly list of scholarships. Please look carefully through each one and apply to those for which you are eligible. Be sure to add the information to your Scholarship Tracker. And, as always, keep your CRC and College Advisor in the loop. <br> <br> Best, <br> <br> The Senior Team <br> <br> <br> Hola, estudiantes <br> <br> Aquí está su lista semanal de becas. Lee detenidamente cada uno de ellos y solicite aquellos para los que seas elegible. Asegúrate de agregar la información a su Rastreador de Becas. Y, como siempre, mantén informados a tu CRC y College Advisor. <br> <br> Atentamente, <br> <br> The Senior Team <br> <br> <table style = border-collapse; border= 1 cellpadding = 5><tr>';
for (var row=0; row<data.length;++row){
  for (var col = 0; col<data[0].length;++col)
  {
    if (row==0)
    {body+=',<th>'+data[row][col]+'</th>'}
    else{
      body+=',<td>'+data[row][col]+'</td>'
    }
  }
  body+='</tr><tr>'
}

body += '</tr></table></body></html>'

/// SEND EMAIL FUNCTION
GmailApp.sendEmail(recipient, subject, body, cc, bcc)
}
</script>

### End Product

With the code above, I'm able to get the script to run. It's odd to me though that the dates in the table are time stamps even though they're not formatted that way in the spreadsheet. The email I receive in my inbox looks like this:

<center>

![email-gif](/media/video-google-app-script.gif)

</center>


## Help Needed

Here's where I'm still trying to figure things out:

1. **Filtering the table** so that the email body includes: 1) only those scholarships whose "open date" is no more than 3 weeks into the future and 2) scholarships whose deadline has not passed.

2. **Formatting the dates** so that the month is written out in the email subject and the email table. 

3. **Formatting the table** with a nicer header, proper spacing between cells, and without weird gaps between the cell borders.

4. **Scheduling the email** for a specific, recurring time (e.g. weekly on Mondays at 8am).

5. **Adding a UI button** to the [Google Sheet](https://docs.google.com/spreadsheets/d/1nooIWAD9K3JBMgEMC_sx3XK2YWNOx9awOlU-8UiEVmc/edit#gid=0), (**not** the Google Apps Script) that says "Send Email" with a  "Send Scholarship Email" drop down button.

Thanks in advance to anyone able to help. Also, I don't assume that this is the exact best way to go about getting the desired product. So feel free to pose alternative suggestions, especially if it's using a "low-lift" Google product.

Lastly, as always, if anyone is just curious to know more about me, this project, or my data journey, feel free to reach out.

~ James
