# host-and-access-laravelwebsitein-localnetwork-and-on-yourphone


To run a Laravel project on your local network and make it accessible from another device like your phone, follow the steps below. This documentation applies to both Windows and Linux systems.

1. Set Up the Laravel Project
On Windows:
Install Laravel via Composer if not already done.
```bash
composer create-project --prefer-dist laravel/laravel project-name
```

Start the Laravel development server:
Navigate to your project directory in the terminal (e.g., C:\xampp\htdocs\project-name) and run:
```bash
php artisan serve --host=0.0.0.0 --port=8000
```
The --host=0.0.0.0 option allows access from other devices on the network.
The default port is 8000, but you can change it if needed.

On Linux (Ubuntu):
Navigate to your Laravel project directory:
```bash
cd /path/to/your/laravel-project
```

Start the Laravel development server with network access:
```bash
php artisan serve --host=0.0.0.0 --port=8000
```

2. Find Your PC's Local IP Address
Your phone will connect to the Laravel project using your PC's local IP address.

On Windows:
Open Command Prompt (CMD):
Press Win + R, type cmd, and press Enter.

Find your IP address:
Run:
```bash
ipconfig
```
Look for the IPv4 Address under your active network connection.

On Linux (Ubuntu):
Open a terminal and run:
```bash
ip addr
```
Look for the inet address associated with your active network interface.


3. Access the Laravel Project from Your Phone
Make sure your phone is connected to the same Wi-Fi network as your PC.

On your phone, open a browser and type the URL:
```bash
http://<your-pc-ip>:8000
```
Replace <your-pc-ip> with your PC's local IP address.

### This is the end of the major steps, until here everything should work!, if it doesn't then you can read the other steps and notes below...!, Have a goodluck !.
................................................................................


4. Configure the Firewall (If Necessary)
On Windows:
Allow PHP through the firewall:
Go to Control Panel > Windows Defender Firewall > Allow an app or feature through Windows Defender Firewall.
Find PHP or add it manually, ensuring both Private and Public are checked.
On Linux (Ubuntu):
If you're using ufw (Uncomplicated Firewall), allow traffic on port 8000:
```bash
sudo ufw allow 8000
sudo ufw reload
```

5. Verify Laravel Configuration
Ensure Laravel is properly configured to serve requests from your local network:

Open the AppServiceProvider.php file:
```bash
nano app/Providers/AppServiceProvider.php
```

Add the following in the boot() method:
```bash
use Illuminate\Support\Facades\URL;

public function boot()
{
    if (env('APP_ENV') !== 'production') {
        URL::forceRootUrl(config('app.url'));
    }
}
```

Set the APP_URL in the .env file to use your local IP:
```bash
APP_URL=http://<your-pc-ip>:8000
```

Clear the cache:
```bash
php artisan config:clear
php artisan cache:clear
php artisan route:clear
```


To run a Laravel project on your local network and make it accessible from another device like your phone, follow the steps below. This documentation applies to both Windows and Linux systems.

1. Set Up the Laravel Project
On Windows:
Install Laravel via Composer if not already done.
```bash
composer create-project --prefer-dist laravel/laravel project-name
```

Start the Laravel development server:
Navigate to your project directory in the terminal (e.g., C:\xampp\htdocs\project-name) and run:
```bash
php artisan serve --host=0.0.0.0 --port=8000
```

On Linux (Ubuntu):
Navigate to your Laravel project directory:
```bash
cd /path/to/your/laravel-project
```

Start the Laravel development server with network access:
```bash
php artisan serve --host=0.0.0.0 --port=8000
```

2. Find Your PC's Local IP Address
Your phone will connect to the Laravel project using your PC's local IP address.

On Windows:
Open Command Prompt (CMD):
Press Win + R, type cmd, and press Enter.

Find your IP address:
Run:
```bash
ipconfig
```
Look for the IPv4 Address under your active network connection.

On Linux (Ubuntu):
Open a terminal and run:
```bash
ip addr
```

Look for the inet address associated with your active network interface (e.g., 192.168.x.x).

3. Access the Laravel Project from Your Phone
Make sure your phone is connected to the same Wi-Fi network as your PC.

On your phone, open a browser and type the URL:
```bash
http://<your-pc-ip>:8000
```

Replace <your-pc-ip> with your PC's local IP address (e.g., 192.168.1.100).

