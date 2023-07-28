# Standard wordpress – replacing DB urls

wp search-replace 'www.olddomain.com' 'www.newdomain.com' --all-tables --allow-root

# Multisite WordPress – replace database urls

## First step - change wp-config.php - DOMAIN_CURRENT_SITE to: www.newdomain.com

wp search-replace --url=www.olddomain.com www.olddomain.com www.newdomain.com 'wp_*options' wp_blogs
wp search-replace 'www.olddomain.com' 'www.newdomain.com' --all-tables –network
wp search-replace 'http://www.newdomain.com' 'https://www.newdomain.com' --all-tables –network
wp search-replace "http:\/\/www.newdomain.com" "https:\/\/www.newdomain.com" --all-tables --network

# Troubleshooting

Styles are not displayed properly / some elements look incorrect / broken

Clear cache plugin cache / rebuild cache of assets (css/js)

Browser padlock displays the following error: Your connection to this site is not fully secure / Connection is Not Secure / Page was loaded over HTTPS, but requested an insecure image.

Make sure all database urls have been replaced  from the http:// to https:// domain protocol.

Before changing DNS records, I would like to see how the page works on the new hosting.

You can do it by hardcoding the IP address in your Windows hosts file: \System32\drivers\etc\hosts , example row:

100.200.300.40 newdomain.com www.newdomain.com