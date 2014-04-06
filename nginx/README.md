nginx
=====

This container runs source installation of nginx with HttpLuaModule
enabled on port 80.

It exposes `/usr/local/nginx/conf/sites-enabled` and
`/usr/local/nginx/conf/conf.d` volumes, so you can
(and should!) add your own `server` blocks in the first one,
and customized config in the second one.

`-v <path1>:/usr/local/nginx/conf/sites-enabled -v <path2>:/usr/local/nginx/conf/conf.d`

By default there are no `server` blocks added, so you have to add
at least one enabled site inside `sites-enabled`.

The HttpLuaModule is here, so that you can use environment variables
inside `server` blocks, before you do so, you must declare them as *allowed*
inside `conf.d`. To do so, place a file inside this directory with

    env MY_ALLOWED_ENV_VARIABLE;

Let's say, that you want to use an upstream server that runs in another
container named *app*. To do so, you must link the ngixn container into
it. Then you edit `conf.d/allowed-variables.conf`:

   env APP_PORT;

Now inside `sites-enabled/app`:

    upstream application  {
        set_by_lua $srvaddr 'return os.getenv("APP_PORT"):gsub("tcp", "http")';
        server $srvaddr;
    }
 
    server {
        location / {
            proxy_pass  http://application;
        }
    }
