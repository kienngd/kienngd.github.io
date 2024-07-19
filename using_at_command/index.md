# Using the at Command in Ubuntu 24.04 to Schedule Tasks


**Using the `at` Command in Ubuntu 24.04 to Schedule Tasks**

The `at` command allows users to execute specific actions at any future time without needing continuous supervision. In this example, I use Ubuntu 24.04 to test.

<!--more-->

## The `at` Command

The `at` command in Ubuntu enables users to schedule tasks to run once at a specified time. This can be particularly useful for automating tasks such as system alerts, reminders, or batch jobs.

## How to Use the `at` Command
### Install
```
    sudo apt install at    
```

### Basic usage
- Schedule a command: `at <t:m>` (example: `at 11:30`)to open at-command-editor, input your command and then CTRL + D to exit
- List all commands: `atq` or `at -l`
- View detail command: `at -c <command-ID>`
- Remove a command: `atrm  <command-ID>`

## Example
To schedule a task, you specify the time and provide the command you want to execute. Here's a simple example:
```bash
    echo "zenity --info --text='Relax time' --icon=clock" | at 11:30
    echo "zenity --info --text='Relax time' --icon=clock" | at $(date -d '+25 minutes' +'%H:%M')    
```
\
In this example:
- `zenity --info --text='Relax time' --icon=clock` is the command to display an informational message using Zenity (a graphical utility for dialog boxes).
- `date -d '+25 minutes' +'%H:%M'` calculates the time 25 minutes from now in `hour:minute` format.
- `echo ... | at ...` pipes the command into `at`, which schedules it to run at the specified time.

## Conclusion

The `at` command in Ubuntu 24.04 provides a simple yet powerful way to automate tasks at a specific future time. Whether it's for personal reminders or system maintenance tasks, mastering `at` can significantly enhance your productivity and efficiency on Ubuntu.

Start using `at` today to streamline your workflow and make the most of your Ubuntu system's capabilities.
