###  Process Management & Monitoring

1. Start a background process (ping google.com > ping_test.log &)
2. Use ps, top, and htop to monitor it.
3. Kill the process and verify it's gone.

   
##Solution

1. Start a Background Process
We will run a "ping" command to test connectivity to google.com and log the output to a file.
![image](https://github.com/user-attachments/assets/bf7c6f46-78ee-470a-8a65-d2ca525d3713)

here; 
* ping google.com	Sends continuous ping requests to Google.
* 'ping_test.log' 	Redirects the output to ping_test.log file instead of displaying on screen.
* &' 	Runs the command in the background, so you can continue using the terminal.

2. ## Check Running Processes
   
* Use ps (Process Status)
  
#output
![image](https://github.com/user-attachments/assets/9873b2f5-3d73-408c-8dcc-97c2c252189d)


- ps aux shows all running processes.
- grep ping filters out only the ping process

-Use top (Real-Time Monitoring)

#output
![image](https://github.com/user-attachments/assets/7ba50106-da67-4190-a726-1b30cdf09f15)

-Use htop (Better UI for Monitoring)

#output
![image](https://github.com/user-attachments/assets/f75ae00a-377f-46a2-834e-40121ef76265)

3. ## Kill the Background Process
- for this step we need to check Process ID (PID) use "ps aux | grep ping "
  
#output
![image](https://github.com/user-attachments/assets/0db50be9-911f-4176-aac2-d5659909b8c2)
 -For killing the process "kill" PID
  "kill 61"
  
#output
![image](https://github.com/user-attachments/assets/cdc31d49-1426-4275-bbc0-33ec62a9a144)




 


