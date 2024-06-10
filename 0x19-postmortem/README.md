
Issue Summary

The company's website was down on June 11th, 2024, from 10:00 AM to 10:10 AM EAT. 100% of the users were experiencing Error 500 caused by a misspelled filename in the server's configuration file.

Timeline

- 10:00 AM — Server error occurs and the outage is detected
- 10:02 AM — On-call DevOps team checks the error logs
- 10:03 AM — Updates error configuration
- 10:04 AM — Filename error caught in the configuration file
- 10:06 AM — Writes a Puppet manifest file to correct the error
- 10:08 AM — Puppet manifest file is executed across all company servers
- 10:10 AM — Website is fully restored and working perfectly.

Root Cause and Resolution

The outage of the website began, and we checked the ‘error.log’ file for the cause but surprisingly no errors were listed. We modified the ‘php.ini’ file by changing the line ‘display_errors=off’ to ‘display_errors=on’. This allowed more error logging in the error file. With the help of strace, it appeared that there was a misspelling of a filename that triggered an error whenever a request was sent to the website. The server tried to locate the file as a normal procedure but failed to find the file ending in ".phpp" when it should be looking for ".php". After changing this line in the '/var/www/html/wp-settings.php' file on line 137, the site was back working perfectly 100%. A Puppet manifest was written and executed across all company servers immediately after to restore service.

Corrective and Preventative Measures

After fixing this error, we decided on the corrective and preventive measures that we should take to avoid future failures like this:

- Run as many tests as possible on the site before deploying so that malfunctions can be detected and corrected.
- Thoroughly check the configuration files before deploying for any typos.
- Keep the error display on for any possible errors.



