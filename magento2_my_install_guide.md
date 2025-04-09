# Magento 2 Install Guide

> **Note**: This guide is for Magento **2.4.7**

---

## 1. Software Requirements

- Windows 10 or 11 (64-bit)
- PHP 8.2 / 8.3
- MariaDB 10.6
- Apache 2.4 with `mod_rewrite`
- Elasticsearch 7.17 or OpenSearch 2.x
- Composer 2.7 / 2.8

---

## 2. Steps to Install

1. **Sign in and generate access keys** on the [Magento Marketplace](https://commercemarketplace.adobe.com/)
2. **Download and install XAMPP**
   - Required PHP extensions (in `php.ini`):
     ```ini
     extension=gd
     extension=soap
     extension=xls
     extension=sockets
     extension=sodium
     extension=zip
     extension=gd
     ```
   - Recommended PHP configuration:
     ```ini
     max_execution_time=18000
     max_input_time=1800
     memory_limit=4G
     ```
3. **Download and install Composer**
4. **Download and install Elasticsearch**
5. **Create a database** in phpMyAdmin
6. **Download Magento using Composer** into your project directory under `/htdocs/`:
   ```bash
   composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
   ```
7. **Set up Virtual Hosts**
   - Edit: `C:\Windows\System32\drivers\etc\hosts`
     ```
     127.0.0.1 magento.local
     ```
   - Add to `vhosts.conf`:
     ```apache
     <VirtualHost *:80>
         ServerAdmin your-email@example.com
         DocumentRoot "C:/xampp/htdocs/magento2/pub"
         ServerName magento.local
         ErrorLog "logs/magento.local-error.log"
         CustomLog "logs/magento.local-access.log" common
     </VirtualHost>
     ```
   - Restart Apache
8. **Install Magento** using Command Prompt:
   ```bash
   php bin/magento setup:install \
     --base-url="http://magento.local/" \
     --db-host="localhost" \
     --db-name="magento2" \
     --db-user="root" \
     --db-password="your_password" \
     --admin-firstname="admin" \
     --admin-lastname="user" \
     --admin-email="admin@example.com" \
     --admin-user="admin" \
     --admin-password="Admin123" \
     --language="en_US" \
     --currency="USD" \
     --timezone="America/Chicago" \
     --use-rewrites="1" \
     --backend-frontname="admin" \
     --search-engine="elasticsearch7" \
     --elasticsearch-host="localhost" \
     --elasticsearch-port=9200
   ```

---

## 3. Possible Issues

1. **CSS and JS not loading properly**
   - Edit: `vendor/magento/framework/View/Element/Template/File/Validator.php`
   - In the method `isPathInDirectories`, replace:
     ```php
     strpos($realPath, $directory)
     ```
     with:
     ```php
     strpos($path, $directory)
     ```
     OR redefine:
     ```php
     $realPath = str_replace('\\', '/', $this->fileDriver->getRealPath($path));
     ```
2. **No login form in admin dashboard**
   - Edit: `vendor\magento\framework\Image\Adapter\Gd2.php`
   - In the method `validateURLScheme`, add:
     ```php
     && !file_exists($filename)
     ```
     at the end of the `if` condition
3. **Two-factor authentication in admin panel**
   - Disable it with:
     ```bash
     php bin/magento module:disable Magento_AdminAdobeImsTwoFactorAuth Magento_TwoFactorAuth
     ```

---

## 4. Sources

1. https://commercemarketplace.adobe.com/
2. https://www.mgt-commerce.com/tutorial/nstalling-magento-2-on-windows/
3. https://www.thecoachsmb.com/6-steps-to-install-magento2-on-xampp-windows-using-composer/#Step-5-Install-sample-data-for-Magento-24
4. https://magento.stackexchange.com/questions/251924/invalid-template-file-magento2-3-0
