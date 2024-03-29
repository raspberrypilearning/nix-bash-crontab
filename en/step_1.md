Sometime you don't want to manually start a script that you have written. You may need the script to run once every hour, or maybe once every thirty seconds, or every time your computer starts. On *nix systems this is a fairly easy task, because you can use a program called **Cron**. Cron will run any command you tell it to run, whenever you have scheduled for it to do so. It will reference what is known as the **cron table**, which is normally abbreviated to **crontab**.

*[*nix]: Computers running a UNIX-like operating system (macOS or GNU/Linux)

### Editing the crontab

- To open the crontab, you first need to open a terminal window. Then you can type:

	~~~bash
	crontab -e
	~~~

- The `-e` in this command is short for *edit*. If this is your first time opening your crontab, then you'll be asked which text editor you would like to use.

```bash
rpf@raspberrypi:~ $ crontab -e
no crontab for rpf - using an empty one

Select an editor.  To change later, run 'select-editor'.
  1. /bin/nano        <---- easiest
  2. /usr/bin/vim.tiny
  3. /bin/ed

Choose 1-3 [1]: 
```
	
- Unless you have plenty of experience using **ed** or **vim**, the simplest editor to use is **nano**, so type `2` to choose it and press `Enter`.

	![crontab in nano](images/crontab-nano.png)
	
- nano is a simple command line text editor. If you want to learn more about using nano, you can have a look at [this resource](nix-bash-using-nano).

*[command line]: A way of interfacing with your computer using text commands
*[text editor]: A program for reading and editing text files

### Syntax for Cron

The crontab contains all the basic information you need to get started. Each line that starts with a `#` is a comment, and therefore ignored by the computer. At the bottom of the crontab you should see a line that looks like this:

```bash
# m h  dom mon dow   command
```

- `m` is short for **minute**
- `h` is short for **hour**
- `dom` is short for **day of the month**
- `mon` is short for **month**
- `dow` is short for **day of the week**
- `command` is the bash command that you want to run

### Creating a new Cron job

To create a Cron job you need to decide under which circumstances you would like it to run. For instance, if you wanted to run a Python script on the 30th minute of every hour, you would write the following, but make sure to change the `rpf` username to your own username.

```bash
30 * * * * python3 /home/rpf/my_cool_script.py
```

If you wanted it to run every 30 minutes you would use:

```bash
*/30 * * * * python3 /home/rpf/my_cool_script.py
```

The `30` is telling the script to run every 30 minutes. The asterisks indicate that the script needs to run for all **legal values** for the other fields.

Here are a few more examples.

| What will happen...                              | crontab syntax                    |
|--------------------------------------------------|-----------------------------------|
| Run a script at 11:59 every Tuesday              | `59 11 * * 2 python3 /home/pi/my_script.py`  |
| Run a script once a week on Monday               | `0 0 * * 1 python3 /home/pi/my_script.py`    |
| Run a script at 12:00 on the 1st of Jan and June | `0 12 1 1,6 * python3 /home/pi/my_script.py` |

### Run on boot

One incredibly useful feature of Cron is its ability to run a command when the computer boots up. To do this, you use the `@reboot` syntax. For instance:

```bash
@reboot python3 /home/rpf/my_cool_script.py
```

### Edit and save the file

You can add in your cron job to the bottom of the crontab. Then save and exit nano by pressing `Ctrl+x` and then typing in 'y' when you are prompted to save. 