4. Configure the Firewall (If Necessary)
On Windows:
Allow PHP through the firewall:
Go to Control Panel > Windows Defender Firewall > Allow an app or feature through Windows Defender Firewall.
Find PHP or add it manually, ensuring both Private and Public are checked.
On Linux (Ubuntu):
If you're using ufw (Uncomplicated Firewall), allow traffic on port 8000:
```bash
sudo ufw allow 8000
sudo ufw reload
```

5. Verify Laravel Configuration
Ensure Laravel is properly configured to serve requests from your local network:

Open the AppServiceProvider.php file:
```bash
nano app/Providers/AppServiceProvider.php
```

Add the following in the boot() method:
```bash
use Illuminate\Support\Facades\URL;

public function boot()
{
    if (env('APP_ENV') !== 'production') {
        URL::forceRootUrl(config('app.url'));
    }
}
```

Set the APP_URL in the .env file to use your local IP:
```bash
APP_URL=http://<your-pc-ip>:8000
```

Clear the cache:
```bash
php artisan config:clear
php artisan cache:clear
php artisan route:clear
```

6. Troubleshooting Common Issues
Issue: "Requested URL was not found on this server."
Check the URL in the browser on your phone and ensure the IP and port match exactly.
Issue: Phone Cannot Connect to the Laravel Server
Ensure your phone and PC are on the same Wi-Fi network.
Check your firewall settings to allow port 8000.

Check Laravel Logs:
If the page doesn’t load, check the logs for errors:
```bash
tail -f storage/logs/laravel.log
```

Check PHP Server Status:
Ensure the Laravel development server is running:
```bash
php artisan serve
```



### NOTE:
If your Laravel website takes a long time to load on the phone via the local network, there could be several reasons for the slowness. Below are steps to optimize the setup and troubleshoot issues:

If your Laravel website takes a long time to load on the phone via the local network, there could be several reasons for the slowness. Below are steps to optimize the setup and troubleshoot issues:

1. Check Your Network Connection
Wi-Fi Signal Strength: Ensure your phone and PC are connected to a strong Wi-Fi signal. Weak signals can cause delays.
Router Speed: If your router is slow or overloaded, it will affect the loading time. Try restarting your router.


If your Laravel website takes a long time to load on the phone via the local network, there could be several reasons for the slowness. Below are steps to optimize the setup and troubleshoot issues:

1. Check Your Network Connection
Wi-Fi Signal Strength: Ensure your phone and PC are connected to a strong Wi-Fi signal. Weak signals can cause delays.
Router Speed: If your router is slow or overloaded, it will affect the loading time. Try restarting your router.
2. Optimize Laravel for Local Network
Laravel’s development mode (php artisan serve) is not optimized for performance. Here’s how to make it faster:

Disable Debugging in .env
Debug mode can slow down requests as Laravel processes and displays detailed logs.

Open the .env file.
Set APP_DEBUG to false:
```bash
APP_DEBUG=false
```

Clear the configuration cache:
```bash
php artisan config:clear
```

Cache Routes and Configurations
Caching can improve performance by reducing runtime processing:
Cache routes:
```bash
php artisan route:cache
```
Cache configurations:
```bash
php artisan config:cache
```

Serve Static Files Efficiently
By default, php artisan serve doesn’t serve static files like CSS, JS, or images efficiently.

Use a real web server like Apache or Nginx for development:

Install Apache or Nginx on your system.
Point the server’s document root to Laravel's public folder.
Configure it to serve your app over the local network.
If you want to keep using php artisan serve, make sure you’re not loading unnecessary large files.

How to achieve the above:
To serve static files efficiently in a Laravel application, it's recommended to use a real web server like Apache or Nginx instead of the built-in PHP development server (php artisan serve). Below are the steps to set up either Apache or Nginx to serve your Laravel application over a local network.

Using Apache
Step 1: Install Apache
For Windows: You can use XAMPP or WAMP, which includes Apache.
For Ubuntu: Run the following command:
```bash
sudo apt update
sudo apt install apache2
```

Step 2: Enable Required Apache Modules
Make sure the following modules are enabled:
```bash
sudo a2enmod rewrite
```

Step 3: Configure Apache
Create a New Configuration File: Create a new configuration file for your Laravel project. For example, create a file named laravel.conf in the Apache configuration directory:
```bash
sudo nano /etc/apache2/sites-available/laravel.conf
```

