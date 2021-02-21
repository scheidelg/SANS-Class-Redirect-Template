**Create OneNote Notebook, Domain, and Redirect**

1. Assign:

    - a name for the class OneNote notebook that is fairly simple and easy to remember
    - a corresponding FQDN as a subdomain of scheidel.net
    - a corresponding GitHub repository name

   We're looking for a OneNote notebook name that's easy for students to remember and closely associated with the event, with a matching FQDN that is easy to remember, short, and easy to type.

   The GitHub repository name should be similar to the FQDN but this isn't too important since students won't generally see it.

   For example, for SEC530 at the SANS Cyber Architecture in the United Arab Emirates (AE) I picked:

    - a OneNote notebook name of `SEC530 - CA 2020 AE`
    - an FQDN of `ca2020ae.scheidel.net`
    - a GitHub repository name of `SEC530-CA-2020-AE`

2. Create a OneNote notebook with the assigned name.

    - Open OneDrive
    - Browse to the folder containing class OneNote notebooks
    - Copy the template to a new notbook

3. Enable sharing for editing, and get the sharable URL.

   Note: For the time being we're trying to avoid using a shared editing password. We might have to staring using passwords if there are ever problems with people maliciously mucking with the notebook.

    - Browse to the notebook via OneDrive
    - Right-click on the notebook and select **Details** from the context menu to activate the details pane
    - In the details pane, under *Has access* you should see "This item is not shared"
    - In the details pane, under *Has access*, click on **Manage access** to activate the *Manage Access* pane
    - In the *Manage Access* pane, in the top-left corner, click on **Share** to activate the *Send link* dialog
    - Click on **Anyone with the link can edit** to activate the *Link settings* dialog
    - Set an expiration date (a few weeks after the class) and click **Apply** to return to the *Send link* dialog
    
      **If you set an expiration date, then you'll need to also create a 'view' link and -  ahead of the edit link's expiration date - update this repository's `index.html` file to redirect to the view link.** Otherwise somebody browsing to the \<DN\>.scheidel.net URL will be denied access.
    - Click on **Copy link** to get a shareable link; copy to clipboard; save in a scratchpad so you don't lose it
    - Close the dialog
    - Close the *Manage Access* pane
    - In the details pane, under *Has access*, click on **Manage access** to activate the *Manage access* pane
    - Confirm that the new sharing link has been created
       - "Anyone with this link can edit this item"
       - Correct expiration date; if incorrect (which sometimes happens with this interface - not your fault), then update and save, and come back in again to double-check; wash-rinse-repeat until the correct date is set

4. Enable sharing for viewing, and get the sharable URL.

    - Browse to the notebook via OneDrive
    - Right-click on the notebook and select **Details** from the context menu to activate the details pane
    - In the details pane, under *Has access*, click on **Manage access** to activate the *Manage Access* pane
    - In the *Manage Access* pane, in the top-left corner, click on **Share** to activate the *Send link* dialog
    - Click on **Anyone with the link can edit** to activate the *Link settings* dialog
    - Uncheck the **Allow editing** checkbox and click **Apply** to return to the *Send link* dialog
    - On the *Send link* dialog, you should see"Anyone with the link can view"
    - Click on **Copy link** to get a shareable link; copy to clipboard; save in a scratchpad so you don't lose it
    - Close the dialog
    - Close the *Manage Access* pane
    - In the details pane, under *Has access*, click on **Manage access** to activate the *Manage access* pane
    - Confirm that the new sharing link has been created
       - "Anyone with this link can fiew this item"
       - No expiration date

5. Create a new GitHub repository with an index.html file.

     - Open GitHub
     - Create a new GitHub repository with the assigned GitHub repository name
     - Click on **creating a new file** to open the GitHub file editor
     - Name the file 'index.html' and paste in content:

           <!-- Redirect to the OneNote page for this class -->
           <!-- If the 'edit' has an expiration date, then remember to come back just ahead of the expiration date and update this file to use the 'view' link -->
           <!-- Editing link: https://1drv.ms/o/s!AmX2EQD23qhmhyvAK-oicNNrOyFv -->
           <!-- Viewing link: https://1drv.ms/o/s!AmX2EQD23qhmhys5lJ-iwh-WXBU- -->
           <!DOCTYPE html>
           <html>
             <head>
               <!-- edit this HTML to use the correct link -->
               <meta http-equiv="Refresh" content="0; url=https://1drv.ms/o/s!AmX2EQD23qhmhyvAK-oicNNrOyFv" />
             </head>
             <body>
               <!-- edit this HTML to use the correct link, class name, and event name -->
               <p>Redirecting to <a href="https://1drv.ms/o/s!AmX2EQD23qhmhyvAK-oicNNrOyFv">the OneNote page</a> for SEC530 at SANS South by Southeast Asia 2021.</p>
             </body>
           </html>

     - Edit the content:
        - Replace the URL in the 'edit link' comment with the edit link for the OneNote notebook
        - Replace the URL in the HTTP redirect with the edit link for the OneNote notebook
        - Replace the URL in the HREF with the edit link for the OneNote notebook
        - Replace the URL in the 'view link' comment with the view link for the OneNote notebook
        - Replace the class name with the correct class name
        - Replace the event name with the correct event name

     - Click on **Commit new file**

6. Enable GitHub Pages

     - Click on **Settings**
     - Scroll down to the **GitHub Pages** section
     - Change the GitHub Pages **Source** setting to the main branch; click **Save**
     - Change the GitHub Pages **Custom domain** setting to the assigned FQDN; click **Save**
     - Return to the repository file listing and make sure that a CNAME file was created (yes, we could just manually create the CNAME file instead of using the **Custom domain** text box; same end result)

7. Login to GoDaddy and create a CNAME record that redirects to the GitHub repository's GitHub Pages web page.
 
     - **Manage My Products**
     - Under the list of domains, find `scheidel.net`
     - To the right of **scheidel.net**, click on **DNS**
     - Click **ADD** to add a new DNS record

| Type | Host | Points to | TTL |
| :--- | :--- | :--- | :--- |
| CNAME | (base name within `scheidel.net`) | scheidelg.github.io | 600 seconds |

   Note: This assumes that we already have the A records created for the apex domain (i.e., `scheidel.net`) to resolve to the GitHub Pages IP addresses:

| Type | Name | Value | TTL |
| :--- | :--- | :--- | :--- |
| A | @ | 185.199.108.153 | 1 week |
| A | @ | 185.199.109.153 | 1 week |
| A | @ | 185.199.110.153 | 1 week |
| A | @ | 185.199.111.153 | 1 week |

8. Browse to \<DN\>.scheidel.net and confirm it redirects to the correct OneNote notebook.

   If it doesn't work right away, then go get a refreshing beverage and come back in 10 minutes. It can take a few minutes for the GitHub pages to be ready.

9. After successfully testing, change the TTL on GoDaddy to 1 week.

10. Go back to the GitHub repository settings and enable 'Enforce HTTPS'.

    If the option is "not yet available for your site because the certificate has not finished being issued," then try again in a few hours.  GitHub says "please allow 24 hours"; it's usually much less than that.

11. Browse to http:\/\/\<DN\>.scheidel.net and confirm it redirects to https:\/\/\<DN\>.scheidel.net and the correct OneNote notebook.

**Setup Initial OneNote Notebook Pages**

Refer to the notes in the OneNote template notebook for customizing and updating for this class.
