# Magento 2 install guide

Please note that this is for magento **2.4.7**

### 1. Software Requirements
-   Windows 10 or 11 (64-bit)
-   PHP 8.2 / 8.3
-   MariaDB 10.6
-   Apache 2.4 with mod_rewrite
-   Elasticsearch 7.17 or OpenSearch 2.x
-   Composer 2.7 / 2.8

### 2. Steps to install
1. Sign in and generate access keys on [Magento marketplace](https://commercemarketplace.adobe.com/)
2. Download and install **Xampp**
	- **php.ini** required extensions: 
	```
	extension=gd
	extension=soap
	extension=xls
	extension=sockets
	extension=sodium
	extension=zip
	extension=gd
	```
	- recommended php configuration (set in **php.ini**):
	```
	max_execution_time=18000
	max_input_time=1800
	memory_limit=4G
	```
3. Download and install **Composer**
4. Download and install **Elasticsearch**
5. Create database in **phpmyadmin**
6. Download magento using composer into your magento project dir in `/htdocs/`
	- ```composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .```
7. Set up virtual hosts:
	- `C:\Windows\System32\drivers\etc\hosts` 
	- Add line `127.0.0.1 magento.local`
	- To `vhosts.conf` add  ```<VirtualHost *:80>  
    ServerAdmin your-email@example.com  
    DocumentRoot "C:/xampp/htdocs/magento2/pub"  
    ServerName magento.local  
    ErrorLog "logs/magento.local-error.log"  
    CustomLog "logs/magento.local-access.log" common  
</VirtualHost>```
	- Restart apache
7. Install magento with command prompt
php bin/magento setup:install   
--base-url="http://magento.local/"   
--db-host="localhost"   
--db-name="magento2"   
--db-user="root"   
--db-password="your_password"   
--admin-firstname="admin"   
--admin-lastname="user"   
--admin-email="admin@example.com"   
--admin-user="admin"   
--admin-password="Admin123"   
--language="en_US"   
--currency="USD"   
--timezone="America/Chicago"   
--use-rewrites="1"   
--backend-frontname="admin"   
--search-engine="elasticsearch7"   
--elasticsearch-host="localhost"   
--elasticsearch-port=9200

### 3. Possible issues
1. CSS and JS not loading properly after install
	- Open `vendor/magento/framework/View/Element/Template/File/Validator.php`
	- Find method `isPathInDirectories`
	- Replace `strpos($realPath, $directory)` with `strpos($path, $directory` OR define `$realPath` like this: `$realPath = str_replace('\\', '/', $this->fileDriver->getRealPath($path));`
2. No login form in admin dashboard
	- Open`vendor\magento\framework\Image\Adapter\Gd2.php`
	- Find method `validateURLScheme` 
	- Add `&& !file_exists($filename)` at end of if statement
3. Two factor auth needed admin panel
	- Disable `php bin/magento module:disable Magento_TwoFactorAuth`

### 4. Soruces:
1. https://commercemarketplace.adobe.com/
2. https://www.mgt-commerce.com/tutorial/nstalling-magento-2-on-windows/
3. https://www.thecoachsmb.com/6-steps-to-install-magento2-on-xampp-windows-using-composer/#Step-5-Install-sample-data-for-Magento-24
4. https://magento.stackexchange.com/questions/251924/invalid-template-file-magento2-3-0