Add the Following Configuration: Replace /path/to/your/laravel/public with the actual path to your Laravel project's public directory.
```bash
VirtualHost *:80>
    ServerName your-local-domain.test
    DocumentRoot /path/to/your/laravel/public

    <Directory /path/to/your/laravel/public>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/laravel_error.log
    CustomLog ${APACHE_LOG_DIR}/laravel_access.log combined
</VirtualHost>
```

Example:
```bash
<VirtualHost *:80>
    ServerName your-local-domain.test
    DocumentRoot /home/jbtechnix/Downloads/programmingandcoding/website/jbwebwsc/public

    <Directory /home/jbtechnix/Downloads/programmingandcoding/website/jbwebwsc/public>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/jbwebwsc_error.log
    CustomLog ${APACHE_LOG_DIR}/jbwebwsc_access.log combined
</VirtualHost>
```

Enable the New Site:
```bash
sudo a2ensite laravel.conf
```
Restart Apache:
```bash
sudo systemctl restart apache2
```

Step 4: Update Your Hosts File (Optional)
If you want to access your Laravel app using a custom domain (like your-local-domain.test), you need to update your hosts file.

Edit the Hosts File:

Windows: Open C:\Windows\System32\drivers\etc\hosts in a text editor with administrator privileges.
Linux: Edit /etc/hosts.
Add the Following Line:
```bash
127.0.0.1 your-local-domain.test
```

Step 5: Access Your Laravel Application
Find Your Local IP Address: Use ipconfig (Windows) or ifconfig (Linux) to find your local IP address.

Access from Your Phone: Open a web browser on your phone and enter:
```bash
http://<your-local-ip-address>
```
or if you set up a custom domain:
```bash
http://your-local-domain.test
```

Using Nginx
Step 1: Install Nginx
For Ubuntu:
```bash
sudo apt update
sudo apt install nginx
```

Step 2: Configure Nginx
Create a New Configuration File: Create a new configuration file for your Laravel project:
```bash
sudo nano /etc/nginx/sites-available/laravel
```

Add the Following Configuration: Replace /path/to/your/laravel/public with the actual path to your Laravel project's public directory.
```bash
server {
    listen 80;
    server_name your-local-domain.test;

    root /path/to/your/laravel/public;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock; # Adjust PHP version if necessary
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

Enable the New Site:
```bash
sudo ln -s /etc/nginx/sites-available/laravel /etc/nginx/sites-enabled/
```

Test Nginx Configuration:
```bash
sudo nginx -t
```

Restart Nginx:
```bash
sudo systemctl restart nginx
```

Step 3: Update Your Hosts File (Optional)
Follow the same steps as in the Apache section to update your hosts file if you want to use a custom domain.

Step 4: Access Your Laravel Application
Find Your Local IP Address: Use ifconfig to find your local IP address.

Access from Your Phone: Open a web browser on your phone and enter:
```bash
http://<your-local-ip-address>
```

or if you set up a custom domain:
```bash
http://your-local-domain.test
```







3. Optimize Assets
Minify CSS and JS Files
Minifying reduces file sizes and speeds up loading:

Open webpack.mix.js in your Laravel project.
Use mix.minify() to minify your assets:
```bash
mix.js('resources/js/app.js', 'public/js')
   .postCss('resources/css/app.css', 'public/css', [
      require('tailwindcss'),
   ])
   .minify('public/js/app.js')
   .minify('public/css/app.css');
```

Recompile assets:
```bash
npm run production
```

Use a CDN for Common Libraries
Instead of serving libraries (e.g., jQuery, Bootstrap) locally, use a CDN:

Replace local script and stylesheet references with CDN links in your Blade templates.
Example:
```bash
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

4. Optimize Images
Large images can cause significant delays, especially over a slow network.

Compress images using tools like TinyPNG.
Use responsive image tags in your Blade templates:
```bash
<img src="{{ asset('images/example.jpg') }}" alt="example" loading="lazy">
```

5. Enable Browser Caching
Configure headers to allow browsers to cache static files like images, CSS, and JavaScript.

If you’re using Apache, add the following to .htaccess in the public folder:
```bash
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresByType image/jpg "access 1 month"
    ExpiresByType image/png "access 1 month"
    ExpiresByType image/gif "access 1 month"
    ExpiresByType image/jpeg "access 1 month"
    ExpiresByType text/css "access 1 month"
    ExpiresByType application/javascript "access 1 month"
</IfModule>
```

