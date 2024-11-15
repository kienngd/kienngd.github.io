# A Late Night Database Recovery Story


## The story
It was late at night when my close friend called me. He was panicked because his database was lost.

He sent me information , then I logged into the server to check. The MySQL service was still running. I found that both `general log` and `binary log` were enabled on the server.

<!--more-->
![Security MySQL](securing-mysql-banner.png "Security MySQL")

When I checked the `general log`, I saw a `delete command` at 8 PM. It came from IP 192.x.x.x using `MySQL Workbench`. After investigation, he told me this was an old, un-used `test server`. Someone had saved MySQL credentials in MySQL Workbench.

The binary logs were partially deleted. Only logs from recent days remained. The system had `no regular backup schedule`.

Luckily, a developer had dumped all database for testing about a week ago. I restored this dump to a new server and checked its master status. It showed we could possibly recover data from binary logs.

I looked through binary log files. I found the exact file and position of the delete command.

Here's what I did to recover the data:
1. Backed up current data (though not much was left)
2. Restored data from the dump file
3. Replayed binary logs from the master position to just before the delete command

After these steps, the data was back to normal. It was a relief!

## Lessons Learned
- Always have regular backups
- Be careful with saved database credentials
- Don't leave test servers unmanaged
- Enable logging can save you in emergencies

This incident shows how important proper database management is. We were lucky this time, but it could have been much worse.
