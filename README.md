# loginNotify
This is a bash script which sends all successfull SSH log-ins to your server
via Telegram bot.Allows to monitor all connections and where are they made from.
Also it using local MySQL DB for whitelist IPs.Using this DB allow to change a 
type of login message - simple view if it's familiar IP + comment from DB to this
IP - usefull to understand who is connecting.
If there is connection from unknown IP (it doesn't exist in DB) - the login message
has another view, and consists info about country and provider of that IP.

Requires curl and whois on the server.

Installation:
- Just download the script to any folder. For example, on Debian-based OS it could be /usr/local/bin/ folder.
- Launch DB init for the first time:
  login-notify initDB <mysql_root_pwd> <db_name> <db_user> <db_pwd>
    <mysql_root_pwd> - password of mysql root account to create everything we need. Type "-" if not need to use pwd for root access to mysql
    <db_name> - The name of DB you want to create
    <db_user> - user of the new DB
    <db_pwd> - password you want to set for new DB
- Then you need to edit this script end set the next variables at the top of script:
    dbName=""
    dbUser=""
    tdbPass=""
- Then dont't foreget to fill in $token and $chat variables in there. Telegram bot requires them very much.
- Finally, add to the end of /etc/pam.d/sshd next string: "session optional pam_exec.so <path_to_this_script>/<this_script_name>"
