Subdomains

Implements the use of separate bases for subdomains.

The settings used in sugar_config:
domain_level - domain level in url; for example, for url admin.example.com subdomain admin is at level 3
domain_db_prefix - prefix the name of the database when creating a new database
It is necessary to fill in correctly (with a sub-domain admin) in /config.php
* site_url
* host_name
fromaddress from email settings
Then these settings will be copied with the replacement of the domain.

Specific domain settings are stored in domains/<домен>/config.php.
That is, the settings sugar_config connect in the next sequence
* config.php
* config_override.php
domains/<домен>/config.php

'langpack' packages are installed only in the Admina domain, as they rewrite config.php.
In case the config of the subdomain rewrites the main config.php, it is recommended to duplicate
Settings of the Admin base, folders, etc. in domains/admin/config.php.

There are upgrade unsafe files.
There are files copied from SuiteCRM 7.6.4 and reworked in modules/Domains/install/

Running commands for each domain:
php domains-foreach.php <shell_command>
In the text of the sub-line, the @@DOMAIN@@ is replaced in the domain name
For example
php domains-foreach.php "spm repair | spm dbquery > domains/@@DOMAIN@@/repair.log"

At the same time, the domain name is available through the SUGAR_DOMAIN's environment variable.

Running crowns for each domain:
php domains-foreach.php "php domains-precron.php && php cron.php && php domains-postcron.php"

Running a team for one domain:
php domains-with.php <domain> <shell_command>
For example
php domains-with.php dom1 "spm sbstatus"
