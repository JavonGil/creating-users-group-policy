<p align="center">
<img width="450" height="250" alt="Microsoft Active Directory Logo" src="https://github.com/user-attachments/assets/cd75c7f5-fba1-4682-a616-dc487e761fbc"
 alt="Microsoft Active Directory Logo"/>
</p>

<h1>Creating Users and Group Policy for Active Directory</h1>
This tutorial outlines creating a User Database and Group Policy Objects for Active Directory within Azure Virtual Machines.<br />

<h2>Prerequisite</h2>

- [Create Active Directory Infrastructure in Azure](https://github.com/JavonGil/Creating-ad-infrastructure)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Wndows App (for macOS)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- macOS Sequoia
- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Section 1: Create User Database
- Section 2: Group Policy Objects 

<h2>Deployment and Configuration Steps</h2>

<h3>Section 1: Create User Database</h3>
<p>
<img width="600" height="500" alt="CU1" src="https://github.com/user-attachments/assets/78ca0b79-47d2-4c1a-8c41-a143b8680c6d" />
</p>

<p>
- Login into DC-1 via Remote Desktop using the jane_admin account. (mydomain.com\jane_admin and password)
<p>- From the Start Menu, type PowerShell in the Search Bar, right-click Windows PowerShell ISE, and Run as Admin.</p>
<br />

<p>
<img width="750" alt="CU2" src="https://github.com/user-attachments/assets/ab10520f-6366-401e-bdd2-576e982c1efd" />
<br />

- Click here --> [SCRIPT](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) to copy the file we need for the User database as seen in Figure 2.

<p>- Select the icon next to Raw in the top right corner. Copy raw file and go back to PowerShell ISE.</p>
<br />

<p>
<img width="750" alt="CU3" src="https://github.com/user-attachments/assets/9dd1f6f1-366a-41fb-9293-069c852967d7" />
</p>

<p>- 1. Click the blank page to Create a new file.</p>
<p>- 2. Paste the Script .</p>
<p>- 3. Click the Play button to Run the Script.</p>
<br />

<p>
<img width="750" alt="CU4" src="https://github.com/user-attachments/assets/3a74ba58-8578-438a-80f9-7d68d63c1843" />
</p>

<p>- While the thousands of users are being created, take a quick note of the password in the 2nd line of the script. This password is for all the users we are adding. We will need this when we attempt to login as one of the new users.</p>
<br />

<p>
<img width="750" alt="CU5" src="https://github.com/user-attachments/assets/b87b5323-61dd-4174-af96-995018e43893" />
</p>

<p>- We should have enough users by now to attempt to login on Client-1 with their credentials.</p>
<p>- Let the script keep running and head to the Start Menu. From here, navigate to Avctive Directory Users and Computers.</p>
<p>- Click OK and select the _EMPLOYEES folder to check out all the users created so far.</p>
<br />

<p>
<img width="750" alt="CU6" src="https://github.com/user-attachments/assets/f2ffba9f-88ac-4ca6-b7ab-aa5003c059e5" />
</p>

<p>- Choose a random Username you like and let's use it to login to Client-1.</p>
<p>- I chose bat.raj because... Why not? 😂</p>
<br />

<p>
<img width="750" alt="CU7" src="https://github.com/user-attachments/assets/192c3116-8252-438c-903b-a4067a1cce80" />
</p>

<p>- Now we will attempt to login to Client-1 with the new user you chose.</p>
<p>- Do not forget to specify domain in username. </p>
<p>- mydomain.com\bat.raj and Password1. (mydomain.com\username and Password1) </p>
<p>- Did it work? bat.raj had zero issues logging in. 😉 </p>
<br />

<h3>Section 2: Group Policy Objects</h3>

<p>
<img width="600" alt="GP2" src="https://github.com/user-attachments/assets/d6583ac0-b04e-496f-b2ff-0ada114649c7" />
</p>

<p>- Log into DC-1 using jane_admin. (mydomain.com\jane_admin)</p>
<p>- Once logged in, right-click the Start Menu and select Run.</p>
<p>- Type in gpmc.msc and click OK.</p>
<br />

<p>
<img width="750" alt="GP3" src="https://github.com/user-attachments/assets/62ddd1e6-4715-4a35-960a-b116522a93d4" />
</p>

<p>- Under mydomain.com, right-click Default Domain Policy and select Edit. See Figure 2.</p>
<p>- This will open the Group Policy Management Editor.</p>
<br />


<p>
<img width="900" alt="GP4" src="https://github.com/user-attachments/assets/84693f7b-2243-42ab-8834-ea704aa31074" />
</p>

<p>- We will need to expand a couple things to find the right path. Here we go. See Figure 3</p>
<p>- In Group Policy Management Editor -> Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Policies.</p>
<p>- Now, open Account Lockout Policy.</p>
<br />

<p>
<img width="900" alt="GP6" src="https://github.com/user-attachments/assets/6cd2af20-a548-4ac7-9645-11bad27e19c8" />
</p>

<p>- Open Account lockout durtion Properties. Check the box by Define the policy, set for 30 minutes, and click Apply and OK. </p>
<br />

<p>
<img width="900" alt="GP7" src="https://github.com/user-attachments/assets/44552a31-91f1-42e5-ac6c-a4881d0ebca0" />
</p>

<p>- Notice the Suggested Value Changes based off our lockout duration. </p>
<p>- We want this, so simply click OK. </p>
<br />

<p>
<img width="900" alt="GP8" src="https://github.com/user-attachments/assets/4f6d968b-2ba2-438a-b546-e4d0da50014a" />
</p>

<p>- We can confirm the details of our updated Account Lockout Policy here. </p>
<p>- I think this takes almost 90 minutes to take effect, but we are not waiting that long because we got stuff to do. </p>
<p>- Next, we will force update the policy so the changes take effect now.</p>
<br />

<p>
<img width="750" alt="GP9" src="https://github.com/user-attachments/assets/b558ed54-2f8b-4174-8b17-32d5502f48bb" />
</p>

<p>- Jump over to Client-1 and log in as jane_admin. (mydomain.com\jane_admin) </p>
<p>- Open Command Prompt, enter the command gpupdate /force  and press enter.</p>
<p>- Once the force update is complete, log out of Client-1.</p>
<br />

<p>
<img width="550" alt="GP10" src="https://github.com/user-attachments/assets/c3be8dc3-5884-412e-8f8f-d09bdcd2a2ee" />
</p>

<p>- Now, we are going to log into Client-1 as another user within the domain but with the wrong password. </p>
<p>- Attempt 6 logins with the wrong password and see what happens.</p>
<p>- YOU SHALL NOT PASS! 🧙🏽‍♂️</p>
<br />

<p>
<img width="750" alt="GP11" src="https://github.com/user-attachments/assets/b54b14ec-de92-45e6-9bed-ffe1893c9e78" />
</p>

<p>- Lets get back on DC-1 as jane_admin (mydomain.com\jane_admin) and navigate to Active Directory Users and Computers.</p>
<p>- We need to find the user (jus.pob) that we just locked out and unlock their account. You can open _EMPLOYEES and scroll for days, depending on what the username is, or right-click mydomain.com and select Find.</p>
<p>- This will be a lot faster.</p>
<br />

<p>
<img width="750" alt="GP13" src="https://github.com/user-attachments/assets/88bce577-435f-4c5a-bbd0-06c57c3b2cf3" />
</p>

<p>- Enter the username and click Find Now. (jus.pob is who I'm looking for).</p>
<p>- Click on the username when it appears in the Search results below. Under the Account tab we will find that the user's account is Locked out of the AD Domain Controller as shown in Figure 10.</p>
<p>- Check the box next to Unlock account, click Apply, and then OK.</p>
<br />

<p>
<img width="750" alt="GP13 1" src="https://github.com/user-attachments/assets/d21d27bf-60c2-4c6c-9de7-8c33b6756f5e" />
</p>

<p>- Now that the account has been unlocked, try log back into Client-1 as that same user. (mydomain.com\jus.pob)</p>
<p>- You will know right a way if it worked or not. I went to PowerShell after logging on and entered "whoami". See figure 11.😆  </p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="GP14" src="https://github.com/user-attachments/assets/67b863ca-28f6-4b05-8e9e-cf7904863144" />
    </td>
    <td>
      <img width="1000" alt="GP15" src="https://github.com/user-attachments/assets/82732951-dcda-47e3-b783-e585b4be4803" />
    </td>
  </tr>
</table>
<p>
 - We can do a bunch of stuff with the user accounts in Active Directory Users and Computers. We can disable accounts if needed. Although that might be more of a HR thing, but you never know.</p> 
<p>- You can disable the username that we just unlocked or pick one you don't like and vote them off the domain. 🤣</p>
<p>- Then, try to log into Client-1 as the exiled user and see what happens.
<p>- Figure 12 shows the long way to find the user and Figure 13 shows the express lane.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="GP16" src="https://github.com/user-attachments/assets/731c7e88-3356-4bdd-baf5-9c41ea9a7659" />
    </td>
    <td>
      <img width="1000" alt="GP17" src="https://github.com/user-attachments/assets/5a349fb3-fb8d-4b41-a61c-eeafe64a9705" />
    </td>
  </tr>
</table>
<p>
 - We can also reset the password if needed. For example, during the account lockout scenario earlier, when we unlocked the account we would have reset the password and then had the user create a new password for security reasons. </p> 
<p>- Same as before, Figure 14 shows the long way to find the user and Figure 15 shows the express lane.</p>
<br />

<p>
<img width="750" alt="GP18" src="https://github.com/user-attachments/assets/8e309698-4ff9-4e39-9a2e-897e4a4d46d0" />
</p>

<p>- One last thing before we end this project. Log into Client-1 as jane_admin (mydomain.com\jane_admin) </p>
<p>- From the Start Menu, search eventvwr.msc and Open as Admin. </p>
<p>- This will take us to the Event Viewer and allow us to look at Security Logs.</p>
<p>- Expand Window Logs -> right-click Security -> click Find. Type in the username that was locked out earlier. (jus.pob)</p>
<p>- We can view the logs and see how many log in attempts the user made with timestamps.</p>
<br />

<h2>Conclusion</h2>

<p>That’s a wrap on this project. We added a whole batch of users to our domain and set up some essential Group Policy Objects to manage how things work across the network. Acting as a Domain Admin gave us a real taste of what it’s like to run the show in a Windows Server environment and honestly, we’ve only just scratched the surface of what Active Directory can do. From centralized user management to enforcing policies across machines, this is where IT starts to feel powerful. Make sure to stop your VMs in Azure to avoid burning through resources. Big thanks for locking in and exploring the lab. Catch you in the next one 😎     
</p>
<br />
