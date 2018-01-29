# rssmail

The purpose of this script is to send an email for each new item found in an RSS feed.
In my main workflow email is very important. I mainly use this script to follow a number
of security related RSS feeds and recieve email alerts when new issue's are published.

## Commandline options

The following commandline options are available:

`-h, --help`

Shows a brief usage message.

`-c <file>, --config <file>`

Overrides the default confgifile locations.

## Configuration

The configuration file is searched for at the locations below in the specified 
order. As soon as a configuration file is found, searching is stopped.

`~/.rssmail.cfg`
`/etc/rssmail.cfg`

These locations are not checked when the configuration file location is 
overridden from the commandline.

Lines in the configuration file that are empty or start with a # will be ignored. So it
is possible to add comments in the file.

The configuration file has generic settings and feeds configuration.

### Generic settings

**email-to**

The specifies 1 or more email (comma seperated) email addresses where output is sent to.

For example, send mail to admin user:

`email-to=admin@example.com`

Send mail to Alice and Bob:

`email-to=alice@example.com,bob@example.com`

**email-from**

This specifies the sending email address. Can be useful for filtering.

Send mail as user rssfeed:

`email-from=rssfeed@example.com`

**xmlstarlet**

This specifies the command name for the xmlstarlet package. When not
defined it defaults to xmlstart.

Override the command to xml:

`xmlstartlet=xml`

### Feeds

It is possible to specify 1 or more feeds in the configuration file. Each line contains
1 feed configuration and should always start with the configuration item feed.

Each feed line contains 3 elements:
* Feed name (is used in the subject of the email)
* Date and time of last item
* URL

The items are seperated like this:

**\<feed name\>:\<timestamp\>@\<url\>**

The feed name should not contain spaces.

When specifying a new feed, the timestamp can be ommited. This will set the feed to the
latest item. Any item published in the feed will not be mailed.

An example feed line for the EFF Action Center feed:

`feed=EFF action:@https://act.eff.org/action.atom`

## Running

The script has a couple of dependancies. The script checks if these are available:

* xmlstarlet
* sed
* mail

The script can be started without arguments:

`rssmail`

It is most useful to start it from cron, for example every hour, 10 past the hour:

`10 * * * * /home/user/bin/rssmail`
