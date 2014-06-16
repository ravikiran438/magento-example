Magento v1.9.0.1 on OpenShift
====================

This git repository creates a Magento installation on OpenShift.

Sample data is populated and the application configured automagically.

Running on OpenShift
----------------------------

Create an account at http://www.openshift.com/

Create a php-5.4 + mysql 5.5 application based on this repo's code (you can call your application whatever you want)

    rhc app create $appname php-5.4 mysql-5.5 phpmyadmin cron

The sample data tarball provided with Magento v1.9.0.1 is more than 400MB which almost exceeds 1GB of free space quota after extraction. So you need to upgrade your gear to atleast another 1GB for this application to be built and deployed successfully. 

Add this upstream Magento repo

    cd $appname 
    git remote add upstream -m master git://github.com/ravikiran438/magento-example.git
    git pull -s recursive -X theirs upstream master
    # note that the git pull above can be used later to pull updates to Magento
    
Then push the repo upstream

    git push

That's it, you can now checkout your application at:

    http://$appname-$yournamespace.rhcloud.com

Default admin credentials: username _admin_ password _OpenShiftAdmin123_.

### Post-installation details

After the installation it is important to change the admin password and other Magento configurations properly. Log in to 

    http://$appname-$yournamespace.rhcloud.com/admin

using the provided credentials and check all system settings, for example:

 * System > My Account
 * System > Configuration > General > Countries Options
 * System > Configuration > General > Locale Options
 * System > Configuration > Admin
 * System > Configuration > System