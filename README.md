# pfds

pfds - report a snapshot of the current processes fd

## usage

- short version

```
$ sudo pfds short `pgrep nginx` | head
   19939 daemon /usr/local/nginx-1.9.5/logs/error.log
   19939 daemon /usr/local/nginx-1.9.5/logs/access.log
   19939 daemon /usr/local/nginx-1.9.5/logs/deflate.log
   19940 daemon /usr/local/nginx-1.9.5/logs/error.log
   19940 daemon /usr/local/apache-2.4.16/htdocs/blog/wp-content/plugins/wp-social-bookmarking-light/images/hatena.gif
   19940 daemon /usr/local/nginx-1.9.5/logs/access.log
```

- output with cpu and memory usage

```
$ sudo pfds `pgrep nginx` | head
   19939  0.0  0.1 daemon /usr/local/nginx-1.9.5/logs/error.log
   19939  0.0  0.1 daemon /usr/local/nginx-1.9.5/logs/access.log
   19939  0.0  0.1 daemon /usr/local/nginx-1.9.5/logs/deflate.log
   19940  0.0  0.3 daemon /usr/local/nginx-1.9.5/logs/error.log
   19940  0.0  0.3 daemon /usr/local/apache-2.4.16/htdocs/blog/wp-content/plugins/wp-social-bookmarking-light/images/hatena.gif
```

## build

- custom `mrblib/pfds/config.rb`

```ruby
module Pfds
  module Config

    MULTI_PROCESS = (ENV["MRUBY_MULTI"] || 4).to_i

    IGNORE_FILES = %w(

    /dev/null
    /var/log/httpd/access_log
    /var/log/httpd/ssl_access_log
    /var/log/httpd/error_log
    /var/log/httpd/ssl_error_log

    )

    IGNORE_PATTERN = %w(

    ^pipe:
    ^anon_inode:
    ^socket:
    ^/dev/pts/

    )
  end
end
```

- build into `mruby/bin/pfds`

```
rake
```

# License
under the MIT License:

* http://www.opensource.org/licenses/mit-license.php