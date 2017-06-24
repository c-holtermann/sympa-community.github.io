Upgrading to latest version of Sympa
====================================

Upgrading from earlier Sympa 6.2.x
----------------------------------

After release of 6.2, several changes on templates are made. Especially, on 6.2.18, web templates for shared document repository and list configuration edit form broke backward compatibility in exchange for bug fixes.

If you have customized templates with earlier version, you should check if web interface will work crrectly after upgrading, and reapply customization to new templates as necessity.

Upgrading from Sympa 6.1.x or earlier
-------------------------------------

Several changes in Sympa 6.2 require to perform specific operations when upgrading. Here is the ordered list of operations to perform.

The changes are the following:

  - sympa.conf and wwsympa.conf are merged. wwsympa.conf is no longer used,

  - sympa.conf is now located in a sympa/ sub-directory,

  - bulk spool is moved from database to file system,

  - formalism for storing messages sent from the web interface has changed

  - custom actions must now be located in a dedicated `custom_actions/` directory,

  - Sympa skin was changed.

  - init script is changed, becausee some Sympa daemons have been renamed. Check your configure optins to make sure the init script ends up in the correct location for your operating system.

Here is the list of commands to run:

``` code
sympa_wizard.pl --check # Update CPAN dependencies
sympa.pl --upgrade_config_location # move existing configs to /etc/sympa/ directory
sympa.pl --upgrade # merge sympa.conf and wwsyamp.conf
upgrade_bulk_spool.pl # move messages stored in database to filesystem
upgrade_send_spool.pl # move messages sent through web interface to the new formalism.
```

  - For all your **custom action** templates, move them to **etc/custom\_actions** directory.
  - **After the upgrade, the following changes will have occured:**

      - **sympa.conf** will have need copied to sympa.conf.upgrade._dd_._Month_._yyyy_-_hh_._mm_._ss_ The sympa.conf remaining will have been stripped of any 'color\_\*' parameters, to prevent you from having a messed up web interface \* any **robot.conf** will have had the same treatment as sympa.conf (copy, then stripped of color\_* parameters).

      - any customized "**web\_tt2**" directory (either in etc/ or in etc/_robot_/) will have been renamed "**web\_tt2.upgrade._dd_._Month_._yyyy_-_hh_._mm_._ss_**". Indeed, as most of the Sympa templates have been changed for the new skin, your customizations could not be compliant to the new web interface. You should see how to reintroduce them to the new templates.

      - Finally, as some Sympa binaries have been renamed, your sympa init script will have been updated. Please make sure your configure options have been correctly set, so that this script ends up in the correct location.

