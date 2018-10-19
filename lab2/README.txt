 _          _    ____            ____            _   _____ _ _
| |    __ _| |__|___ \          | __ )  __ _  __| | |  ___(_) | ___  ___
| |   / _` | '_ \ __) |  _____  |  _ \ / _` |/ _` | | |_  | | |/ _ \/ __|
| |__| (_| | |_) / __/  |_____| | |_) | (_| | (_| | |  _| | | |  __/\__ \
|_____\__,_|_.__/_____|         |____/ \__,_|\__,_| |_|   |_|_|\___||___/

Introduction
------------
The purpose of this lab is to track suspicious files dropped on the file system.

Recipe
------
To achieve this, we will use an export from a MISP instance and populate the rootcheck detection feature.

Steps
-----
1. Let's use my script 'mof.py' ("MISP OSSEC Feeder"). To gain time, a file is already present in your /lab2 directory.

2. Review the file misp_windows_ioc.txt to learn the format

3. We don't have a Windows agent available, let's create a simple UNIX config.
A sample configuration is already available in your /lab2 directory:

        lab2_unix_ioc.txt

4. Add the file to your OSSEC agent config:

# cd /var/ossec/etc/shared
# cp /home/student/lab2/lab2_unix_ioc.txt .
# cd ../etc
# vi ossec.conf

Add new lines in the <rootcheck> block:

<frequency>600</frequency>
<rootkit_files>/var/ossec/etc/shared/lab2_unix_ioc.txt</rootkit_files>

Save the file and restart OSSEC

5. Create the test file:

# touch /etc/ossec_is_here

6. Wait approx 10 mins and check the alerts.log file for results:

# tail -f /var/ossec/logs/alerts/alerts.log

