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














