# Installation Troubleshooting



### In this article, possible error messages:

---

- It was not possible to move mattermost `to/opt/mattermost`.
- `cp: could not get status of 'mattermost/*'`: Non-existent file or directory. 
- Job for nginx.service failed because the control process exited with error code. See "systemctl status nginx.service" and "journalctl -xeu nginx.service" for details.

---



#### It was not possible to move mattermost `to/opt/mattermost` when `sudo mv mattermost /opt`



> **Error Message:**
>
> mv: could not move 'mattermost' to '/opt/mattermost': Directory not empty



Verify the if there's existing directory content:

```bash
sudo ls /opt/mattermost
```

Decide what to do with the existing directory 

##### Option 1: Overwrite the existing directory

If you decide to overwrite the existing directory, you can delete the current directory and then move the new one.

Warning: This action will permanently delete the contents of the existing directory.

```bash
sudo rm -rf /opt/mattermost
sudo mv mattermost /opt
```

##### Option 2: Merge directory contents
If you want to merge the contents of the new directory with the existing one, you can copy the files manually. Note, however, that this may lead to conflicts if files with the same name exist.

```bash
sudo cp -r mattermost/* /opt/mattermost/
```

##### Option 3: Moving the existing directory to another location
If you prefer not to overwrite existing content, you can move the current directory to another location before moving the new one.

```bash
sudo mv /opt/mattermost /opt/mattermost_backup
sudo mv mattermost /opt
```

After moving the new directory to /opt, continue with the Mattermost configuration.

If you decide to merge or move the directory, remember that you may need to adjust the permissions and check the configuration again.





#### `cp: could not get status of 'mattermost/*'`: Non-existent file or directory when     `sudo cp -r mattermost/* /opt/mattermost/`

 Verify current location and content

```bash
pwd
ls
```

Download Mattermost again (if necessary). If the mattermost directory is not present, you can download it again by following the correct steps.

Download Mattermost tar file:

```bash
wget https://releases.mattermost.com/7.10.2/mattermost-7.10.2-linux-amd64.tar.gz
```

Extract the tar file:

```bash
tar -xvzf mattermost-7.10.2-linux-amd64.tar.gz
```

After downloading and extracting, move the directory to `/opt`:

```bash
sudo mv mattermost /opt
```

After moving the new directory to /opt, continue with the Mattermost configuration.

If you decide to merge or move the directory, remember that you may need to adjust the permissions and check the configuration again.





#### Job for nginx.service failed because the control process exited with error code. See "systemctl status nginx.service" and "journalctl -xeu nginx.service" for details when `sudo systemctl restart nginx`
Verify the status of the Nginx service:

```bash
sudo systemctl status nginx.service
```

Check the Nginx error log:

```bash
sudo journalctl -xeu nginx.service
```

Inspect the Nginx configuration file for possible errors:

```bash
sudo nginx -t
```

This will show any syntax errors in the Nginx configuration. If there are errors, correct them in the relevant configuration files and retry restarting Nginx.

Opens the Nginx configuration file or individual site configuration files to correct errors indicated by the above commands:

```bash
sudo nano /etc/nginx/nginx.conf
sudo nano /etc/nginx/sites-available/default
```

Restart Nginx after correcting the errors:

```bash
sudo systemctl restart nginx
```

By following these steps, you should be able to identify and resolve the problem that is preventing Nginx from starting correctly.



