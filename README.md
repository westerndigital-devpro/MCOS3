# My Cloud OS3 NAS SDK
----

## CONTENTS
1. [INTRODUCTION](#introduction)
2. [APPS PACKAGE SDK V2.0](#apps-package-sdk-v20)
3. [GETTING STARTED: USING MKSAPKG](#getting-started-using-mksapkg)
4. [WRITE YOUR OWN APKG.RC FILE](#write-your-own-apkgrc-file)
5. [APPS PACKAGE NAMING RULES AND HEADER DEFINITION](#apps-package-naming-rules-and-header-definition)
6. [WHEN WILL SHELL SCRIPT FILES BE CALLED](#when-will-shell-script-files-be-called)
7. [APP SERVER](#app-server)
8. [SAMPLE APP PACKAGE WITHOUT WEB UI](#sample-app-package-without-web-ui)
9. [CREATE WEB PAGE](#create-web-page)
10. [MULTI-LANGUAGE SUPPORT](#multi-language-support)
11. [DOWNLOADS](#downloads)
----

## INTRODUCTION
Apps Package is a small package management system that designed for the My Cloud OS3 NAS devices. We refer to Add-ons in the document as Apps. As you can see by the below image, the UI refers to Add-ons as Apps. The SDK v2.0 provides basic functions to control packages. These controls are: install, remove, start, and stop. You only need to use the templates that are contained in the SDK, which are just simple shell scripts to create an App quickly and easily without writing complex programs.

[VIEW SDK](./SDK/README.md)

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image002.jpg)

[^](#contents)
---

## APPS PACKAGE SDK V2.0

The Apps Package SDK v2.0 includes [MKSAPKG](https://developer.westerndigital.com/develop/wd/sdk.html#downloads), a tool that wraps your app into an Apps Package that can be installed on a My Cloud OS3 NAS device. It also includes a sample that guides you in creating your own app.

[^](#contents)
---

## GETTING STARTED: USING MKSAPKG

mksapkg is a tool that helps you create your own app for My Cloud OS3 NAS devices. It is included in the Apps Package SDK v2.0, and we provide the executable binary to run your app on our system. Users must install libxml2 and GNU “tar” in their Linux system to run mksapkg.

<pre>Usage: mksapkg -E -s -m [module_name]</pre>

The parameters you can use when running mksapkg in a command line are as follows:

<table class="table table-bordered">
<tbody><tr><th><b>Parameter</b>&nbsp; &nbsp; &nbsp;</th>
<th><b>Description</b></th>
</tr><tr><td>-E</td>
<td>auto-start application after install</td>
</tr><tr><td>-s</td>
<td>create apkg.sign for security check</td>
</tr><tr><td>-m</td>
<td>create application for specific NAS device</td>
</tr></tbody></table>

Note: each device requires its own app file. Please create a separate apps package for each device if your app is supported on multiple OS3 NAS devices. When you specify the [module_name] while packaging the app, use the following values for each supported NAS device:

<table>
  <tbody>
    <tr>
      <td><b>module_name</b></td>
      <td><b>NAS device</b></td>
    </tr>
    <tr>
      <td>MyCloudEX2Ultra</td>
      <td><a href="https://www.wd.com/products/network-attached-storage/my-cloud-expert-series-ex2-ultra.html" target="_blank">WD My Cloud EX2 Ultra</a></td>
    </tr><tr><td>WDMyCloudEX4100</td>
    <td><a href="https://www.wd.com/products/network-attached-storage/my-cloud-ex4100.html" target="_blank">WD My Cloud EX4100</a></td>
    </tr><tr><td>MyCloudPR2100</td>
    <td><a href="https://www.wd.com/products/network-attached-storage/my-cloud-pr2100.html" target="_blank">WD My Cloud PR2100</a></td>
    </tr><tr><td>MyCloudPR4100</td>
    <td><a href="https://www.wd.com/products/network-attached-storage/my-cloud-pr4100.html" target="_blank">WD My Cloud PR4100</a></td>
    </tr>
  </tbody>
</table>

If you are missing the xml2 library, use the following for Fedora:

<pre>$ yum -y install libxml2 libxml2-devel</pre>

[^](#contents)
---

## WRITE YOUR OWN APKG.RC FILE

All string characters cannot contain spaces except the description field:

<pre>
Package: utelnetd (the max length is 64)
Section: Apps
Version: 1.00 (the max length is 32)
Packager: WD (the max length is 32)
Email: support@wdc.com (the max length is 64)
Homepage: http://support.wdc.com (the max length is 64)
Description: This is a simple demonstration to wrapped telnet daemon. (the max length is 256)
AddonShowName: utelnetd (the max length is 64)
Icon: utelnetd.png
AddonIndexPage:
AddonUsedPort:
InstDepend:
InstConflict:
StartDepend:
StartConflict:
CenterType:
UserControl:
MinFWVer:
MaxFWVer:
IndividualFlag:
</pre>

Note: the string values you add to apkg.rc will be used to build your app's entry in the App Catalog [WHEN YOU SUBMIT YOUR APP](https://developer.westerndigital.com/develop/wd/submit-app-new-mcos3on.html):

<table cellpadding="1" cellspacing="0">
  <tbody>
    <tr><td><b> APKG.RC File </b></td>
      <td> <b>App Pages</b></td>
    </tr><tr><td> AddonShowName            </td>
    <td> App name</td>
    </tr><tr><td> Version</td>
    <td> App version</td>
    </tr><tr><td> Description</td>
    <td> App description as it will appear in the App Catalog <br />
    </td>
    </tr>
  </tbody>
</table>

Here are the definitions of variables in apkg.rc:

### About UserControl

UserControl is used to control the App visibility. Based on the parameter, the App could be visible on admin account only or both admin and user accounts.

If the UserControl value is “1”, only the admin can see the app.

Example:

Dropbox is set to “1”, and normal user can’t see the app.

<b>Login by Admin:</b>

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image003.jpg)

<b>Login by User:</b>

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image004.jpg)

### About CenterType

If the CenterType value is “1”, and the setting page will build-in.

The CentherType value is “0”, and the setting page will pop-out.

<b>Setting page build-in:</b>

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image005.jpg)

<b>Setting page pop-out:</b>

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/Picture1.png)

### About MinFWVer &amp; MaxFWVer

<b>MinFWVer &lt;= Current firmware &lt;= MaxFWVer</b>

<b>Format: 1.xx.xx.xx (support 6 token)</b>

If the MaxFWVer or MinFWVer is empty and it won’t check the min version or max version. The version limitation will check the current firmware version when installing apps.

Example:

<pre>
MinFWVer: 1.03.00
MaxFWVer: 1.04.00
</pre>

If the current firmware version is 1.02.00 or 1.05.00, App installation will return a failure.

### About IndividualFlag

WebUI will show some notice information for Apps. If the App is completed by ALPHA, we will hide the information.

Note: Support for each App should be obtained through the developer directly. The App's description in the WebUI shows support contact information.

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image006.jpg)

### About AddonIndexPage

If the “AddonIndexPage” is empty, the App will not provide a setting page.

The WebUI will still show the “configure” button, but it will not work.

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image007.jpg)

Dependency &amp; conflict rules defined by the App SDK v2.0:

<pre>
Package:       A
…
InstDepend:    B
InstConflict:  C
StartDepend:   D
StartConflict: E, F

_   App A can't install when App B is not installed
_   App A can't install when App C is installed
_   App A can't enable when App D is not enabled
_   App A can't enable when App E or F is enabled
</pre>

### About Version

Please set your version string value as <b>xx.xx</b> (ex: 0.0, 10.1, 1.10, 99.99 in whole numbers)

When running mksapkg, it will parse apkg.rc to create apkg.xml, and apkg.xml will be used by the App Server to get information about the installed App.

<b>Sample:</b>

<pre>
&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;
&lt;config&gt;
&lt;apkg&gt;
    &lt;item&gt;
    &lt;procudt_id&gt;0&lt;/procudt_id&gt;
    &lt;custom_id&gt;20&lt;/custom_id&gt;
    &lt;model_id&gt;0&lt;/model_id&gt;
    &lt;user_control&gt;0&lt;/user_control&gt;
    &lt;center_type&gt;0&lt;/center_type&gt;
    &lt;name&gt;utelnetd&lt;/name&gt;
    &lt;show&gt;utelnetd&lt;/show&gt;
    &lt;enable&gt;0&lt;/enable&gt;
    &lt;version&gt;1.00&lt;/version&gt;
    &lt;date&gt;20130301&lt;/date&gt;
    &lt;inst_date&gt;&lt;/inst_date&gt;
    &lt;path&gt;&lt;/path&gt;
    &lt;ps_name&gt;&lt;/ps_name&gt;
    &lt;url&gt;&lt;/url&gt;
    &lt;url_port&gt;&lt;/url_port&gt;
    &lt;apkg_version&gt;WD&lt;/apkg_version&gt;
    &lt;packager&gt;WD&lt;/packager&gt;
    &lt;email&gt;support@wdc.com&lt;/email&gt;
    &lt;homepage&gt;http://support.wdc.com&lt;/homepage&gt;
    &lt;inst_depend&gt;&lt;/inst_depend&gt;
    &lt;inst_conflict&gt;&lt;/inst_conflict&gt;
    &lt;start_depend&gt;&lt;/start_depend&gt;
    &lt;start_conflict&gt;&lt;/start_conflict&gt;
    &lt;description&gt; This is a simple demonstration to wrapped telnet daemon.&lt;/description&gt;
    &lt;icon&gt;utelnetd.png&lt;/icon&gt;
    &lt;MinFWVer&gt;&lt;/MinFWVer&gt;
    &lt;MaxFWVer&gt;&lt;/MaxFWVer&gt;
    &lt;/item&gt;
&lt;/apkg&gt;
&lt;/config&gt;
</pre>

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image008.jpg)

Notes:

- The name of the directory where mksapkg is run from must match the app name. If not, app installation will fail.

- The app name is from “package name” in the apkg.rc file.

- Because mksapkg will compress the current directory when making the app, apkg will get app name which is from apkg.rc and use the name to check. If the app name doesn’t match with the directory name, app installation will fail.

### Shell script files

<b>preinst.sh:</b> This script is used to pre-run some commands if needed, or for user to back up their configuration files to other places such as: /tamp, /var/tmp or any directory on your hard drive before installing an App.

<b>install.sh:</b> Will copy files and install App to an appropriate folder.

<b>remove.sh:</b> Will remove the installed App from hard drive.

<b>init.sh:</b> Will create necessary symbolic links of installed App before being executed (we suggest creating the symbolic link to /usr/bin or /usr/sbin). If necessary, restore the configuration files backed up through preinst.sh back to the App installation directory.

<b>clean.sh:</b> Will remove all links or files that created by init.sh.

<b>start.sh:</b> Will start App daemon.

<b>stop.sh:</b> Will stop App daemon.
---

## APPS PACKAGE NAMING RULES AND HEADER DEFINITION

### Apps Package Naming Rules

Ex: WDMyCloudEX4 utelnetd Package v1.00_03012013

### Apps Package File Blocks

<table cellpadding="1" cellspacing="0">
  <tbody><tr><td style="text-align: center;"><h5>        apkg header       </h5>
    </td>
    </tr><tr><td style="text-align: center;"><h5>      Module tar file     </h5>
    </td>
    </tr></tbody></table>

### Header structure definition

<pre>
typedef struct _APKG_HEADER_
{
char           ah_magic_num[MAGIC_NUM_LEN];
char           ah_module_name[APKG_64_LEN];
char           ah_version[APKG_32_LEN];
int            ah_apkg_version;
int            ah_product_id;
int            ah_custom_id;
int            ah_model_id;
char           ah_reserve[64];
unsigned long  ah_checksum;
unsigned long  ah_length;
} APKG_HEADER, *APKG_HEADER_ID;
</pre>

Header magic number definition: the last byte of magic number must be <b>0x5a</b> in App SDK v2.0

<pre>
WDMyCloudEX4: {0x4c,0x69,0x67,0x68,0x74,0x6e,0x69,0x5a}
</pre>
---

## WHEN WILL SHELL SCRIPT FILES BE CALLED

When the Web UI uploads an App package, it is installed to:

<pre>
Example : module name is (MNAME) = utelnetd
default install path: (INST_PATH) = /mnt/HD/HD_a2/Nas_Prog/$MNAME
default upload path: (UPLOAD_PATH) = /mnt/HD/HD_a2/Nas_Prog/_install
</pre>

The install and upload path is scanned dynamically by the App server when daemon is initiated.

When installing a new App, the following shell script will be called:

<pre>
$UPLOAD_PATH/install.sh $UPLOAD_PATH $INST_PATH
$INST_PATH/init.sh $INST_PATH
</pre>

When removing an App, the following shell script will be called:

<pre>
$INST_PATH/stop.sh
$INST_PATH/clean.sh
$INST_PATH/remove.sh $INST_PATH
</pre>

When enabling an App, the following shell script will be called:

<pre>
$INST_PATH/start.sh
</pre>

When disabling an App, the following shell script will be called:

<pre>
$INST_PATH/stop.sh
</pre>

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image007.jpg)

When re-installing an App, the following shell script will be called:

<pre>
$INST_PATH/stop.sh
$INST_PATH/clean.sh
$INST_PATH/preinst.sh $INST_PATH
$INST_PATH/remove.sh $INST_PATH
$UPLOAD_PATH/install.sh $UPLOAD_PATH $INST_PATH
$INST_PATH/init.sh $INST_PATH
</pre>

When your app has its own configure file settings, you need to backup these files to other place in preinst.sh script file and copy files back in init.sh. Because remove.sh will remove all configuration files of this App on the hard disk and reinstall it in install.sh. Beware of incorrect shell script files which may cause the system to crash. For example, without the remove link from hard drive correctly, it may cause the system to format hard drive failure due to hard drive can't be un-mounted.

[^](#contents)
---

## APP SERVER

- The App Server will scan all volume to find out the installed Apps and enable it, if necessary
- The App Server will control and maintain installed database of Apps
- Apps Server will provide interface to run shell script file from Web GUI

The main purpose of Apps SDK v2.0 is implemented the App dependencies and configuration check.

[^](#contents)
---

## SAMPLE APP PACKAGE WITHOUT WEB UI

Prepare the necessary binaries of your application, and create a folder name that is the same name as the Package field in the apkg.rc file.

<pre>
$ ls -R
.:
apkg.rc  bin  clean.sh  init.sh  install.sh  preinst.sh  remove.sh  start.sh  stop.sh

./bin:
utelnetd
</pre>

<b>Create your own apkg.rc file</b>

<pre>
Package:            utelnetd
Version:            1.00
Packager:           WD
Email:              support@wdc.com
Homepage:           http:// support.wdc.com
Description:        This is a simple demonstration to wrapped telnet daemon.
Icon:               utelnetd.png
AddonShowName:      utelnetd
AddonIndexPage:
AddonUsedPort: 
InstDepend:
InstConflict: 
StartDepend: 
StartConflict:
CenterType:
UserControl:
MinFWVer:
MaxFWVer:
</pre>

<b>Write preinst.sh</b>

<pre>
#!/bin/sh

path_src=$1
path_des=$2
#we do nothing here for utelnetd
</pre>

<b>Write install.sh</b> (most apps will use this example)

<pre>
#!/bin/sh

path_src=$1
path_des=$2
mv $path_src $path_des
</pre>

<b>Write remove.sh</b> (most apps will use this example)

<pre>
#!/bin/sh

path=$1
rm -f /usr/bin/utelnetd 2&gt; /dev/null
rm -f /var/www/utelnetd &gt;/dev/null
rm -rf $path
</pre>

<b>Write init.sh</b>

<pre>
#!/bin/sh

path=$1

#create link
ln -s $path/sbin/utelnetd /usr/bin/utelnetd
ln -s $path/var/www/utelnetd /var/www

#cmd on pre-install
idx=0
while [ $idx -lt 7 ]; do
    mknod /dev/ptyp$idx c 2 $idx 2&gt;/dev/null
    mknod /dev/ttyp$idx c 3 $idx 2&gt;/dev/null
    idx=`expr $idx + 1`
done
</pre>

<b>Write clean.sh</b>

<pre>
#!/bin/sh

#remove link
rm -f /usr/bin/utelnetd  2&gt; /dev/null
rm -f /var/www/utelnetd &gt;/dev/null
rm -f /dev/ttyp*
rm -f /dev/ptyp*
</pre>

<b>Write start.sh</b>

<pre>
#!/bin/sh

#start daemon
utelnetd -d
</pre>

<b>Write stop.sh</b>

<pre>
#!/bin/sh

#stop daemon
killall utelnetd
</pre>

<b>Create Apps package using mksapkg</b>

<pre>
[hostname ~ /mksapkg/utelnetd]$ ls
apkg.rc  bin  clean.sh  init.sh  install.sh  preinst.sh  remove.sh  start.sh  stop.sh
[hostname ~ /mksapkg/utelnetd]$ mksapkg -E -s -m WDMyCloudEX4
============================================
        mksapkg version: v1.1
============================================
utelnetd/
utelnetd/remove.sh
utelnetd/apkg.rc
utelnetd/clean.sh
utelnetd/apkg.sign
utelnetd/bin/
utelnetd/bin/utelnetd
utelnetd/utelnetd.png
utelnetd/init.sh
utelnetd/apkg.xml
utelnetd/install.sh
utelnetd/stop.sh
utelnetd/start.sh
utelnetd/preinst.sh
***[../WDMyCloudEX4_utelnetd_1.00.bin(06192013)]

NAS type:               WDMyCloudEX4
module name:            utelnetd
module versioin:        1.00
packager:               WD

header length:          26659
header checksum:        E40297BE

Add-ons &quot;../WDMyCloudEX4_utelnetd_1.00.bin(06192013)&quot; create!
</pre>

<b>What happens when the installed App doesn’t work?</b>

If an App is not installed correctly, then the package will not install, remove, enable, or disable due to improper shell script files creation. It is easy to solve this error by removing the installed package folder and sending a rescan command to the APKG daemon.

<pre>
# rm -rf /mnt/HD/HD_a2/Nas_Prog/utelnetd
# kill -USR1 `pidof apkg`
</pre>

When you are at the stage of development, it is recommended not to install other Apps. This is because a clean environment will help you to reduce development time for debugging.

[^](#contents)
---

## CREATE WEB PAGE

Check these items in the apkg.rc file:

<pre>
Package:            hello
...
Icon:               hello.png
AddonShowName:      hello
AddonIndexPage:     index.html
AddonUsedPort:      
…
</pre>

Note: If your package does not require a GUI, make sure the AddonIndexPage field is empty.

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image012.jpg)

In the Application page, we need to have an App icon and the recommended icon size is 128xn or nx128 (n &gt; 128).

Icon naming rules: Package_name.png.

When package name is hello, you should rename icon file as hello.png. And make sure the icon can be found in the /var/www/hello/hello.png.

Put your html, jpg, css files in the webpage directory. You should link webpage to /var/www/hello, because the root path of web server is /var/www.

When you implement cgi functions, you should link to /var/www/cgi-bin. Just write it down on init.sh script file. And remember to add remove link command on clean.sh script file.

<pre>
ln -s $path/webpage /var/www/hello
ln -s $path/cgi/* /var/www/cgi-bin/
</pre>

<b>Make sure the path of index file is correct. ex:</b>

<pre>
AddonIndexPage:     index.html  -&gt; you should have this file in /var/www/hello/index.html
AddonIndexPage:     /web/index.html -&gt; you should have this file in /var/www/hello/web/index.html
</pre>

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image013.jpg)

[^](#contents)
---

## MULTI-LANGUAGE SUPPORT

We support multiple languages in the app’s description. Please put language xml file to Addon_Name/web/desc.xml and link the language file to /var/www/Addon_Name in init.sh when creating the addon package.

1. Put language xml file to the add-on folder.

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/image009.png)

2. Add link command for the desc.xml file to init.sh

<pre>WEBPATH=&quot;/var/www/aMule/&quot;
Path=” /mnt/HD/HD_a2/Nas_Prog/aMule”

ln -s $path/web/desc.xml  $WEBPATH
</pre>

You can put “desc.xml” to anywhere in add-on package, but you must link the page to its folder.

The Web UI will check the “desc.xml” file to show the indicated language.

![image](https://github.com/westerndigital-devpro/MCOS3/blob/master/images/mcos3/Picture2.png)

The desc.xml example for Icecast:

<pre>
&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
&lt;config&gt;
&lt;en-US&gt;A free server software for streaming multimedia.&lt;/en-US&gt;
&lt;cs-CZ&gt;Bezplatný serverový software pro vysílání multimediálního obsahu.&lt;/cs-CZ&gt;
&lt;de-DE&gt;Eine kostenlose Serversoftware für das Streaming von Multimedia-Inhalten.&lt;/de-DE&gt;
&lt;es-ES&gt;Software gratuito de servidor para transmitir contenido multimedia.&lt;/es-ES&gt;
&lt;fr-FR&gt;logiciel serveur gratuit de diffusion de contenus multimédias.&lt;/fr-FR&gt;
&lt;hu-HU&gt;Ingyenes kiszolgálószoftver a multimédiás tartalmak adatfolyam útján történ_ továbbításához.&lt;/hu-HU&gt;
&lt;it-IT&gt;software server gratuito per lo streaming dei contenuti multimediali.&lt;/it-IT&gt;
&lt;ja-JP&gt;マルチメディア ストリーミング用の無料サーバー ソフトウェア。&lt;/ja-JP&gt;
&lt;ko-KR&gt;멀티미디어 스트리밍을 위한 무료 서버 소프트웨어.&lt;/ko-KR&gt;
&lt;no-NO&gt;Et gratis serverprogram for direkteavspilling av multimedia.&lt;/no-NO&gt;
&lt;nl-NL&gt;Een gratis serversoftware voor het streamen van multimedia.&lt;/nl-NL&gt;
&lt;pl-PL&gt;Bezp_atne oprogramowanie serwerowe do strumieniowych transmisji danych multimedialnych.&lt;/pl-PL&gt;
&lt;pt-BR&gt;Um software de servidor gratuito para fazer transmissão multimídia.&lt;/pt-BR&gt;
&lt;ru-RU&gt;Бесплатное серверное программное обеспечение для потокового воспроизведения мультимедиа.&lt;/ru-RU&gt;
&lt;sv-SE&gt;En gratis serverprogramvara för strömning av multimedia.&lt;/sv-SE&gt;
&lt;tr-TR&gt;Multimedya akı_ına yönelik ücretsiz bir yazılım.&lt;/tr-TR&gt;
&lt;zh-CN&gt;用于流式传输多媒体的免费服务器软件。&lt;/zh-CN&gt;
&lt;zh-TW&gt;用於串流多媒體的免費伺服器軟體。&lt;/zh-TW&gt;
&lt;/config&gt;
</pre>

Note: the translated app descriptions you add to desc.xml will be used to build your app's entry in the App Catalog [WHEN YOU SUBMIT YOUR APP](https://developer.westerndigital.com/develop/wd/forms/mcos3on/submit-app-new-mcos3on.html).

As you can see from the desc.xml example, your app can be added to the App Catalog in the following regions &amp; locales:

en-US - English (United States)

cs-CZ - Czech (Czechia)

de-DE - German (Germany)

es-ES - Spanish (Spain)

fr-FR - French (France)

hu-HU - Hungarian (Hungary)

it-IT - Italian (Italy)

ja-JP - Japanese (Japan)

ko-KR - Korean (South Korea)

no-NO - Norwegian (Norway)

nl-NL - Dutch (Netherlands)

pl-PL - Polish (Poland)

pt-BR - Portuguese (Brazil)

ru-RU - Russian (Russia)

sv-SE - Swedish (Sweden)

tr-TR - Turkish (Turkey)

zh-CN - Chinese (China)

zh-TW - Chinese (Taiwan)

[^](#contents)
---

## DOWNLOADS

Visit the [DOWNLOADS](https://account.wdc.com/devportal) page to get the Apps Package SDK & compilers. This requires a free Developer Portal account - [CLICK HERE TO REGISTER](https://account.wdc.com/devportal).

[^](#contents)
---

----

| Updated  |  Rev       |
|----------|-----------:|
|GF        |v08082019   |
