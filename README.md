# Tryhackme-Walkthrough #Splunk Investigating(THM)
Investigate anomalies using Splunk.

Alright, fellow tech detectives, today we’re diving into Splunk — to investigate some suspicious anomalies. Whether you’re tracking down a sneaky intruder or just trying to figure out why your server keeps crying at 3 AM, Splunk’s got your back.
Room: https://tryhackme.com/room/investigatingwithsplunk

Answer the questions below:
1. How many events were collected and Ingested in the index main? 🚨
   - First, let’s access to Splunk via your given IP Address.
   - Go to “Apps” → click “Search & Reporting”.
   - Tryhackme is telling you that the index is “main”. Search by typing: <index=main> (note: rmbr to set the filter to “All time”).
   - You should see the number of events under the search bar.
![image](https://github.com/user-attachments/assets/55865c5c-e7d6-4546-a014-2fb884c5c55e)
![image](https://github.com/user-attachments/assets/125ef10f-f9db-464a-8405-7a76f7caaccf)
![image](https://github.com/user-attachments/assets/ffa59be6-87a6-459f-b2bd-4889335b13c2)

Answer: 12 ***

2. On one of the infected hosts, the adversary was successful in creating a backdoor user. What is the new username?
   - We know that Event ID 4720 is for new user. Let’s search this 🔎: <index=main EventID=4720>
   - You will see the Account name for this new account.
![image](https://github.com/user-attachments/assets/91d98b9c-0f3c-4aea-b4ad-a1777d1f6bcd)
![image](https://github.com/user-attachments/assets/ec774710-d65f-4a33-b9f7-22c476092da2)

Answer: Al*****

3. On the same host, a registry key was also updated regarding the new backdoor user. What is the full path of that registry key?
   - You may search through and get the info that registry have 3 ID(s) which are 13, 14, and 15. You may try them.
   - Here, I used <index=main Alberto EventID=13> by reference to a Medium’s Author (Chicken0248). But for me the targetobject is different from this. You may still try it and see.
     
![image](https://github.com/user-attachments/assets/1eca7532-b84a-4640-a7e6-e766a7b42c75)

Answer: HLKM\SAM\SAM\Domains\Account\Users\Names\Alberto

4. Examine the logs and identify the user that the adversary was trying to impersonate.
   - You may directly search the Alberto and inspect the User.
![image](https://github.com/user-attachments/assets/03d3d4ba-8108-4076-b538-f95be4e32c54)
![image](https://github.com/user-attachments/assets/7e6d869d-75e3-4473-b518-28c05d0c4e9a)

Answer: Alberto

5. What is the command used to add a backdoor user from a remote computer?
   - Search index=main Alberto, inspect User and you may see the command.
![image](https://github.com/user-attachments/assets/b2a70232-514d-4fa0-b32b-13c9e990e1e0)

Answer: As in the picture.

6. How many times was the login attempt from the backdoor user observed during the investigation?
   - search the EID 4624 (logon ID) to check the login attempt: <index=main EventID=4624>. 
   - Inspect the Hostname. Unfortunately, I saw Alberto is not on the list so I guess is 0 times login.
![image](https://github.com/user-attachments/assets/2fb3df84-d355-440d-bd5c-86ce8ae2db75)

7. What is the name of the infected host on which suspicious Powershell commands were executed?
   - In question 5, we can clearly see that the one executed this command is “James”.
   - Guess “James” is the infected host.
![image](https://github.com/user-attachments/assets/1fe5118e-71a0-4698-ac96-80ce8f2862f4)

Answer: James.Browne

8. PowerShell logging is enabled on this device. How many events were logged for the malicious PowerShell execution?
   - You may research and see the <index=main EventID=4103> is for powershell.
   - Type in the searchbar: index=main EventID=4103.
   - Under the searchbar you will see the number of events for powershell execution.
![image](https://github.com/user-attachments/assets/b5f813dc-c3e3-44f3-93a3-6835fa922a33)

Answer: 79

9. An encoded Powershell script from the infected host initiated a web request. What is the full URL?
    - Remain with previous search, just click “ContextInfo”, you will see a base64 alphanumeric code here.
    - Copy until ==, as base64 code commonly ends with “==”.
![image](https://github.com/user-attachments/assets/730c24e7-fd27-42ed-a7ef-ff50ffc4b445)

  - Visit to CyberChef websites and select the recipe of “Base64” and “DecodeText”.
  - Paste the data you copied just now and paste to the “input” box, output is given.
![image](https://github.com/user-attachments/assets/955ad0b3-98cc-445a-b75c-fb7ae75de0dc)

  - copy the string, and paste in input.
  - The HTTP URL is given in the output table.
![image](https://github.com/user-attachments/assets/567eef69-32f7-46ec-bfe2-b1d06213c8c6)

 - One more steps to go.
 - copy the URL from the output and add “news.php” behind the URL.
 - Now, this is the URL we want. Copy it and paste in your tryhackme answer box. Congrats everyone!
![image](https://github.com/user-attachments/assets/e7e08726-b3b1-403d-9e79-69985bd7e10d)

Answer: hxxp[://]10[.]10[.]10[.]5/news[.]PHP

Wish You All enjoys the lab!
#DFIR #Splunk #CyberSecurity #HumorInTech

