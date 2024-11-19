# Lets-Defend-Incident-Response-4
SOC168 - Whoami Command Detected in Request Body

**Summary:**

In this Incident I responded to an alert triggered by "Request Body Contains whoami string". After locating the whoami command and others inside the endpoint affected (WebServer 1004). Looking through filtered logs confirmed the commands injected were succeful. Server was immediatly isolated, and incident was escalated. 

**Incident Response:**

Start by creating a case and taking ownership.

Then starting a playbook.

<img width="557" alt="Screenshot 2024-11-19 140400" src="https://github.com/user-attachments/assets/4590ddd0-8954-4ad1-8188-a2214e7df445">

Looking at the information provided.

<img width="704" alt="Screenshot 2024-11-19 140449" src="https://github.com/user-attachments/assets/207be456-44f2-4453-95b2-15159a2dc80a">
.
Now I can start investigating.

The alert was triggered due to "Request Body Contains whoami string".

Request URL: https://172.16.17.16/video/

Looking up the source IP in VirusTotal and Cisco Talo shows this IP has been proven to be malicous.

<img width="926" alt="Screenshot 2024-11-19 141229" src="https://github.com/user-attachments/assets/33f590c2-ad63-4559-a769-1bf7396d6407">

<img width="915" alt="Screenshot 2024-11-19 141246" src="https://github.com/user-attachments/assets/214c67cc-1fe7-43a8-a392-ee4812a9f37b">

Next I am wanting to go to the provided WebServer1004 to investigate any commands given.

Inside Endpoint Security tab > select WebServer1004 > Terminal History 

Looking through this server I found some suspicous commands from a different source.

<img width="471" alt="Screenshot 2024-11-19 141507" src="https://github.com/user-attachments/assets/abb1685b-006b-465c-a18f-060da48ca9dd">

Now that I have located the whoami command, and noticed there completed. I am going to filter the logs from the source IP: 61.177.172.87

<img width="922" alt="Screenshot 2024-11-19 141744" src="https://github.com/user-attachments/assets/f0e830e3-6712-4b9d-9af8-72737e6a24d4">

Looking at all the logs, this confirms the commands were successfull and the username and password are most likely exposed.

All logs have a HTTP response code of 200 meaning successful.

<img width="474" alt="Screenshot 2024-11-19 141923" src="https://github.com/user-attachments/assets/46473423-a185-4982-a555-0a57bac2d668">
<img width="353" alt="Screenshot 2024-11-19 141942" src="https://github.com/user-attachments/assets/0ce041b0-045f-4ffb-ab2f-bcfd45dc287f">
<img width="398" alt="Screenshot 2024-11-19 141950" src="https://github.com/user-attachments/assets/a1489e34-eb21-4784-8c99-2b109654c6c0">

Now that I know this attack was successful and credentials are exposed. The next immediate step is to isolate the machine.

And in a real world situation I would escalte this incident due to its severity.

<img width="627" alt="Screenshot 2024-11-19 142231" src="https://github.com/user-attachments/assets/04052abd-aefd-4a1a-a3f5-c88a3eb254a6">

Now to continue the playbook.

<img width="511" alt="Screenshot 2024-11-19 142320" src="https://github.com/user-attachments/assets/20f6a019-da9b-4826-985b-4d7c44bba5f3">

* Yes this incident has malicous intent. This is obvious with the commands probing for credentials.

<img width="506" alt="Screenshot 2024-11-19 142501" src="https://github.com/user-attachments/assets/38a42ee8-f4d1-4927-807e-7099e8d61dbf">

* Attack type was command injection.

<img width="497" alt="Screenshot 2024-11-19 142614" src="https://github.com/user-attachments/assets/b2477a76-6425-4288-adf1-8a932030029e">

* Checking back in the email security tab to confirm nothing was sent, confirms it was not planned.

<img width="464" alt="Screenshot 2024-11-19 142824" src="https://github.com/user-attachments/assets/b1c4918a-9344-4cf0-b401-9a49203bac4d">

* Direction of traffic was from Internet -> Company 

<img width="523" alt="Screenshot 2024-11-19 142910" src="https://github.com/user-attachments/assets/43c1af22-ac83-466c-9d8b-3a167573dd35">

* Yes as we saw this attack was successful

<img width="496" alt="Screenshot 2024-11-19 143143" src="https://github.com/user-attachments/assets/75aedcfb-5272-4850-9d48-4bda57c53c2b">

* Add my artifacts

<img width="514" alt="Screenshot 2024-11-19 143242" src="https://github.com/user-attachments/assets/4c274663-28d5-46f9-b339-cece1b7139a9">

* Yes escalation is needed due to the severity of credentials being leaked.

<img width="425" alt="Screenshot 2024-11-19 143622" src="https://github.com/user-attachments/assets/919d15f2-9790-463d-8ab8-d3947beaf944">

<img width="698" alt="Screenshot 2024-11-19 143705" src="https://github.com/user-attachments/assets/1ebde230-4126-4749-9f97-36e7a76f54a9">




