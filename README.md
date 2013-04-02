Introspy
========

Blackbox tool to help understand what an iOS application is doing at runtime
and assist in the identification of potential security issues.


Description
-----------

Introspy comprises two separate modules: a tracer and an analyzer. 

The tracer component can be installed on a jailbroken device and dynamically
configured to hook security-sensitive iOS APIs at run-time. The tool records
details of relevant API calls made by the application, including function
calls, arguments and return values and persists them in a database.
Additionally, the calls can optionally be sent to the Console for real-time
analysis.

The Introspy analyzer can then be used to analyze a database generated by the
tracer, and generate HTML reports containing the list of logged function calls
as well as a list of potential vulnerabilities affecting the application.


Introspy Tracer
---------------

Users should first download the right pre-compiled Debian package:
-  https://www.dropbox.com/s/otag5l99b0slbbn/com.isecpartners.introspy_0.2.0-14_iphoneos-arm.deb?dl=1

### Dependencies

The tracer will only run on a jailbroken device. Using Cydia, make
sure the following packages are installed:
- dpkg
- MobileSubstrate
- PreferenceLoader
- Applist

### How to install

Download and copy the Debian package to the device; install it:  

    dpkg -i <package.deb>

Respring the device:

    killall -HUP SpringBoard

There should be a new menu in the device's Settings where you can
enable the extension.

Finally, kill and restart the App you want to monitor.

### How to uninstall

    dpkg -r com.isecpartners.introspy


Introspy Analyzer
-----------------

The analyzer requires Python 2.6 or 2.7.

### Usage

The Introspy tracer should be first used on the application to be tested. Then, 
the tester has to recover the .db file containing the data generated by the tracer,
which will be located on the device :
- For system and Cydia applications:  /var/mobile/
- For store/regular applications:     /User/Applications/<App ID>/

Then introspy DB can then be fed to any SQLite reader or the analyzer in order
to generate an HTML report.


Building the Tracer
-------------------

Most users should just download and install the pre-compiled Debian 
package.
The build requires the Theos suite to be installed; 
see http://www.iphonedevwiki.net/index.php/Theos/Getting_Started .
You first have to create a symlink to your theos installation:

    ln -s /opt/theos/ theos

Then, the package can be built using:

    make package


License
-------

See ./LICENSE.


Authors
-------

Tom Daniels
Alban Diquet
