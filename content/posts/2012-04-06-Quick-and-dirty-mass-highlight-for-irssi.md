---
comments: true
date: "2012-04-06T18:36:12Z"
categories:
- irc
tags:
- irssi
- perl
- mass highlight
title: Quick and Dirty Mass Highlight for irssi
---

This is the defacto mass highlight I use to annoy the fuck out of people when on
IRC with [irssi][1]. It's good stuff. Modify it to say something incredibly
offensive and use it yourself.

{{< highlight perl >}}
use strict;
use Irssi;

sub cmd_hilight {
        my ($data, $server, $win) = @_;
        my $channel = Irssi::active_win()->get_active_name();
        my $foo = "\cBHey,\cB ";
        foreach ($win->nicks())
        {      
                next if ($_->{'nick'} eq $server->{nick});
                $foo .= "\cB\c_$_->{'nick'}\cB\c_ ";
        }
        $server->command("MSG $channel $foo");
}

Irssi::command_bind('mh', 'cmd_hilight');
{{< / highlight >}}

[1]: http://irssi.org/
