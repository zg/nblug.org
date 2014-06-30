# NBLUG.org

This is the nblug.org web site.
It's static HTML, built from [Markdown][markdown] files in the ``content/`` directory using [Pelican][pelican].

[markdown]: https://en.wikipedia.org/wiki/Markdown
[pelican]: http://docs.getpelican.com/

## Getting Started

To make it easy to reproduce the site exactly, we install pinned versions of all of the tools used to build it in a Python "virtual environment".
Bootstrap requires this tool in the host system.
On a Debian-like system:

    sudo apt-get install python-virtualenv

(On Debian Jessie the package has been renamed to ``virtualenv``.)

Next create and initialize the virtualenv:

    make init

## Building the Site

You can build and view the site locally with these commands:

    make devserver
    make regenerate

This will launch a web server in the background and monitor the Pelican site contents and configuration, automatically rebuilding when changes occur.
You can view this local site at <http://localhost:8000/>.
When you're done you can stop it with ``make stopserver``.

When you're ready to publish to the real site, run these commands:

    make publish
    make rsync_upload

For the second command to work you will need shell access to enigma.wiredgoats.com (and your username must be set in ``~/.ssh/config`` if it differs from your local username).

Don't forget to commit your changes to the git repo!

## Adding Events

All of the events are stored as text Markdown files in``content/news/``.
These files start with a metadata header in which we place some NBLUG-specific data about the speaker time of the presentation.
A blank line follows this header, then the talk description in Markdown format (which may include embedded HTML if necessary).
For example, ``content/news/2016-11-20-strfry.md``:

    Title: Data Security with strfry()
    Tags: general meeting
    Start: 2016-12-25 7:30 pm
    End: 2016-12-25 9:00 pm
    Speaker: Kyle Rankin
    Location: O'Reilly Media
    Author: Alan Cecil

    This talk will cover a frequently-overlooked security feature of the GNU C library: the ability to apply one-way encryption to NUL-terminated strings.

In this example, the ``Speaker`` field is for the name of the presenter, while the ``Author`` field contains the name of the poster—that is, *your name*.

The ``Tags`` field should contain one of these values:

 * general meeting
 * installfest
 * board meeting

In the filename "2016-11-20" is today's date, when this notice is posted.

## Migrating Pages from the Old Site

When migrating pages from the Drupal site, an additional metadata field can be used to make sure the page shows up with the same URL:

    Druapl_Node: <number>

You can get this value from the URL of the page, which will look something like this:

    http://nblug.org/node/<number>

See ``content/news/2011-11-08-gpu-password-cracking-election.md`` for an example of this.

Some pages on Drupal don't actually list a publication date.
For these, use the event date instead.