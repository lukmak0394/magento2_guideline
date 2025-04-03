# Magento 2 CLI Cheat Sheet

## General
```bash
php bin/magento --help              # List all available CLI commands
php bin/magento list                # List available commands with descriptions
php bin/magento help <command>     # Show help for a specific command
```

## Cache Management
```bash
php bin/magento cache:clean        # Clean cache types
php bin/magento cache:flush        # Flush cache storage
php bin/magento cache:status       # Show cache status
php bin/magento cache:enable       # Enable all cache types
php bin/magento cache:disable      # Disable all cache types
```

## Index Management
```bash
php bin/magento indexer:reindex    # Reindex all indexers
php bin/magento indexer:status     # Show status of indexers
php bin/magento indexer:reset      # Reset all indexers
```

## Setup & Upgrade
```bash
php bin/magento setup:upgrade                   # Run database upgrades
php bin/magento setup:di:compile                # Run dependency injection compilation
php bin/magento setup:static-content:deploy     # Deploy static content
php bin/magento setup:install                   # Install Magento
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
```

## Module Management
```bash
php bin/magento module:status       # Show status of all modules
php bin/magento module:enable <Module_Name>     # Enable a module
php bin/magento module:disable <Module_Name>    # Disable a module
php bin/magento module:uninstall <Module_Name>  # Uninstall a module
```

## Maintenance Mode
```bash
php bin/magento maintenance:enable     # Enable maintenance mode
php bin/magento maintenance:disable    # Disable maintenance mode
php bin/magento maintenance:status     # Check maintenance mode status
```

## Admin User
```bash
php bin/magento admin:user:create      # Create new admin user
```

## Cron Jobs
```bash
php bin/magento cron:run               # Run cron jobs
php bin/magento cron:install           # Install cron jobs
```

## Store Configuration
```bash
php bin/magento config:set <path> <value>           # Set configuration value
php bin/magento config:show <path>                  # Show configuration value
php bin/magento config:delete <path>                # Delete configuration value
```

## Logs
```bash
php bin/magento setup:cron:run         # Run all scheduled cron jobs manually
```

## Other Useful Commands
```bash
php bin/magento info:adminuri          # Show admin URI
php bin/magento setup:uninstall        # Uninstall Magento
php bin/magento deploy:mode:show       # Show current deploy mode
php bin/magento deploy:mode:set <mode> # Set deploy mode (developer/production)
php bin/magento admin:user:create # Create admin user 
	--admin-user="USER_USERNAME" 
	--admin-password="USER_PASSWORD" 
	--admin-email="USER_EMAIL" 
	--admin-firstname="USER_FIRSTNAME" 
	--admin-lastname="USER_LASTNAME
```
