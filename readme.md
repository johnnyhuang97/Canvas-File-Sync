# Canvas Class File Sync

Easy-to-use, versatile, platform-independent program that downloads course files from Canvas and syncs them to your cloud storage of choice. Gracefully handles incompatible filenames and preserves deleted/outdated files in a separate folder.

## Prerequisites
This tool requires [rclone](https://rclone.org/downloads/) along with Python 3.7 or later, with the modules `requests` and `pytz`.
Once you have all of these installed, you should be able to run the following commands without errors:
```
$ rclone version
rclone v1.44
- os/arch: linux/arm
- go version: go1.11.1
$ python3.7
Python 3.7.2 (default, Dec 28 2018, 03:13:11) 
[GCC 6.3.0 20170516] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> import pytz
>>> quit()
```

## Quick start
1. Download or clone the repo.
2. Set up a new remote in rclone:
   ```
   $ rclone config
   ...
   n/r/c/s/q> n
   ```
   Remember the remote name you set, as this will be used later.
3. In a web browser, login to Canvas and head to Account > Settings. Under Approved Integrations, click New Access Token. Type a purpose and click Generate Token.
4. Copy the access token that appears.
5. Open the `settings.json.` repo file in a text editor.
6. In the `tokens` object, paste your access token in place of `<access_token>`.
7. Next to `timezone`, set your local timezone that you would like to appear in file version names. (See [here](https://stackoverflow.com/questions/13866926/is-there-a-list-of-pytz-timezones) for a list of acceptable options.)
8. Next to `base_url`, change the domain from ```canvas.instructure.com``` to whatever domain your school's Canvas uses.
9. (optional) If you prefer a different time format to be displated in file version names, set it at `time_fmt`. See [this page](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior) for more details.
10. Set up the courses for which you would like your files synced. Go back to your web browser and visit the homepage for the course in Canvas. In the url bar, you should see something like this:
    ```
    https://<canvas-domain>/courses/123456
    ```
11. Copy the number at the end. This is the course id.
12. In the settings file, edit the `id` of one of the courses to this value. Make sure the `acctep 6.
13. For the `rclone` key, change the drive to the remote name you set in step 2, and change the path to wherever you want your course files to appear relative to your cloud storess_token` key refers to the name in front of the actual token you pasted in sage.
14. Repeat steps 10-13 for each course. You can have as many `courses`, `tokens`, or `rclone` entries you want.
15. Validate the file's text with a website like https://jsonlint.com/.
16. Run the canvassync.py file to test it. (Use ```./canvassync.py -h``` to see available options.)
17. Make a cronjob using ```crontab -e``` to have your files synced automatically on a specified interval and receive email notifications on error. For example, to sync your files every 10 minutes, add the following to the file:
    ```
    MAILTO:<your_email>
    */10 * * * * <path_to_canvassync.py>
    ```
