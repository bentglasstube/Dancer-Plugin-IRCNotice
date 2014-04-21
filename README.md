# NAME

Dancer::Plugin::IRCNotice - Send IRC notices from your dancer app

# SYNOPSIS

    use Dancer::Plugin::IRCNotice;

    notify('This is a notification');

# DESCRIPTION

Dancer::Plugin::IRCNotice provides a quick and dirty way to send IRC NOTICEs to
a specific channel.

This is __very alpha__ software right now.  No error checking is done and it
uses a fork to (optionally) background the process of sending the notice.

# CONFIGURATION

    plugins:
      IRCNotice:
        host: 'chat.freenode.net'
        nick: 'testnick12345'
        name: 'Dancer::Plugin::IRCNotify'
        channel: '#dpintest'
        fork: 1

The host, nick, name, and channel should be pretty obvious.  If fork is set to
a true value, the plugin will fork and background the sending of the notice.

# TODO

This is so bootleg, it really needs to be cleaned up to handle IRC correctly.
Unfortunately, all of the IRC modules I saw on cpan are event based
monstrosities so this just uses [IO::Socket::IP](http://search.cpan.org/perldoc?IO::Socket::IP) to connect.

The notify routine should probably let you override the settings or maybe I
should use something like [Dancer::Plugin::DBIC](http://search.cpan.org/perldoc?Dancer::Plugin::DBIC) to define multiple notifiers
that can then be used.

A connection to IRC must be made for each notification presently.  Instead, it
should try to keep a connection open and reuse it or something.  However, that
would require threads instead of simple forking, and I'm not sure how that will
play with whatever plack frontend people are using.

# AUTHOR

Alan Berndt <alan@eatabrick.org>

# COPYRIGHT

Copyright 2013 Alan Berndt

# LICENSE

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
