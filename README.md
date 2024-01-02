# Awesome-website
#Choose or create a directory where your website files will reside. Let's assume it's Awesome website
#Create a simple HTML file, e.g., index.html, in your chosen directory.
<!-- /var/www/awesomeweb/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Awesome Web</title>
</head>
<body>
    <h1>Welcome to Awesome Web!</h1>
    <p>This is a simple example website.</p>
</body>
</html>
# installed Nginx
sudo apt-get update
sudo apt-get install nginx
#Create a new configuration file for your site. Let's create a file named awesomeweb in the Nginx sites-available directory.
#Add the following configuration. Update the server_name to your chosen DNS name.
sudo nano /etc/nginx/sites-available/awesomeweb
server {
    listen 80;
    server_name awesomeweb;

    root /var/www/awesomeweb;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
#Enable the Site and Restart Nginx
sudo ln -s /etc/nginx/sites-available/awesomeweb /etc/nginx/sites-enabled/
#Test the Nginx configuration and restart Nginx
sudo nginx -t
sudo systemctl restart nginx
#Modify Hosts File (Simulating DNS
sudo nano /etc/hosts
#open website and Test Your Website:
127.0.0.1 awesomeweb

#Quest-2
pip install requests
pip install prettytable
#Now, create a Python script (check_subdomains.py) with the following content

import requests
import time
from prettytable import PrettyTable

def check_subdomains(subdomains):
    table = PrettyTable()
    table.field_names = ["Subdomain", "Status"]

    while True:
        for subdomain in subdomains:
            url = f"http://{subdomain}"
            try:
                response = requests.get(url)
                if response.status_code == 200:
                    status = "Up"
                else:
                    status = "Down"
            except requests.ConnectionError:
                status = "Down"

            table.add_row([subdomain, status])

        # Clear the console (works on Unix-based systems and Windows)
        print("\033c")
        print(table)

        # Wait for one minute before checking again
        time.sleep(60)

if __name__ == "__main__":
    # Add your subdomains here
    subdomains_to_check = ["subdomain1.example.com", "subdomain2.example.com", "subdomain3.example.com"]

    check_subdomains(subdomains_to_check)
#Replace the subdomains_to_check list with your actual subdomains. The script will continuously check the status of each subdomain every minute and display the results in a table format on the console.