6. Optimize Database Queries
Check for unnecessary queries in your controllers or views.
Use Eager Loading to reduce the number of queries:
```bash
$users = User::with('posts')->get();
```
Optimize database indexes for faster lookups.


7. Troubleshoot Network Latency
Test Network Latency
Use ping to test the latency between your phone and PC:

On your phone, install a terminal app (like Termux) or use a computer.
Run:
```bash
ping <PC-IP-Address>
```
Improve Latency
If latency is high, consider using a wired connection for your PC.
Check for interference or overloading on your Wi-Fi channel. Use a tool like Wi-Fi Analyzer to identify the best channel.

8. Run a Performance Monitor
Use Laravel Telescope to monitor the performance of requests:

Install Telescope:
```bash
composer require laravel/telescope
php artisan telescope:install
php artisan migrate
```
View performance insights by visiting /telescope.


9. Optional: Deploy Locally with Docker
Docker provides an optimized local development environment:

Install Docker.
Use Laravel Sail (a lightweight CLI for Docker)
```bash
composer require laravel/sail --dev
php artisan sail:install
```

Start the application:
```bash
./vendor/bin/sail up
```

By following these steps, you should see a significant improvement in the loading speed of your Laravel project on your phone via the local network. 





### NOTE2:
If some routes in your Laravel application are loading quickly on your PC but are slow or timing out when accessed from your phone, there could be several factors at play. Here are some potential causes and solutions to consider:

1. Network Issues
Wi-Fi vs. Mobile Data: If you're accessing the application over Wi-Fi on your phone, check the network speed. Sometimes, mobile data can be faster than a slow Wi-Fi connection.

Local Network Configuration: Ensure that your phone is connected to the same local network as your PC. If you're using a different network, it may lead to slower access times.

3. Server Performance
Resource Limitations: If your development server (Apache or Nginx) is running on a machine with limited resources (CPU, RAM), it may struggle to handle multiple requests, especially if you're running other applications simultaneously.

Check Server Load: Use tools like htop or top on your server to monitor CPU and memory usage. 
If the server is under heavy load, it may slow down response times.

5. Caching Issues
Browser Cache: Sometimes, the browser cache can affect loading times. Clear the cache on your phone's browser and try again.

Laravel Caching: If you have caching enabled in Laravel, ensure that the cache is not causing issues. You can clear the cache using:
```bash
php artisan cache:clear
php artisan route:clear
php artisan config:clear
```

4. Database Performance
Slow Queries: If the slow routes involve database queries, check if those queries are optimized. Use Laravel's query logging or tools like Laravel Debugbar to analyze query performance.

Database Connection: Ensure that your database connection is stable and not causing delays. If you're using a remote database, latency can be an issue.

6. Debugging and Logging
Check Logs: Look at the Laravel logs (storage/logs/laravel.log) for any errors or warnings that might indicate what is causing the slowdown.
Debugging Tools: Use tools like Laravel Debugbar to get insights into the performance of your application, including route execution times, database queries, and more.

7. Mobile Browser Limitations
Browser Differences: Different browsers may handle requests differently. Test the application on multiple browsers on your phone to see if the issue persists.

JavaScript and CSS: If the slow routes involve heavy JavaScript or CSS, ensure that these assets are optimized for mobile. Large files can slow down loading times.

9. API Response Times
API Calls: If your routes are making API calls, check the response times of those APIs. Slow API responses can lead to longer loading times on your phone.
Network Latency: If your application relies on external APIs, network latency can affect performance.

10. Testing with Different Devices
Device Performance: Test the application on different mobile devices to see if the issue is device-specific. Older devices may struggle with resource-intensive applications.

Emulators: Use mobile emulators to test how the application performs under different conditions.

10. Check for SSL Issues
If you're using HTTPS, ensure that your SSL certificate is correctly configured. Sometimes, SSL misconfigurations can lead to slow loading times.

By investigating these areas, you should be able to identify the cause of the slow loading routes on your phone. If the problem persists, consider providing specific details about the routes that are slow, any error messages you encounter, and the network conditions under which you're testing. This information can help in diagnosing the issue more effectively.



### NOTE3:
# How to setupcustom domain in local network
Example:
To access http://0.0.0.0:8000 as http://wsccharityconsortium.test/, you will need to perform a few steps to set up your local environment. Here's how you can do it:

