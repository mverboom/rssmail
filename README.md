# rssfeed

The purpose of this script is to send an email for each new item found in an RSS feed.
In my main workflow email is very important. I mainly use this script to follow a number
of security related RSS feeds and recieve email alerts when new issue's are published.

## Configuration

The script requires a configuration file which is expected in the homedirectory of the
user running the script:

  ~/.rssmail.cfg

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

### Feeds

It is possible to specify 1 or more feeds in the configuration file. Each line contains
1 feed configuration and should always start with the configuration item feed.

Each feed line contains 3 elements:
* Feed name (is used in the subject of the email)
* Date and time of last item
* URL

The items are seperated like this:

**<feed name>:<timestamp>@<url>**

When specifying a new feed, the timestamp can be ommited. This will set the feed to the
latest item. Any item published in the feed will not be mailed.

An example feed line for the EFF Action Center feed:

`feed=EFF action:@https://act.eff.org/action.atom`

