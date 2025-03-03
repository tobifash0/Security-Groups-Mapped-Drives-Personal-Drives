# Overview: Lab 7 Security Groups, Mapped Drives, Personal Drives
This section of my home lab documentation focuses on managing Security Groups, Mapped Drives, and Personal Drives in a domain environment. The project demonstrates how to create and configure security groups for managing permissions, set up mapped drives for network access, and configure personal drives for user-specific storage.

## Objectives

- Create and configure Security Groups in Active Directory to manage access to resources and network drives.
- Set up Mapped Drives to enable users to access shared resources across the network automatically.
- Configure Personal Drives for individual users to store data securely in the domain environment.
- Implement best practices for permission management using security groups and ensuring appropriate access control for mapped and personal drives.

  ## Documentation
  
In this home lab, we will focus on implementing Security Groups, Mapped Drives, Personal Drives, and Drive Letter Mapping. Let’s start by opening Server Manager on our Windows Server 2022. Then, select File and Storage Services on the left-hand side, followed by Shares. Right-click and select New Share.

<br>

![Screenshot 2025-02-28 at 11 30 26 PM](https://github.com/user-attachments/assets/da3ae51b-87a8-4bc8-b424-e5b7a022cd9d)

<br> 

1. Click Next until you reach the Specify Share Name screen. Name the share HR, then continue selecting Next until you reach the Create button. Click Create to finish setting up the shared folder.

<br>

![image](https://github.com/user-attachments/assets/36c6953e-59c7-4e39-8f51-a3a21a59cc43)

<br> 

2. Repeat the process, but this time name the share Personal. Select Next, then click Create to complete the setup for the second shared folder.

<br> 

![image](https://github.com/user-attachments/assets/57a351cb-c485-4106-b40b-599c20e21d65)

<br> 

3. Now that we have our shared folders, open File Explorer → This PC → Local C Drive → Shares to access the shared folders.

<br>

![image](https://github.com/user-attachments/assets/768db1ff-330d-4715-a766-69100fafdafd)

<br> 

4. Now, go to Active Directory Users and Computers → right-click on Users → select New → then click Group to create a new security group.

<br> 

![Screenshot 2025-02-28 at 11 34 18 PM](https://github.com/user-attachments/assets/5f21c36a-7f77-4d1c-b040-eb84d1cf3484)

<br> 

5. Name the group name “HR”.

<br> 

<img width="674" alt="Screenshot 2025-03-01 at 12 37 27 AM" src="https://github.com/user-attachments/assets/b307c9be-02ca-4a98-ae76-e1c1350cb87c" />

<br> 

6. Now lets double click on “HR” → select “Managed By” → “Change” then enter “Helpdesk”.

<br> 

![Screenshot 2025-02-28 at 11 37 22 PM](https://github.com/user-attachments/assets/0950807f-a19b-42f7-b2cf-577489c1ef11)

<br> 

7. We will create another group the same way and call it “Personal” and have it managed by Helpdesk as well.

<br>

![Screenshot 2025-02-28 at 11 44 25 PM](https://github.com/user-attachments/assets/46fe31ab-d438-435f-83c1-221d6170acba)

<br> 

8. Now, go back to the shared folders. Right-click on Personal → select Properties, then navigate to the Sharing tab. Highlight the path \SERVER2022\Personal, right-click, and select Copy. 
<br> 

![image](https://github.com/user-attachments/assets/efb21991-04de-4889-9dea-1198ff89a2b5)

<br> 

9. Then, paste this path into the Description field of the Personal properties in Active Directory Users and Computers.


![Screenshot 2025-02-28 at 11 49 20 PM](https://github.com/user-attachments/assets/5a2c7986-7e00-4f47-9114-2f38125d44db)

<br> 

10. Repeat the process for the HR share folder. Once that’s done, open the HR group in Active Directory Users and Computers and click on the Members tab. Select Add, then search for and add Bob to the group.

<br> 

![Screenshot 2025-02-28 at 11 53 12 PM](https://github.com/user-attachments/assets/166a38ea-5d76-4695-b5b0-ec3dc62e05bc)

<br> 

11. Repeat the process for the Personal share folder. Open the Personal group in Active Directory Users and Computers, click on the Members tab, select Add, and then add Bob to the group.

<br> 

![Screenshot 2025-02-28 at 11 54 52 PM](https://github.com/user-attachments/assets/8726200b-b8a3-46b3-8a61-038bd307e4f5)

<br> 


12. To verify, select the HR organizational unit in the domain, then double-click on Bob. Next, go to the Member Of tab to confirm that Bob is a member of the HR group.

<br> 

![Screenshot 2025-02-28 at 11 56 58 PM](https://github.com/user-attachments/assets/32b4fb44-575f-404f-a706-dc26dd7db4a0)

<br>

13. Now, we will focus on configuring the correct permissions. To do this, navigate to the Personal share folder, right-click on it, and select Properties. In the Security tab, click on Advanced, then select Disable Inheritance.

<br> 

![Screenshot 2025-02-28 at 11 58 25 PM](https://github.com/user-attachments/assets/39d77704-f416-4a42-a4b0-14337f668e3e)

<br> 

14. Select the first option “Covert inherited permissions…”

<br>

![image](https://github.com/user-attachments/assets/9c5ee87b-cb50-48ba-a940-892beecba61e)

<br> 

15. Now remove both “Users”. This removes any users who do not have access to this personal folder.

<br>

![Screenshot 2025-02-28 at 11 59 02 PM](https://github.com/user-attachments/assets/bb94ac99-336a-4aa7-8d93-9601e19684c8)

<br>

16. Click Add, then select Select a principal. Add the Helpdesk group and assign the Modify permission under the basic permissions section.

<br> 

![Screenshot 2025-03-01 at 12 00 14 AM](https://github.com/user-attachments/assets/0c67f9d8-9d17-4bba-96ae-479563dd8403)

<br> 

17. Repeat the process and add the Personal group, ensuring the Modify permission is enabled under the basic permissions section.

<br> 

![Screenshot 2025-03-01 at 12 06 08 AM](https://github.com/user-attachments/assets/0ba22024-c5d3-4f8f-a624-237c4ae6badd)

<br>

18. Now, in the Personal folder properties, navigate to the Sharing tab → select Share... → right-click on Personal → choose Read/Write, then click Share.

<br> 

![image](https://github.com/user-attachments/assets/64d4dda1-d6f6-435f-9368-a63f97d8e08c)

<br> 

19. Now, repeat the process on the HR folder:
    

- Right-click on HR → select the Security tab → click Advanced.

- Select Disable Inheritance → choose Convert inherited permissions....

- Delete the two Users permissions.

- Click Add, then Select a Principal, and add Helpdesk.

- Enable Modify for basic permissions.

- Click OK, then Apply.

<br> 

![Screenshot 2025-03-01 at 12 09 17 AM](https://github.com/user-attachments/assets/426f3bd3-ed8a-4df7-a624-35cbf5df6b3b)


<br> 

20. To ensure the HR group can "Read/Write" in the sharing properties, follow these steps:


-  Right-click on the HR folder.

- Select Properties and go to the Sharing tab.
   
- Click Share….
   
- In the Network Access window, ensure HR is listed.
   
- Right-click on HR and select Read/Write.
    
-  Click Share to confirm the settings.
    
   <br>
This ensures that members of the HR group have the correct permissions to both read and write to the HR shared folder.

   <br>

   ![image](https://github.com/user-attachments/assets/63dacc13-7cc6-470b-808c-9e816e857b5d)

<br>

21. o check Bob's access to the HR folder on Desktop2:
    

- Log in as Bob on the Desktop2 account.
-  Open File Explorer.
-   In the File Explorer search bar, paste the following network path:\\Server2022\HR
-  Pess Enter to navigate to the HR shared folder.
<br>
Since Bob is part of the HR group, he should have access to this folder. You should be able to see the contents of the HR folder. If you followed the permissions setup correctly, Bob should have Read/Write access to this folder.

<br>

![image](https://github.com/user-attachments/assets/62968c8e-4a97-4dec-9384-a36878c45e5c)

<br>

22.

- Copy the network path for the HR folder: \Server2022\HR
- Right-click on This PC in File Explorer and select Map this Network drive.
- In the Map Network Drive window:
  <br>
  - Drive letter: Choose a drive letter, such as Z:
- Folder: Paste the network path \Server2022\HR into the folder field.

- Check the box for Reconnect at sign-in if you want the drive to be remapped automatically on login.
- Click Finish.

<br> 

![image](https://github.com/user-attachments/assets/e4b7a50c-4608-488e-ae41-c7d71f966f2b)

<br>

23. <br> 

![image](https://github.com/user-attachments/assets/2bead10b-f88d-4c90-9ac6-ccad9a7d01c8)

<br>

24. Another method to map a personal drive is by accessing your Windows Server 2022 account, copying the network path from the "Personal Properties" section in the shared folders.

<br> 

![image](https://github.com/user-attachments/assets/3462175a-c940-42a0-8e7f-0abb8d073e94)

<br> 

25. Next, open Active Directory Users and Computers, search for "Bob," right-click on his name, and select "Properties." Then, go to the "Profile" tab and under "Home Folder," choose "Connect" and set the drive letter to P:. Paste the network path for the drive: \SERVER2022\Personal%username% (make sure to include "%username%"). Finally, click "Apply." This will create a personal folder within Bob's directory.

<br> 

![image](https://github.com/user-attachments/assets/90fa7671-3a96-40c7-a608-b74819853a43)

<br> 

26. Once we log into Desktop2 as Bob, we will see that both the Personal and HR drives are mapped.

<br> 

![image](https://github.com/user-attachments/assets/c958d944-a281-4b22-996e-6747c441d797)

<br> 

Congratulations we have successfully configured on how to implement Security Groups, Map Drives, Personal Drives and Map Letter.

👉 [Next Lab 8 : Windows 10 Remote Access: Remote Desktop, Remote Registry](https://github.com/tobifash0/Windows-10-Remote-Access-RemotDesktop-Remote-Registry)