1. Update Your Hosts File
You need to map the domain wsccharityconsortium.test to 127.0.0.1 (or 0.0.0.0, which is equivalent) in your hosts file.

Linux/Mac: Open a terminal and run:
```bash
sudo nano /etc/hosts
```

Windows: Open Notepad as an administrator and edit the file located at:
```bash
C:\Windows\System32\drivers\etc\hosts
```

Add the following line to the end of the file:
```bash
127.0.0.1 wsccharityconsortium.test
```

2. Configure Your Web Server
If you are using Apache, you need to create a virtual host configuration for wsccharityconsortium.test.

Create a new configuration file:
```bash
sudo nano /etc/apache2/sites-available/wsccharityconsortium.conf
```

Add the following configuration:
```bash
<VirtualHost *:80>
    ServerName wsccharityconsortium.test
    DocumentRoot /home/jbtechnix/Downloads/programmingandcoding/website/jbwebws>

    <Directory /home/jbtechnix/Downloads/programmingandcoding/website/jbwebwsc/>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/jbwebwsc_error.log
    CustomLog ${APACHE_LOG_DIR}/jbwebwsc_access.log combined

    ProxyPass / http://0.0.0.0:8000/
    ProxyPassReverse / http://0.0.0.0:8000/
</VirtualHost>
```

Enable the necessary modules: Make sure you have the proxy and proxy_http modules enabled:
```bash
sudo a2enmod proxy
sudo a2enmod proxy_http
```

Enable your new site configuration:
```bash
sudo a2ensite wsccharityconsortium.conf
```

Restart Apache:
```bash
sudo systemctl restart apache2
```

3. Access the Site
Now, you should be able to access your application by navigating to http://wsccharityconsortium.test/ in your web browser.

Notes:
Make sure that whatever service is running on 0.0.0.0:8000 is up and running.
If you are using a firewall, ensure that it allows traffic on port 80 (HTTP).
If you want to use HTTPS, you will need to set up SSL certificates and adjust the configuration accordingly.







### Accessing the custom domain from local network
To access the custom domain http://wsccharityconsortium.test/ on your phone, follow these steps:

1. Ensure Your Phone is on the Same Network
Make sure your phone is connected to the same local network (Wi-Fi) as the machine where your web server is running. This is essential because the custom domain is likely pointing to a local IP address (like 127.0.0.1 or 0.0.0.0), which is not accessible from outside that network.

2. Modify the Hosts File on Your Phone (if necessary)
If you want to use the custom domain on your mobile device without a DNS server, you will need to modify the hosts file. However, this is typically not straightforward on most mobile devices without rooting (Android) or jailbreaking (iOS). Instead, you can use one of the following methods:

For Android (Without Rooting)
Use a DNS App: Some apps can change DNS settings or allow you to set custom domains. Look for apps like "DNS Changer" or "DNS Override".

Browser Access: If your web server is accessible via the local IP address, you can directly enter the IP address in the browser on your phone.

For iOS
Using a DNS App: Similar to Android, you can use an app that allows you to change DNS settings or create local DNS entries.

Browser Access: Again, you can directly enter the local IP address of your server in Safari or another browser.

3. Accessing the Custom Domain
If you have set everything up correctly and your phone is on the same network as your server, you should be able to access the custom domain by:

Opening a Web Browser: Open a web browser on your phone (e.g., Chrome, Safari).
Entering the Custom Domain: Type http://wsccharityconsortium.test/ in the address bar and hit enter.

4. Use a Local DNS Server (Optional)
If you find modifying the hosts file cumbersome, you could set up a local DNS server on your network (like Pi-hole or dnsmasq) that can resolve wsccharityconsortium.test to the local IP address of your server. This way, any device connected to your network can resolve the custom domain without manual configuration.

5. Accessing from Outside Your Local Network
If you want to access http://wsccharityconsortium.test/ from outside your local network (e.g., using mobile data), you will need to:

Set Up Port Forwarding: Configure your router to forward requests on port 80 (HTTP) to the internal IP address of your web server.

Use a Public IP or Dynamic DNS: If your public IP address changes, consider using a dynamic DNS service to map a domain name to your changing IP.


To summarize, if you want to access http://wsccharityconsortium.test/ on your phone, ensure you are on the same network as your server, and either modify your hosts file or directly access it via the server's IP address. For external access, consider port forwarding and using a public IP or dynamic DNS.





### proudly made by johnboscocjt











