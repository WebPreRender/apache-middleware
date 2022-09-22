👋 Hi, I’m **@WebPreRender**

**`apache-middleware (beta)`**
 If your website is hosted on Apache Webserver then you need to follow this steps to make prerender work or you can ask your server guy to enable this modules in Apache.

 1. Login to Server, You Must need to Login with root user
 2. Run this commands
 - [ ] `a2enmod rewrite`
 - [ ] `a2enmod headers`
 - [ ] `a2enmod proxy*`
 - [ ] `a2enmod ssl`
 3. Run this commands, to restart your Apache server
 - [ ] `service apache2 restart`

 4. Add this code to your **.htaccess** file
   
        <IfModule mod_rewrite.c>
        RequestHeader set X-Web-Prerender-Token "YOUR_TOKEN"
        RewriteEngine On

        <IfModule mod_proxy_http.c>
        RewriteCond %{HTTP_USER_AGENT} googlebot|bingbot|yandex|baiduspider|facebookexternalhit|twitterbot|rogerbot|linkedinbot|embedly|quora\ link\ preview|showyoubot|outbrain|pinterest\/0\.|pinterestbot|slackbot|vkShare|W3C_Validator|whatsapp|redditbot|applebot|flipboard|tumblr|bitlybot|skypeuripreview|nuzzel|discordbot|google\ page\ speed|qwantify|bitrix\ link\ preview|xing-contenttabreceiver|chrome-lighthouse|telegrambot [NC,OR]
        RewriteCond %{QUERY_STRING} _escaped_fragment_
        RewriteCond %{REQUEST_URI} ^(?!.*?(\.js|\.css|\.xml|\.less|\.png|\.jpg|\.jpeg|\.gif|\.pdf|\.doc|\.txt|\.ico|\.rss|\.zip|\.mp3|\.rar|\.exe|\.wmv|\.doc|\.avi|\.ppt|\.mpg|\.mpeg|\.tif|\.wav|\.mov|\.psd|\.ai|\.xls|\.mp4|\.m4a|\.swf|\.dat|\.dmg|\.iso|\.flv|\.m4v|\.torrent|\.ttf|\.woff|\.svg))

        RewriteRule ^(index\.html|index\.php)?(.*) https://crawl.webprerender.io/?url=%{REQUEST_SCHEME}://%{HTTP_HOST}$2 [P,END]
        </IfModule>
    </IfModule>
