# rssmail

The purpose of this script is to send an email for each new item found in an RSS feed.
In my main workflow email is very important. I mainly use this script to follow a number
of security related RSS feeds and recieve email alerts when new issue's are published.

## Commandline options

The following commandline options are available:

`-h`

Shows a brief usage message.

`-c <file>`

Overrides the default confgifile locations.

`-m`

Send an email for every new item in the feed.

`-k`

Create an item in kanboard for every new item in the feed.

`-K`

Create an item in kanboard for every new item in the feed and if there is one
or more item, send a mail new items have been created.

## Configuration

The configuration file is searched for at the locations below in the specified 
order. As soon as a configuration file is found, searching is stopped.

`~/.rssmail.cfg`
`/etc/rssmail.cfg`

These locations are not checked when the configuration file location is 
overridden from the commandline.

Lines in the configuration file that are empty or start with a # will be ignored. So it is possible to add comments in the file.

The configuration file has a .ini style format. There is a main section
which specifies gobal settings and a section per configured feed.

### Generic settings

These settings should be set in section [main].

**emailto**

The specifies 1 or more email (comma seperated) email addresses where output is sent to.

For example, send mail to admin user:

`emailto=admin@example.com`

Send mail to Alice and Bob:

`emailto=alice@example.com,bob@example.com`

**emailfrom**

This specifies the sending email address. Can be useful for filtering.

Send mail as user rssfeed:

`emailfrom=rssfeed@example.com`

**xmlstarlet**

This specifies the command name for the xmlstarlet package. When not
defined it defaults to xmlstart.

Override the command to xml:

`xmlstartlet=xml`

**proxy**

This specifies a proxy to use when retrieving the RSS feed. Without this
option no specific proxy is set, but any proxy defined in the environment
will not be removed.

Set proxy to wwwproxy with port 3128

`proxy=wwwproxy:3128`

**ipv4only**

This forces the RSS feed URL's to be retrieved over IPv4 only.

Force connection over IPv4

`ipv4only=1`

**kanboardapikey**

This is the API key in kanboard that needs to be used to use the API.

**kanboardapi**

This is the URL where the kanboard API can be reached.

**kanboardproject**

Name of the kanboard project into which the items need to be created.

### Feeds

It is possible to specify 1 or more feeds in the configuration file. Each feed
requires its own section.

The section name is the shorthand name for the feed. The name can not contain
spaces.

Below are the elements that can be defined for a feed.

#### timestamp (mandatory)

When initially specifying a feed, this field should be defined empty:

`timestamp=`

It will be updated automatically when the feed is processed.

#### url (mandatory)

This is the url of the RSS feed that needs to be parsed.

For example:

`url=https://act.eff.org/action.atom`

#### titleexclude (optional)

This option specifies a pattern that will be applied to the title of a feed
item. If the pattern matches, the item will not be processed.

The pattern is matched using egrep. Compatible patterns can be used.

For example:

`titleexclude=exclude this title|exclude other title`

#### titleinclude (optional)

This option specifies a pattern that will be applied to the title of a feed
item. If the pattern matches, the item will be processed.

The pattern is matched using egrep. Compatible patterns can be used.

`titleinclude=include this title|include other title`

#### linkexclude (optional)

This option specifies a pattern that will be applied to the link of a feed
item. If the pattern matches, the item will not be processed.

The pattern is matched using egrep. Compatible patterns can be used.

For example:

`linkexclude=exclude this link|exclude other link`

#### linkinclude (optional)

This option specifies a pattern that will be applied to the link of a feed
item. If the pattern matches, the item will be processed.

The pattern is matched using egrep. Compatible patterns can be used.

`linkinclude=include this link|include other link`

## Running

The script has a couple of dependancies. The script checks if these are available.

The script can be started without arguments:

`rssmail`

It wil show help output.

It is most useful to start it from cron. For example every hour, 10 past the hour send email for all matches:

`10 * * * * /home/user/bin/rssmail -m`
