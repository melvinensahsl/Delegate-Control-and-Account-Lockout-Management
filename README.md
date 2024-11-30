<h2>Overview: Lab 14 Delegate Control and Account Lockout Management</h2>

This repository documents the setup and configuration of a home lab environment dedicated to studying "Delegate Control and Account Lockout Management." The focus of this lab is to explore best practices for managing user permissions and account lockout policies in an Active Directory (AD) environment. 

<h1>Objectives</h1>

- **Delegate Control**: Implementing and testing delegation of administrative privileges in an AD environment to different users or groups, ensuring least privilege access.
- **Account Lockout Management**: Configuring and testing account lockout policies to secure accounts from brute-force attacks while ensuring proper exception handling.



<h1>Documentation</h1> 

In this home lab, we will focus on understanding **Delegation Control** and **Account Lockout**. Delegation involves granting a user limited access through **Active Directory**. To begin, we will create a new user in **Active Directory Users and Computers** on our **Windows Server 2022 VM**.




1. <p align="center">
   <img src="https://i.imgur.com/EvUqa8d.png" height="80%" width="80%" alt="Disk Sanitization Steps 1"/>
   <br />
   <br />
</p>

We will create a user named Andrew for both the First and Last Name, and his login username will also be Andrew.

2. <p align="center">
   <img src="https://i.imgur.com/7N7rkGz.png" height="80%" width="80%" alt="Disk Sanitization Steps 2"/>
   <br />
   <br />
</p>

After creating the user Andrew, we will create a new Organizational Unit (OU). Right-click on the domain SimoTech.com, select New → Organizational Unit, and name it Consultants. Then, drag Andrew into the newly created Consultants OU and click Yes to confirm.

3. <p align="center">
   <img src="https://i.imgur.com/7zePSxs.png" height="80%" width="80%" alt="Disk Sanitization Steps 3"/>
   <br />
   <br />
</p>

Next right click on the domain SimoTech.com and select “Delegate Control”

4. <p align="center">
   <img src="https://i.imgur.com/6eNrMfO.png" height="80%" width="80%" alt="Disk Sanitization Steps 4"/>
   <br />
   <br />
</p>

Then add “Andrew”. 

5. <p align="center">
   <img src="https://i.imgur.com/31Vhyof.png" height="80%" width="80%" alt="Disk Sanitization Steps 5"/>
   <br />
   <br />
</p>

Will only give Andrew the permission to reset passwords for other users. Check mark “Reset user passwords and force password change at next logon”. Then select “Next” then “Finish”.

6. <p align="center">
   <img src="https://i.imgur.com/uy0ysxv.png" height="80%" width="80%" alt="Disk Sanitization Steps 6"/>
   <br />
   <br />
</p>

Now that the setup is complete, let's log in as Andrew on our Windows 10 VM. Open Active Directory Users and Computers. To verify the actions available to Andrew, search for the user Bob, right-click on his account, and select Properties. Then, go to the Account tab. Under Account options, you'll notice that everything is grayed out except for the option User must change password at next logon.

7. <p align="center">
   <img src="https://i.imgur.com/qFd5Uvj.png" height="80%" width="80%" alt="Disk Sanitization Steps 7"/>
   <br />
   <br />
</p>


To verify further, let's right-click on **Bob** and select **Reset Password**. This will prompt us to reset Bob's password.

Next, let's lock out **Andrew's** account. Use the **Input** button at the top of the VM, select **Keyboard** → **Insert Alt + Ctrl + Del**, then choose **Lock**. This will intentionally lock **Andrew's** account.

8. <p align="center">
   <img src="https://i.imgur.com/XwAn3NH.png" height="80%" width="80%" alt="Disk Sanitization Steps 8"/>
   <br />
   <br />
</p>

To investigate a user account that has been locked out, we can use a tool from Microsoft called the Account Lockout and Management Tools. We can download it from Microsoft’s website at this link. After downloading, we’ll move the file into our SimoTech Lab folder, which is shared with our Windows Server 2022 VM.


