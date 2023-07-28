# Standard wordpress – replacing DB urls

wp search-replace 'www.olddomain.com' 'www.newdomain.com' –all-tables –allow-root

# Multisite WordPress – replace database urls

## First step - change wp-config.php - DOMAIN_CURRENT_SITE to: www.newdomain.com

wp search-replace --url=www.olddomain.com www.olddomain.com www.newdomain.com 'wp_*options' wp_blogs
wp search-replace 'www.olddomain.com' 'www.newdomain.com' --all-tables –network
wp search-replace 'http://www.newdomain.com' 'https://www.newdomain.com' --all-tables –network
wp search-replace "http:\/\/www.newdomain.com" "https:\/\/www.newdomain.com" --all-tables --network
