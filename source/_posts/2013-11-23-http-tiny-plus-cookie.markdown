---
layout: post
title: "HTTP::Tiny + cookie"
date: 2013-11-23 03:00:00 +0900
comments: true
categories: perl
---

HTTP::Tiny でただ単に cookie を set してリクエストしたいときがよくある。
add, cookie_header メソッドをもったクラスなら cookie になるらしいので、
以下のようにすればいい。

```
#!/usr/bin/env perl
use strict;
use warnings;
use HTTP::Tiny;

{
    package Cookie;
    sub new {
        my ($class, $raw) = @_;
        bless { raw => $raw }, $class;
    }
    sub add {}
    sub cookie_header { shift->{raw} }
}

my $cookie = Cookie->new( 'rk=your-cookie-value' );
my $url = "http://b.hatena.ne.jp/ks0608/atomfeed";
my $ua = HTTP::Tiny->new( cookie_jar => $cookie );
my $res = $ua->get($url);

die "Failed." unless $res->{success};
print "$res->{status} $res->{reason}\n";
print $res->{content};
```

ちなみに、ブラウザから cookie をとるには
[Gnaw Cookie](https://chrome.google.com/webstore/detail/gnaw-cookie/kjhpfgmflgeokjflbkhplnjoikaagedk) 
がおすすめ（ステマ）。