9. <p align="center">
   <img src="https://i.imgur.com/LEj1vK9.png" height="80%" width="80%" alt="Disk Sanitization Steps 9"/>
   <br />
   <br />
</p>

Next, we need to enable shared folders on our Windows Server 2022 VM. Right-click on the folder icon at the bottom and select Share Folder Settings. For the Folder Path, locate the SimoTech Lab folder in our Downloads directory. Check the box for Auto-mount and click OK.


10. <p align="center">
    <img src="https://i.imgur.com/UeQUpkd.png" height="80%" width="80%" alt="Disk Sanitization Steps 10"/>
    <br />
    <br />
</p>

The SimoTech Lab folder should now appear as our Z: drive. Open the Z: drive, then locate and open the Account Lockout and Management Tools application. Run the tool to begin the investigation.


11. <p align="center">
    <img src="https://i.imgur.com/Vvw2SFL.png" height="80%" width="80%" alt="Disk Sanitization Steps 11"/>
    <br />
    <br />
</p>

For extraction location, choose the Documents and select “OK”.


12. <p align="center">
    <img src="https://i.imgur.com/gCaacXC.png" height="80%" width="80%" alt="Disk Sanitization Steps 12"/>
    <br />
    <br />
</p>

In Documents, open the LockoutStatus application. This tool is designed to analyze and manage account lockouts in Active Directory environments. It's especially useful in large or complex networks where account lockouts may be caused by issues such as misconfigured applications, password synchronization problems, or unauthorized access attempts.


13. <p align="center">
    <img src="https://i.imgur.com/FNh598c.png" height="80%" width="80%" alt="Disk Sanitization Steps 13"/>
    <br />
    <br />
</p>

Navigate to File in the top-left corner and select Select Target. Enter Andrew as the target user and click OK. This will display the User State, which shows that the account is currently locked due to 4 bad password attempts. It also provides key details, including the time of the last password attempt, the date the password was last set, the domain or origin of the lockout, and the lockout timestamp.


14. <p align="center">
    <img src="https://i.imgur.com/8cynxOx.png" height="80%" width="80%" alt="Disk Sanitization Steps 14"/>
    <br />
    <br />
</p>



15. <p align="center">
    <img src="https://i.imgur.com/vFe3kXQ.png" height="80%" width="80%" alt="Disk Sanitization Steps 15"/>
    <br />
    <br />
</p>

Now that we’ve confirmed **Andrew’s** account is locked, we can fix it by following these steps:

1. Open **Active Directory Users and Computers**.
2. Search for **Andrew** in the **Consultants** organizational unit (OU).
3. Right-click on **Andrew** and select **Properties**.
4. Go to the **Account** tab and check the box for **Unlock account**.
5. Click **Apply** to unlock the account.

16. <p align="center">
    <img src="https://i.imgur.com/rDrfn0n.png" height="80%" width="80%" alt="Disk Sanitization Steps 16"/>
    <br />
    <br />
</p>

Now we can have Andrew sign back into his account. 

17. <p align="center">
    <img src="https://i.imgur.com/NBOmB4q.png" height="80%" width="80%" alt="Disk Sanitization Steps 17"/>
    <br />
    <br />
</p>



18. <p align="center">
    <img src="https://i.imgur.com/LDi6ybY.png" height="80%" width="80%" alt="Disk Sanitization Steps 18"/>
    <br />
    <br />
</p>

If we run the Bobby application again and search for Andrew, the results will show that the account is no longer locked.

19. <p align="center">
    <img src="https://i.imgur.com/YbVJPrV.png" height="80%" width="80%" alt="Disk Sanitization Steps 19"/>
    <br />
    <br />
</p>



Congratulations! We have successfully completed the final home lab, gaining a thorough understanding of Delegation Control and how to investigate an account lockout using Microsoft’s Account Lockout and Management Tools.
