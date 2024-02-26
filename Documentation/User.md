# Feature Navigation as a User
---
For easy navigation, please use GitHub's Table of Contents feature: ![TOC](<../Auxiliary Files/Images/User_Images/toc.png>)

---

### Requirements and Assumptions
1. **__The development environment must be setup and running before attempting to use the application__**
    - See [Development.md](Development.md) for steps on how to do this.
2. The server is running - either with `python manage.py runserver` as detailed 
[here](Development.md#testing-the-environment-and-app) or with a full deployment as detailed [here](Deployment.md)
3. URLs point to the local machine on port 8000 - otherwise replace 
`localhost:8000` with the appropriate address.
4. If you are connecting to our cloud deployment (IP will vary with restart), you should use HTTPS. Because we are currently using a self-signed certificate, most browsers will give you a warning. You should proceed anyways to use the software. Here are the fingerprints so you may verify you are connected to the correct site:
```
SHA-1:      30:3E:39:66:C9:26:FB:FA:C6:6E:22:25:1C:AC:89:FF:28:2B:D2:14
SHA-256:    2E:EB:2D:8A:01:0E:41:9E:4B:F8:87:8A:8B:74:3A:A9:16:12:56:CF:EE:73:AF:26:89:8E:36:15:FB:FC:15:B8
```

***

## Opening the Application
- The CME Commitment to Change App is accessed through a local internet browser.
1. Open a web browser (Microsoft Edge, Firefox, Chrome...)
2. In the address bar, type in `http://localhost:8000/`
3. Currently, this welcome page will redirect to the login page.

**All preceding addresses will begin with `http://localhost:8000/` for this specific environment setup**

**If running the development server or Apache without SSL, change `https` to `http` in the links.**


&nbsp;
&nbsp;


---
# General Instructions and Tips
---
## Info icons (Help modals and popovers)
- Look for the info icons throughout the app like the one shown below:
  
![Info Icon](<../Auxiliary Files/Images/User_Images/info-icon.png>)

- You can click on these info icons if you need help or tips for how to use the application effectively. Once clicked, a dialogue box like the one below will show with added information.

![Info Popup](<../Auxiliary Files/Images/User_Images/info-popup.png>)

## Registering for an Account

- This page is used to create new provider user profiles.
- For providers, the address for this page is: `/app/register/provider/`
- For providers, the address for this page is: `/app/register/clinician/`

1. Navigate to the registration webpage. This can be done from the 
login page by clicking on "Click here to register".
 
1. Choose either a clinician account or provider account.

![Account Type](<../Auxiliary Files/Images/User_Images/register_account_type.PNG>)

3.  Fill out the required fields for username, email, password, and password verification.

![Generic register Account](<../Auxiliary Files/Images/User_Images/generic_register.png>)

4. Fill out the Provider/Clinician specific fields:
   
   - PROVIDERS: If you are registering as a provider, you will also need to fill out the required "Institution" field. This field is to associate the courses you make with the institution you represent. (eg. Ball State University, Indiana University, etc.)

![Register Account](<../Auxiliary Files/Images/User_Images/register_provider.png>)

   - CLINICIANS: If you are registering as a clinician, you can fill out the optional "First name", "Last name", and "Institution" fields if you would like. The institution field will associate your account with the institution you attend or are a part of. (eg. Ball State University, Indiana University, etc.) These fields can help providers clarify who has joined their course on the site, so it is recommended that you fill them out.

![Register Clinician Account](<../Auxiliary Files/Images/User_Images/register_clinician.png>)

- Please note that you can reveal the password as you type it by clicking on the eye icon in the password field.

![Register Show Password](<../Auxiliary Files/Images/User_Images/show_password.png>)


5. Select 'Submit'.
   - **If you are redirected back to this page, either an invalid email was used, 
    the password was not strong enough, or the passwords did not match. Error 
    text in this page should inform you of the specific reason.**
6. You will be met with a "Verify your email" page:

![please verify](<../Auxiliary Files/Images/User_Images/verify-email.png>)

7.
   #### Email verification:
   This will vary depending on how the service is deployed when you access it.
   ##### Fully configured deployment with STMP
   Check your email, including your spam folder. You should see an email with subject "Verify you CME Commitment to Change account". Verify that the link points to the same website as you have been accessing and click it/paste it into your browser and hit enter.
   ##### Development environment
   Navigate to your email capture service. If you are using manual replication, [check here for information on where to find the verification email.](https://github.com/lee-blake/CME-Commitment-to-Change/blob/master/Documentation/Development.md#consider-your-email-backend). If you are using the Docker app, navigate to the main container, and click on the sub-container labeled: "commitment-to-change-app-cme-ctc-mailcapture-1".

![email container](<../Auxiliary Files/Images/User_Images/docker_mailcapture.png>)

   - In the resulting terminal, locate the verification email sent to your newly created account, and click on the verification link at the bottom.

![verify email](<../Auxiliary Files/Images/User_Images/docker-click-link-to-verify-email.png>)
   ***

9. If your verification was successful, you should see the following page:

![verification complete](<../Auxiliary Files/Images/User_Images/account-activation-complete.png>)


### - Logging In
- This page is used for logging into an already registered clinician or provider profile.
- Address for this page: `/accounts/login/`
1. Fill out the fields with the username and password that you used when creating a profile.

![sign_in](<../Auxiliary Files/Images/User_Images/sign_in.PNG>)

- Please note that you can reveal the password as you type it by clicking on the eye icon in the password field.

![Login Show Password](<../Auxiliary Files/Images/User_Images/sign_in_show_password.png>)

2. Press the 'log in' button located underneath these fields.
3. If you were successfully logged in, you will be redirected to your dashboard.
4. If you were not successful, you will be directed to enter a correct username and password.


### - Logging Out
- This button is used to log out the currently logged-in user.
- Must be logged in.
- Address for this page: `/accounts/logout/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Logged in as 'USERNAME'* title followed by a *Log Out* button. Press this button.

![log_out-button.PNG](<../Auxiliary Files/Images/User_Images/log_out_button.PNG>)

3. After pressing *Logout*, you will be brought to the logout confirmation page.

![logout_success.PNG](<../Auxiliary Files/Images/User_Images/logout_success.png>)

4. If this was a mistake, you can log back in using the [Log In](#Logging-in) button.

### - Resetting account password with "Forgot Password"
- This page is used for resetting your account's password if you have forgotten it.
- Address for this page: `accounts/password-reset/`

1. From the [login page](#logging-in), click on the "Forgot your password?" link

![forgot password](<../Auxiliary Files/Images/User_Images/forgot_password_link.png>)

2. Enter the email that you associated your account with [when creating your account](#registering-for-an-account) and click the "Reset Password" button.

![reset enter email](<../Auxiliary Files/Images/User_Images/reset_enter_email.png>)

3. You will be met with the following page:

![reset email sent](<../Auxiliary Files/Images/User_Images/password_reset_email_sent.png>)

4. Navigate to your email or email capture service [as explained in the register verification step](#email-verification) and click on the "Reset your password" link towards the end of the email. The email subject should be something like "Reset your CME Commitment to Change password".
   
5. On the resulting page, enter a new password and re-enter it in the confirmation field. Then click "Confirm Password".
![reset password confirm](<../Auxiliary Files/Images/User_Images/confirm_new_password_page.png>)
6. If your password reset was successful, you will be redirected to the following page:

![reset password complete](<../Auxiliary Files/Images/User_Images/password_reset_complete.png>)
&nbsp;
&nbsp;

---


# Provider Specific Instructions
---

## Dashboard:
- Your dashboard :
   - A Courses section, which contains all courses you have created, their Course ID, start, and end date if added, and an aggregate course statistics download button.
   - A Commitment Templates section, which contains all of the commitment templates you have created.
---
### - Navigating to the Provider Dashboard
- These instructions detail how to get back to the Course Dashboard that most 
provider instructions will reference.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. When logging in as a provider, you will generally be automatically redirected
to the dashboard.
2. If you are on another page, you can click "Dashboard" in the navigation bar 
at the top of the current page.
3. If you prefer, you can instead manually type the url `/app/dashboard` after the address discussed in [Opening the Application](#opening-the-application).
4. You will be redirected to the dashboard, which looks like this:
![Provider Dashboard](<../Auxiliary Files/Images/User_Images/provider_dashboard.png>)

### - Downloading a CSV containing your courses' aggregate statistics
1. [From your dashboard](#Navigating-to-the-Provider-Dashboard), click on the "Download aggregate course statistics" button located under the "Courses" header.
 ![Associated Commitments Section](<../Auxiliary Files/Images/User_Images/download-aggregate-course-statistics-button.png>)
2. The CSV downloaded should contain the following headers:
   - Course Identifier
   - Course Title
   - Start Date
   - End Date
   - Total Commitments
   - Num. In Progress
   - Num. Past Due
   - Num. Completed
   - Num. Discontinued
 ![Course aggregate statistics CSV](<../Auxiliary Files/Images/User_Images/aggregate-course-statistics-csv.png>)

---
## Courses:
- Courses are hubs for you to invite clinicians to. You can set a course description, add a course identifier, start date, and end date, and create "suggested commitment" templates for clinicians to use in your course.
---
### - Creating a Course 
- This page is used to create a course that you can then invite clinicians to join.
- Must be logged-in.
- Address for this page: `/app/course/create/`
1. Click "Create Course" in the navigation bar at the top.

![Provider Dashboard](<../Auxiliary Files/Images/User_Images/provider_create_course.png>)

3. Fill out the title and description of the course. Optionally, you can add a course identifier, a start date, and an end date. The course identifier is NOT unique, and can be used however you please to fit your needs. It is recommended that you choose to make this ID unique across your different courses, so as to more easily identify them, especially when using similar or identical Course Titles.

   ![Provider Create Course](<../Auxiliary Files/Images/User_Images/create_course.png>)

4. When you click submit, you will be taken to the course's view page.

### - Viewing a Created Course 
- This page shows the details for a course.
- Must be logged-in.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the Course Dashboard.
2. In the "Courses" section, locate the button with the name of the course you want to view.
3. Click the button.

![Provider view course](<../Auxiliary Files/Images/User_Images/Provider_view_course.png>)

4. You will be redirected to the course view page, which should look similar  to the following

![Provider Course View](<../Auxiliary Files/Images/User_Images/provider-course-view.png>)

### - Editing a Course
- Must be logged-in.
- Address for this page: `/app/course/<Course id>/edit/`

1. Navigate to your Course's view page [as shown here](#viewing-a-created-course)
2. Click on the "Edit" button at the bottom of the page.

![Edit Course](<../Auxiliary Files/Images/User_Images/edit_course.png>)

3. Adjust the fields as needed and click "Submit".

### - Inviting Clinicians to Your Course 
- This covers inviting clinicians to a course by sharing a link.
- Must be logged-in.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the View Course page for the course.
2. Locate the section with "Share this link to invite students"
   
![Share course link](<../Auxiliary Files/Images/User_Images/provider-share-course-link.png>)

3. Click on the "Copy to Clipboard" button, or manually copy the link.
4. Distribute the link to the clinicians you want to invite to the course.
5. When they go to the link, they will be prompted to log in and automatically
join the course.

### - Viewing Enrolled Student Information
- Must be logged-in.
  
1. Navigate to your course's view page [as shown here](#Navigating-to-the-View-Course-Page).
2. In the "List of Students Enrolled" section, you will find a list of all students enrolled in your course.
3. Click on any name in the list to view their full name, Institution, and user name.
![Enrolled student info](<../Auxiliary Files/Images/User_Images/enrolled_student_info.png>)

### - Sending an email to an enrolled student

1. Navigate to your course's view page [as shown here](#Navigating-to-the-View-Course-Page).
2. In the "List of Students Enrolled" section, click the email icon next to the student you wish to contact to open in your email program of choice.
![Mailto Link](<../Auxiliary Files/Images/User_Images/mailto.png>)


### - Viewing Course Commitments and Status Breakdown
1. [From your course's view page](#Navigating-to-the-View-Course-Page), look for the "Associated Commitments" section. 
2. In the "Status Breakdown" section, you will see a pie chart containing a breakdown of all commitment statuses made in your course.
3. The "Commitments Made in This Course" section contains the names of all commitments created in your course. You can click on the link for each to view the commitment's details.

![Associated Commitments Section](<../Auxiliary Files/Images/User_Images/associated_commitments_section.png>)

### - Downloading a CSV containing your Course's Commitment Statistics 
1. [From your course's view page](#Navigating-to-the-View-Course-Page), navigate to the "Commitments Made In This Course" header. You'll see a "Download Commitments List" button. Click that button to download a CSV file.
 ![Commitments list download](<../Auxiliary Files/Images/User_Images/download-commitments-list-button.png>)
2. This CSV should contain the following headers: 
   - Commitment Title
   - Commitment Description
   - Status
   - Due
   - Owner First Name
   - Owner Last Name
   - Owner Email
![Commitments list CSV](<../Auxiliary Files/Images/User_Images/commitments-list-csv.png>)

---
## Commitment Templates
-  Commitment templates are used to suggest that clinicians in a course make a commitment that you have specified in the template. You can create as many templates as you wish, and you can even use the same templates across multiple of your courses.
---

### - Creating a Commitment Template
- This covers how to create a commitment template that will be used to suggest a commitment to clinicians.
- Must be logged-in.
- Address for this page: `/app/commitment-template/create/`

1. Click "Create Commitment Template" in the navigation bar at the top.

![Provider create commitment template](<../Auxiliary Files/Images/User_Images/provider_create_commitment_template.png>)

2. Fill out the commitment's title and description fields and press "Submit".

![provider template creation page](<../Auxiliary Files/Images/User_Images/create_commitment_template.png>)

### - Associating a Created Commitment Template with a course
- Must be logged-in.

1. Navigate to your course's view page [as shown here](#Navigating-to-the-View-Course-Page).
2. In the "Suggested Commitments" section, click the "Select" button.

![select suggested commitment](<../Auxiliary Files/Images/User_Images/select_suggested_commitment.png>)

3. On the resulting page, select the templates you wish to use in this course, then click "Submit".

![checkbox suggested commitment](<../Auxiliary Files/Images/User_Images/select_commitment_tempalate_check_screen.png>)

4. Your suggested commitment(s) will now appear in your "Suggested Commitments" section for your clinicians to use. You can click on the commitment template name to view and edit it, or click "Select" to add/remove commitment templates. The same Commitment Template may be reused across multiple courses if you so choose. It is recommended to reuse rather than create a new, identical template because this saves effort, reduces dashboard clutter, and allows grouping of statistics.

![suggested commitment list in course view](<../Auxiliary Files/Images/User_Images/suggested_commitment_list.png>)

### - Viewing a commitment template and its aggregate status statistics
1. Navigate to your dashboard [as shown here](#Navigating-to-the-Provider-Dashboard)
2. Click on the commitment template you would like to view
3. If clinicians have created a commitment using this template, a pie chart will appear showing the statuses of all commitments made using that template.
![commitment pie chart](<../Auxiliary Files/Images/User_Images/commitment-template-statistics.png>)

&nbsp;
&nbsp;

---
# Clinician Specific Instructions
---
## Dashboard:
---

### - Navigating to the Clinician Dashboard 
- This button is used to navigate to the logged-in user's commitment dashboard.
- Must be logged-in
- Address for this page: `/app/dashboard/` or `/app/dashboard/clinician/`
1. Locate the navigation bar at the top of the screen
2. There should be a *Dashboard* text that can be clicked. Click this text.

![Nav Bar Dashboard](<../Auxiliary Files/Images/User_Images/clinician_nav_bar_dashboard.PNG>)

3. Alternatively, you can press the *CME Commitment to Change* text.
4. This opens the dashboard.

![Clinician Dashboard](<../Auxiliary Files/Images/User_Images/finalDashboard.png>)


### - Creating A Commitment 
- This button is used to create a new commitment.
- Must be logged in.
- Address for this page: `/app/commitment/make/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Create a Commitment* text that can be clicked. Click this text.
   
![Nav Bar Create](<../Auxiliary Files/Images/User_Images/clinician_nav_bar_create_commitment.PNG>)

3. This opens the commitment creation page. Fill out the title, description, and deadline fields
   and press the *Submit* button underneath the deadline field.
   
![Commitment Create](<../Auxiliary Files/Images/User_Images/commitment_creation.PNG>)

### - Completing A Commitment 
- This button is used to mark a commitment complete.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress* or *Past Due* boxes on the dashboard.
3. Below the title of the commitment, click on the box that says *Complete*.
   
![Complete Button](<../Auxiliary Files/Images/User_Images/commitment_complete_circled.png>)

4. This opens the commitment creation page. Fill out the title, description, and deadline fields
   and press the *Submit* button underneath the deadline field.

![Complete Confirm Button](<../Auxiliary Files/Images/User_Images/commitment-complete-confirm.png>)\

5. The commitment should move from whichever box it was in, into the *Completed* box, 
   and it will be marked as complete.
   
![Completed Commitments](<../Auxiliary Files/Images/User_Images/commitment_complete.PNG>)


### - Deleting A Commitment 
- This button is used to delete a commitment.
- Must be logged-in.
Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress*, *Expired*, *Discontinued*, or *Complete* boxes on the dashboard.
3. Open the edit view for the commitment by clicking on it.
4. Below the commitment details, there should be a button titled *Delete*. Click that button.

![Edit Button](<../Auxiliary Files/Images/User_Images/commitment_delete_circled.PNG>)

5. This brings up a modal asking you to confirm. Click the *DELETE* button to confirm deletion.
   
![Delete Confirm](<../Auxiliary Files/Images/User_Images/commitment_delete.PNG>)


### - Discontinuing a Commitment 
- This button is used to mark a commitment as discontinued indefinitely but not
completed.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress* or *Past-Due* boxes.
3. Below the title of the commitment, click on the box that says *Discontinue*.

![Discontinue Button](<../Auxiliary Files/Images/User_Images/commitment_discontinue_circled.png>)

4. This brings up a modal asking you to confirm. Click the *Discontinue* button to confirm discontinuation.

![Discontinue Confirm Button](<../Auxiliary Files/Images/User_Images/commitment-discontinue-confirm.png>)

5. The commitment should move from whichever box it was in, into the *Discontinued* box,
   and it will be marked as discontinued.
   
![Discontinued](<../Auxiliary Files/Images/User_Images/commitment_discontinued.png>)

6. If this action was a mistake, the commitment can be reopened from here.


### - Reopening Discontinued Commitments 
- This button is used to reactivate a discontinued or completed commitment.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *Discontinued* box.
3. At the bottom of the commitment, click on the box that says *Reopen*.

![reopen discontinued](<../Auxiliary Files/Images/User_Images/discontinued_Reopen.png>)

4. This brings up a modal asking you to confirm. Click the *Reopen* button to confirm.

![reopen Confirm Button](<../Auxiliary Files/Images/User_Images/confirm-reopen.png>)

5. The commitment should move from whichever box it was in, into the *In-Progress* box,
   and it will be marked as in-progress.

&nbsp;
&nbsp;

---
## Commitment Vew Page:
---

### - Navigate to a Commitment Page from the Dashboard 
- Must be logged in to navigate from your dashboard.
- Address for this page: `/app/commitment/<Commitment ID Number>/view/`
1. Locate the navigation bar and go to the commitment dashboard.
2. Locate a commitment in the *In-Progress*, *Past Due*, or *Discontinued* boxes.
   
![View Commitment](<../Auxiliary Files/Images/User_Images/view_commitment_text.PNG>)

3. Click on the text of the commitment.

![Commitment View](<../Auxiliary Files/Images/User_Images/commitment_view.PNG>)

4. This opens the commitment view page.

### - Editing A Commitment 
- This option is used to edit an existing commitment.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Locate a commitment in the *In-Progress*, *Expired*, or *Discontinued* boxes 
on the dashboard.
2. Click on the commitment that you want to edit and open its view page.
3. Below the commitment details, there should be a box labeled *Edit*. Click this box.

![Edit Button](<../Auxiliary Files/Images/User_Images/commitment_edit_circled.PNG>)

4. This brings you to the commitment edit page. Make your edits in these fields.
   - Please note: If the commitment you are editing is from a suggested commitment, you will not be able to edit some fields. Please see the [Making a Course's Suggested Commitment](#making-a-courses-suggested-commitment) for more information.

![Edit View](<../Auxiliary Files/Images/User_Images/commitment_edit_page.PNG>)

5. Below the commitment edit details, press the submit button to save your changes.

### - Sharing a Commitment Page
- Note: Currently, since there is no domain name registered, the link will need
to change `localhost:8000` to `<your ip address>:8000` to be viewable from 
another machine.
- Address for this page: `/app/commitment/<Commitment ID Number>/view/`
1. View one of your owned commitments with the instructions above
2. Copy and paste the URL in the browser.
   
![View Link](<../Auxiliary Files/Images/User_Images/commitment_view_link.PNG>)

3. Share with others. They will be able to see the details of the commitment but
not alter it.
&nbsp;
&nbsp;

---
## Courses:
---
### - Joining a Course 
- This procedure is used to join a course created by a provider.
- Must be logged in.

1. Obtain an invitation link from a provider.
  - It should look something like the link in [Inviting Clinicians to your Course](#inviting-clinicians-to-your-course).
2. Click the link or paste it into your browser.
3. If prompted, log in.
   
![Clinician join course](<../Auxiliary Files/Images/User_Images/clinician_confirm_join_course.png>)

5. You will automatically be enrolled in the course and be taken to that course's page.

### - Viewing a Course 
- This page displays the details of a course you are enrolled in.
- Must be logged in.
- Must be a member of the course.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the Commitment Dashboard.
2. Locate the "My Courses" section. You will see a button with the course's name, as well as the start and end date for the course if applicable.
   
![my course view](<../Auxiliary Files/Images/User_Images/my_courses.png>)

3. Clik on the button with the name of the course you want to view. This will take you to the course page.

![Course View Clinician](<../Auxiliary Files/Images/User_Images/clinician_course_view.png>)

### - Associating a Commitment with a Course 
- Commitments may be optionally associated with a course.
- Must be logged in.
- Must be a member of the course.
- Addresses for this page: `/app/commitment/make/` and 
`/app/commitment/<commitment id>/edit/`
1. Association may be done while making or editing a commitment. Navigate to 
the respective page depending on whether your commitment already exists.
2. In the form, locate the "Associate Course" dropdown menu.
3. In that dropdown menu, select the name of the desired course to associate with.
4. Complete the make/edit process for a commitment as usual.

![Associate commitment](<../Auxiliary Files/Images/User_Images/Associate_commitment_with_course.png>)

### - Disassociating a Commitment with a Course 
- If a commitment is associated in error, this can be reversed.
- Must be logged in.
- Must be a member of the course to reassociate.
- Address for this page: `/app/commitment/<commitment id>/edit/`
1. Edit the commitment.
2. In the "Associated Course" dropdown menu, select "-----" to remove any course
association or the correct course if an incorrect course was selected.

![Selecting "-----"](<../Auxiliary Files/Images/User_Images/commitment_disassociate_course.PNG>)

3. Complete the edit process as usual.

### - Making a Course's Suggested Commitment

1. Navigate to your Course's view page [as shown here](#Viewing-a-Course).
2. In the "Suggested Commitments" section, click the "Make This Commitment" button for the commitment you wish to make.

![Make commitment template](<../Auxiliary Files/Images/User_Images/make_this_commitment.png>)

3. Choose a deadline for your commitment. 
   - Please note: Suggested commitments must retain the same Title, Description, and Associated course fields as the original suggested commitment and as such, you will be unable to edit these fields. This is to ensure that all clinicians who join the same suggested commitment, make the same commitment.

![Make from template](<../Auxiliary Files/Images/User_Images/create_from_template.png>)

4. Your commitment will now show up in that associated [Course's view page](#Viewing-a-Course), as well as [on your dashboard](#Navigating-to-the-Clinician-Dashboard) and functions just like [a normal commitment would](#Creating-A-Commitment)
