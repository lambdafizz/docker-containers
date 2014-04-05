nginx
=====

This container runs source installation of nginx on port 80.

It exposes `/usr/local/nginx/conf/sites-enabled` volume, so you can
(and should!) add your own `server` blocks. Just put them on host
machine and then mount volumes with:

`-v <full path on host dir>:/usr/local/nginx/conf/sites-enabled`.

By default there are no `server` blocks added, so you have to add
at least one for nginx to actually return anything.

