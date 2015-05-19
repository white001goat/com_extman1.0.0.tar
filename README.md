Please note that the following versions, at the time of this writing, are the latest working and compatible Joomla and Nooku 
releases that work with the current CCK. Of course before we continue the installation, we will need a working "stack" 
\(eg. LAMP, WAMP, MAMP\)

While one might choose to use a standard Vagrant virtual machine distribution to simplify and standardize the "stack" all of
your developers and clients maybe using \(e.g. joomlatools\) LINK, one can always manually install their environments with the 
following three components:

    * Apache Web Server VERSION/LINK
    * PHP 5.5.14 which employs it's own distributed Zend Engine v2.5.0 LINK
    * MySQL VERSION/LINK

Install Joomla 3.3.6 (https://github.com/joomla/joomla-cms/releases/download/3.3.6/Joomla_3.3.6-Stable-Full_Package.zip)
Install Nooku 1.0.0 via com_extman

The step of installing Nooku seems to be the Achillies heal in this whole process. Nooku, it's marketing name, within the code is 
known as Koowa. As if this was not vague enough, the compatible version for this installation, is difficult to find for download. 

License issues? Screenshot of installation page on administrator backend, adding a component from an upload com_extman1.0.0.tar.


Now that we have our basic Joomla installation and have written over some of the packages by installing Nooku over the top of it, 
we can now add the packages from the CCK distribution in consideration.


```git clone ssh://repository/atSomeProjectDistribution.git```

```git reset --hard HEAD```

If your "stack" environment lacks a distribution of Composer (http://getcomposer.com) LINK/CHECK, we will need to install this PHP based 
package dependency manager. For proper installation of composer, please do consider reading more on their website. For now 
let us assume that you followed the installation as they advise, and you have moved your downloaded composer.phar file \(the 
binary compressed executable, written also by chance in PHP\) into a known path directory, having renamed it to composer, you should 
be able to follow the command instructions below. Otherwise, replace the word "composer" with "php composer.phar".
 
Now, from our previous download of the git repository, we should have a composer.json file in the Joomla website's root directory. A 
good step for safety measure is to test your composer.json for errors. This can be done with:
    
    ```$ composer validate```
    
    ```./composer.json is valid```

composer install 
