---
layout: post
title:  "Blog-14-Google-Sheets"
date:   2022-02-22 11:58:57 -0700
categories: Munki MDM Tool
---

<h1>Google Applications</h1>
      There are many Google Applications such as Google Mail, slides, docs, calendar, drive 
      and more. The Applications we will be using is the Google sheets. In Sheets we have 
      access to the other google applications and unquine features Google offices, the mail 
      feature we will use in Google sheet is the Mail Merge extension

<h1>How Google Mail Merge work</h1>
      You make a Gmail draft format with stand ins for data from a Google Sheets 
      spreadsheet. A placeholder tag is represented by each column heading in a 
      sheet. The script transmits each placeholder's information from the spreadsheet 
      to the location of the appropriate replacement tag in your email document.

<h1>Step 1: Copy spread sheet </h1>
- In the new spread sheet, we will navigate to extensions --> app scripts and import the script provided by google for mail or make a copy of the mail merge 


- In this new mail merge sheet, write in one of the columns RECIPIENTS with th email addresses you want to mail merge
Example 1

- You can Add, edit, and remove columns to whatever is need for the data your email template.

- You must edit the related code in the Apps Script project if you alter the name of the Recipient or Email Sent columns. Click Extensions > Apps Script to open the Apps Script project.

<h1>Step 2: Create an email template </h1>
- Create a google email to use as template, if you would like to call out the data from the mail merge sheet, we have to label the email correctly with the columns. For example {{FirstName}}, {{LastName}}, {{Date}} and more. The double brackets capture the column needs in the from the sheet.

- Once the draft is complete and the subject line an apocopate and save a draft or a templet.
 
 <h1>Step 3: Send Emails</h1>
 - To send these emails with the data we must navigate to sheet, click mail merge---> Send emails. It will prompt you to input the google templet name you have, once entered it will take a few mins to send. If you do not see the tool you might need to refresh the page for this custom menu to appear.
 
 - Click Mail Merge > Send Emails again.

 - Paste the email template's subject line and click OK. 

<img src="https://developers.google.com/apps-script/samples/images/mail-merge.gif" alt="Jira" width="460" height="345">

<h1>Summary:</h1>
Make a copy of mail merge sheet
      - Label the columns anything you???d like such as FirstName, LastName, date and more but one of the one column must have the Recipient because this is email that will be used to mail merge with your templet
      
Create an email templet with a subject line, type information in the email templet. To use the data from the sheet you must label words in your templet for example:

Hello {{FirstName}},

Welcome {{FirstName}} {{LastName}} to the CSUN and we want to attend our master???s degree program on {{Date}}.

Best,
Andrew

In this example we have labeled the data we want to use from sheets.

Once the templet is created, we will now navigate to the spread sheet and click mail merge --> send the email. It will prompt you for the templets subject line that was created. copy and paste the subject line text and send.


