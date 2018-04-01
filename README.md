## Windows Redstone 4 (1803 Data analysis)

Explains the telemetry, opt-out methods and provides some Wireshark/Burp dumps with an explanation. All findings are on the Enterprise Redstone 4 (Spring Creators Update) -> 17133.1.180323-1312.RS4_RELEASE_CLIENTCOMBINED_UUP_X64FRE_EN-US (created from official UUP files). 

The pcaps are there in case you want to verify my words and decipher the traffic in order to see what is been transmitted.

Please do not ask if I do this for Pro versions too, this project here is really huge and I don't have time to do this every month when something is changed or on other versions. The main goal is to identify what is been collected after you changed the telemetry via gpedit.msc (Group Policy Editor) to 0 [security only] in order to see if Microsoft holds what they promise or not. This must be done objectively.


The default telemetry level is 'Full' for Windows 10 Home and Pro and Enhanced for Enterprise edition. On a device that is running an Insider preview edition, this value is set to Full and can only be changed by installing a released version.

 
Test procedure:
===============
* 17133.1.180323-1312 x64 Enterprise (no OEM)
* No additional software installed except Wireshark, NetLimiter & NetWorx 
* No tools to 'manipulate any settings (registry, gpedit.msc) 
* Gpedit.msc telemetry is set to 0 -> security only.
* No KB's installed.
* No HOSTS entries.
* The GPO and Registry settings must be untouched which means a fresh user account must be used.
* The traffic must be re-directed trough a proxy (router/software) in order to catch everything since Microsoft use it's own DNS mechanism which can't be disabled anymore via services.msc (only via registry and this will be overridden next restart).
* The view must be objective based on the findings, not 'what you think MS might do or not do' which means even if there is a connection we need to decipher the connection in order to see what is (or not) been collected.

My own IP was obfuscated in order to protect my real location. My IP was replaced with: 


Repository
===============

Every troll comment, things without OWN prove gets immediately banned from my project without any first warning. I won't tolerate any trolling anymore in any of my projects. I don#t have time for this. 



Possible telemetry related
===============

Some services never submitting anything unless you use them, some running in the background and some only collect something only in case you explicitly use them. 

* Diagnostics Tracking Service (KB3022345 & more) - called during the setup.exe & via task scheduler
* Connected User Experiences and Telemetry aka DiagTrack (svchost.exe -k utcsvc -p) can be manually stopped.
* Web Search
* Cortana (Anonymous info, usage information will be shared but not search history, Microsoft Account information, or specific location the stream is encrypted).
* Possible some other tasks & services.msc related automatically enabled services (Keep in mind that even if there automatically started doesn't mean there submitting something unless xyz behavior was triggered).
* Microsoft certified diagnostic tools: msinfo32.exe, powercfg.exe, and dxdiag.exe.


Windows 10 Enterprise edition
===============

* Automatic Root Certificates Update (enabled by default) 
* Cortana and Search (enabled by default but not active unless you use it the first time)
* Date & Time (enabled by default) 
* Device meta-data retrieval (enabled by default)
* Find My Device (optional)
* Font streaming (enabled by default)
* Insider Preview builds (optional + requires an Account)
* Internet Explorer (enabled by default but not active unless you use it the first time)
* Microsoft Edge (enabled by default but not active unless you use it the first time)
* Live Tiles (enabled by default)
* Mail synchronization (optional)
* Microsoft Account (optional during setup or afterwards)
* Network Connection Status Indicator (enabled by default) 
* Offline maps (enabled by default but optional since it doesn't send any data unless you use it)
* OneDrive (enabled by default)
* Preinstalled apps (enabled by default)
* Retail Demo Service (enabled by default)
* Homegroup (gets removed in RS 5)


Settings > Privacy via GPO or MDM/Registry or cmd line
* General (depending on the settings)
* Location (optional)
* Camera (optional)
* Microphone (optional)
* Notifications (enabled by default)
* Speech, inking, & typing (optional via Setup)
* Account info (optional via Setup)
* Contacts (optional)
* Calendar (optional)
* Call history (optional)
* Email (optional)
* Messaging (optional)
* Phone calls (optional)
* Radios (optional)
* Other devices (optional) 
* Feedback & diagnostics (enabled by default)
* Background apps 
* Motion (optional)
* Tasks (never, tasks itself are related to pre-set ones)
* App Diagnostics (enabled by default)
* Software Protection Platform (enabled by default, manage license etc)
* Storage Health (optional trough notification settings)
* Teredo (pre-installed and activated but can be configured)
* Wi-Fi Sense (enabled by default)
* Windows Defender (enabled by default)
* Windows Media Player (gets replaced? enabled by default but optional)
* Windows Spotlight (optional)
* Microsoft Store (enabled by default)
* Apps for websites (optional and depending on settings)
* Windows Update Delivery Optimization (enabled by default)
* Windows Update (enabled by default)

Server Editions and other Windows versions don't differ much because the settings are within the kernel, however some simply don't have a GUI, GPO/MDM or cmd.



Other services according to the EULA

* All Microsoft services scanning for offensive language, unclear how this is done?!


Where is Telemetry Data Stored?
===============

Telemetry data is stored in encrypted files in the hidden %ProgramData%\Microsoft\Diagnosis folder. The UTC client connects to settings-win.data.microsoft.com, provides its device ID (a randomly generated Globally Unique ID that is not associated with any personal information). The telemetry client uses that settings file to connect to the Microsoft Data Management Service at v10.vortex-win.data.microsoft.com and upload any data that is waiting to be sent. The transmission takes place over encrypted HTTPS connections.

Windows 7 sends same data, previous versions sent telemetry data over unencrypted connections, making it possible for attackers to intercept the data. The myth that Vista or other systems have no telemetry is debunked. It is there just not over HTTPS.


How often are the data been submitted?
===============

Telemetry component avoids gathering information that could directly identify a person or an organization. The process is running by the task scheduler, and within the Windows kernel which means it gets triggered even after you disable or delete all task scheduler tasks, this is since RS 2.


How does Microsoft use it's data and how long there stored?
===============

There is no specific detail on that, how long Microsoft stores the data. There is an unofficial statement which mentioned 30 days.

The Windows Devices Group gets this data which is a small group, according to Microsoft only those who can demonstrate a valid business need can access the telemetry info.

The data itself are compiled into business reports for analysis and for use by teams tasked with fixing bugs and improving the performance of the overall operating system and associated services. Microsoft says that only aggregated, anonymous telemetry information is included in reports that are shared with partners. The partner names are not directly mentioned on the EULA nor any official Microsoft page.


## Observational artillery

Fingerprint/TouchID: Scans the user’s fingerprint.

Proximity: Measures the distance of other objects from the phone’s touch screen.

Light: Gauges the light level in the phone’s environment.

Barometer: Measures ambient pressure around the phone.

Accelerometer: Measures acceleration of the device’s movement or vibration.

Gyroscope: Evaluates degree and direction of a phone’s rotation.

Magnetism: Reports the magnetic field intensity around the phone.

Gravity: Measures the force of gravity.

....



