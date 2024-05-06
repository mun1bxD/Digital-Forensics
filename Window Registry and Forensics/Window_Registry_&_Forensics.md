**Registry Forensics & Forensics**

**Window Registry Structure**

The Windows Registry is a hierarchical database used by the Microsoft Windows operating system to store configuration settings and options. It acts as a centralized repository for storing information about system hardware, software, user preferences, and system settings. The registry is organized into keys, subkeys, and entries, similar to a hierarchical file system.

1. Open the Run dialog: Press Windows Key + R on your keyboard. This action will open the "Run" dialog box.
2. Enter the command: Type regedit into the text field of the "Run" dialog box. Then, press Enter or click "OK".
3. User Account Control (UAC) prompt: If prompted by User Account Control, click "Yes" to allow the Registry Editor to make changes to your system. You may need administrator privileges to proceed.
4. Registry Editor: Once you've confirmed the UAC prompt, the Registry Editor window will open. Here, you'll see a hierarchical view of the registry keys on the left side and their corresponding values on the right side.


In Registry Editor, the hives are the set of registry keys that appear as folders on the left-hand side of the screen when all other keys have been minimized.

**Registry hives function**

HKEY_CLASSES_ROOT (HKCR):

- Main Function: This hive contains information about file associations and OLE object class registration. It maps file extensions to the applications that are associated with them and defines which application should be launched when a particular file type is opened.
- Typical Contents: File extension associations, COM (Component Object Model) class registrations, and OLE (Object Linking and Embedding) information.

HKEY_CURRENT_USER (HKCU):

- Main Function: This hive contains configuration information specific to the currently logged-in user. It stores settings such as desktop preferences, environment variables, application settings, and personalized preferences for installed software.
- Typical Contents: User-specific settings for desktop, Start menu, Control Panel, installed applications, and more.

HKEY_LOCAL_MACHINE (HKLM):

- Main Function: This hive contains configuration data that applies to the local computer and all users who log on to the computer. It stores settings related to hardware, system software, drivers, and security.
- Typical Contents: Hardware settings, system configuration, installed software information, security settings, device drivers, and more.

HKEY_USERS:

- Main Function: This hive contains subkeys corresponding to user profiles loaded on the computer. Each subkey represents the HKEY_CURRENT_USER hive for a specific user.
- Typical Contents: User-specific settings and configurations for each user profile on the computer.

HKEY_CURRENT_CONFIG:

- Main Function: This hive contains information about the current hardware profile used by the system. It is a pointer to the HKEY_LOCAL_MACHINE\System\CurrentControlSet\Hardware Profiles hive.
- Typical Contents: Hardware profile settings, including information about devices, drivers, and system configuration.

**Example of each hive**

Certainly! Here are some examples of the types of information you might find in each of the primary registry hives:

**HKEY_CLASSES_ROOT (HKCR):**

- Example: File associations

- ".txt" file extension mapped to "Notepad.exe"
- ".docx" file extension mapped to "Microsoft Word"

- Example: COM class registrations

- CLSID {00021401-0000-0000-C000-000000000046} mapped to "Shell Application Object"

- Example: OLE object information

- ProgID "Word.Document.12" mapped to "Microsoft Word Document"

**HKEY_CURRENT_USER (HKCU):**

- Example: Desktop preferences

- Wallpaper setting
- Screen resolution

- Example: Application settings

- Preferences for web browser
- Customizations in Microsoft Office applications

- Example: Environment variables

- User-specific PATH variable

**HKEY_LOCAL_MACHINE (HKLM):**

- Example: Hardware settings

- Configuration information for installed hardware components (e.g., CPU, GPU, RAM)
- Device drivers and related settings

- Example: System configuration

- Boot configuration
- Services configuration

- Example: Installed software information

- List of installed programs and their settings
- Uninstall information

**HKEY_USERS:**

- Example: User-specific settings

- Preferences for desktop background
- Start menu layout

- Example: Application settings

- Customizations in software applications specific to each user

- Example: Security settings

- User-specific permissions and policies

**HKEY_CURRENT_CONFIG:**

- Example: Hardware profile settings

- Current hardware configuration (e.g., display settings, device configurations)
- Plug and Play information

- Example: Device settings

- Configuration settings for connected hardware devices
- Driver information

**Part of registry hives**

**Root Keys:** all the above 5 key

**Keys and Subkeys:** Keys are containers that store configuration settings, and they can contain subkeys and values.

Below is the key and sub key of HKEY_CURRENT_CONFIG


**Values:** Values are data entries within keys that store configuration information. Each value has a name (often referred to as the value name or entry name) and a corresponding data value.

**Data Types:** Each registry value has a data type that specifies the format of the data it contains. Common data types include:

- REG_SZ: String value
- REG_EXPAND_SZ: Expandable string value
- REG_DWORD: 32-bit DWORD value
- REG_QWORD: 64-bit QWORD value
- REG_BINARY: Binary data value
- REG_MULTI_SZ: Multiple strings value



**Security Descriptors:** Registry keys and values can have security descriptors associated with them, which define the permissions and access control settings for the corresponding configuration data. Security descriptors determine who can read, write, modify, or delete registry entries.

To view a security Descriptor

Right click on key or sub key ->permission


**Different operations on window registry**

**Adding:** You can add new keys, subkeys, and values to registry hives. This allows you to customize system settings or configure applications according to your requirements.

Add a New Key or Subkey:

- Right-click on the parent key where you want to add the new key or subkey.
- From the context menu, select "New", and then choose either "Key" or "String Value" (depending on whether you want to add a key or a value).
- Enter a name for the new key or subkey and press Enter to create it.


**Deleting:** You can delete keys, subkeys, and values from registry hives. This is useful for removing outdated or unused configurations, uninstalling software, or resetting settings to default values.

To delete a key or sub key right click on the folder and select delete.

A pop message will appear just click ye to delete it



**Window Registry forensics**



**HKCU\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Explorer**

\\ComDlg32

o \LastVistedPidlMRU

o \OpenSavePidlMRU

- The comdlg32.dll file, also known as the Common Dialog Box Library, is a dynamic link library file that contains functions and resources used by various Windows applications. It provides a standardized way for developers to implement common dialog boxes, ensuring a consistent user experience across different programs.

1. OpenSaveMRU:

- This key tracks files that have been opened or saved within a Windows shell dialog box. It includes a wide range of applications, not just web browsers like Internet Explorer and Firefox, but also many commonly used applications.
- The key is located at HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSaveMRU (named OpenSavePidlMRU in Vista/Win7).
- It contains both values and multiple subkeys. The values store items that don't have file extensions associated with them, often auto-complete information. Subkeys correspond to various file extensions and store full path information for files of that extension that have been opened or saved.
- Each subkey maintains its own Most Recently Used (MRU) list and last write time.

3. LastVisitedMRU:

- This key tracks the specific executable used by an application to open the files documented in the OpenSaveMRU key, along with the directory location for the last file accessed by that application.
- The key is located at HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedMRU (named LastVisitedPidlMRU in Vista/Win7).
- Data in this key is stored in binary format.
- It also maintains its own MRU list and last write time.

\MountPoints2:
- Tracks data about removable devices, including USB drives, external hard drives, and network drives.
- Each mounted drive has a unique GUID associated with it, which is stored within this key.
- This information helps Windows Explorer remember the drive mappings and access them easily.

\RecentDocs:
- Maintains a list of recently accessed files and folders.
- This allows users to quickly access previously opened documents from the Explorer Quick Access panel.
- The number of entries stored here is usually limited by a configurable setting.

\RunMRU:
- Contains the history of programs launched through the Start Menu's "Run" dialog.
- This list provides quick access to frequently used applications.
- Similar to RecentDocs, the number of entries is usually limited.

\TypedPaths:
- Tracks the history of paths manually entered into the Explorer address bar.
- This helps users quickly navigate back to previously visited locations.
- The number of entries stored here might also be limited by a setting.

\UserAssist:
- Stores evidence of program execution within the user's profile.
- This information is used by various features like the Start Menu search and Cortana to personalize suggestions and recommendations.
- It essentially tracks which GUI programs the user has been running.

\WordWheelQuery:
- Records the history of search queries entered within the Explorer search bar.
- This information helps improve search suggestions and results based on the user's past searches.
- Similar to other history-based keys, the number of entries might be limited.

HKLM\\SYSTEM\\CurrentControlSet\\Enum\\USB
- This key stores information about all USB devices that have ever been connected to your system.
- It acts as a central repository for tracking USB devices and their associated details.

- Device IDs: Each USB device has a unique identifier, often referred to as the "VID/PID" (Vendor ID/Product ID). This information is crucial for the operating system to identify the specific device and load the appropriate drivers.

- Additional Details: Besides VID/PID, the key might store other relevant information about the USB device, such as:

- Device name or description 
- Serial number 
- Manufacturer information 
- Connection status (currently connected or previously connected)


This string is id of the usb device if & is in second last it mean it globally unique serial number if the serial number at second location it mean the usb manufacturer doenot follow microsoft guideline.in this case window generate unique serial number which is unque on window but not globally unique

HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USB iSerial #\Properties\{83da6326-97a6-4088-9453-a1923f573b29}\####

• 0064 = First Install (Win7 / 8)

 o Also found in setupapi.log / setupapi.dev.log

• 0066 = Last Connected (Win8+ only)

 o Also \Enum\USB\VID_XXXX&PID_YYYY last write time of USB Serial # key

 o Also \MountPoints2\{GUID} last write time of key

 • 0067 = Last Removal (Win8+ only)



**HKLM\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\AppCompatCache**

• Also known as “Shimcache”, this can sometimes be an evidence of execution artifact

o Windows 10/11 removed the “InsertFlag”, sometimes incorrectly referred to as an “Execution Flag”, that was used to show likely execution; thus, this artifact can NOT be used to show execution in Windows 10/11

• Stores the full file path and name and last modified (M) timestamp



**HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters**
controls settings related to two Windows performance features: Prefetcher and Superfetch. Here's a breakdown of their functions:

Prefetcher:

- Analyzes your computer's usage patterns and identifies frequently used applications and files.
- Proactively loads these files into RAM (memory) in the background before you actually need them.
- This can significantly reduce application launch times and improve overall system responsiveness, especially on HDDs (hard disk drives).

Superfetch:

- Similar to Prefetcher, but with a wider scope.
- Analyzes not only frequently used applications but also recently used system files and libraries.
- Can also leverage unused disk space to store less frequently accessed files, making them readily available when needed.
- This further enhances system performance, particularly on systems with limited RAM.

0 = Disabled

1 = Application prefetching enabled

2 = Boot prefetching enabled (default on Windows 2003 only)

3 = Application and Boot prefetching enabled (default)

• Task Scheduler calls Windows Disk Defragmenter every three (3) days

• When idle, lists of files and directories referenced during boot process and application startups is processed

• The processed result is stored in Layout.ini in the Prefetch directory, and is subsequently passed to the Disk Defragmenter, instructing it to re-order those files into sequential positions on the physical hard drive


**HKLM\\SYSTEM\\CurrentControlSet\\Control\\TimeZoneInformation**


TimeZoneKeyName:This is a string value that specifies the current time zone your system is configured to use.

- It stores the standard time zone name, such as "Pacific Standard Time" or "Pakistan Standard Time".

ActiveTimeZoneBias:This is a DWORD (32-bit) value that represents the offset of your current time zone from Coordinated Universal Time (UTC) in minutes.

- A positive value indicates your time zone is ahead of UTC, while a negative value indicates it's behind.

Other Values:

- Several other values within this key store additional time zone-related information, such as:

- StandardName: The name of the standard time zone without DST. 
- DaylightName: The name of the time zone with DST applied. 
- DaylightStart: Specifies the date and time when DST starts. 
- DaylightEnd: Specifies the date and time when DST ends.

**HKLM\\SYSTEM\\CurrentControlSet\\Control\\ComputerName\\ComputerName**


**HKLM\\SYSTEM\\CurrentControlSet\\services\\LanmanServer\\Shares**

• Stores all Network Shares

This key stores information about all the file and folder shares currently configured on your computer. Each subkey within this key represents an individual share, and its values define various aspects of the share


**HKLM\\SYSTEM\\CurrentControlSet\\services\\Tcpip\\Parameters\\Interfaces**

• Stores network interface configuration information (record the interface GUID!)

plays a critical role in managing your network interface configurations within the Windows registry. Here's a breakdown of its significance:

Function:

This key is a container for subkeys, each representing a specific network interface card (NIC) installed on your computer. These subkeys store various TCP/IP configuration settings for each network adapter, including:

- IP Address: The unique identifier assigned to your device on the network.

- Subnet Mask: Defines the network segment the device belongs to.

- Default Gateway: The router's IP address used to route traffic outside your local network.

- DNS Server(s): The addresses of servers responsible for translating domain names into IP addresses.

- Other settings: Additional configurations like WINS servers, DHCP settings, and more.


**HKLM\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\NetworkList**

- HKLM: Stands for "HKEY_LOCAL_MACHINE," which stores system-wide settings and configurations accessible by all users on the computer.

• \Signatures

o \Unmanaged (record DefaultGatewayMac, DnsSuffix, FirstNetwork (SSID), ProfileGuid)

o \Managed

• \Nla

o \Cache

• Profiles

- SOFTWARE: This subkey contains information related to installed software applications and their settings.

- Microsoft\Windows NT: This subkey further delves into Windows NT specific settings.

- CurrentVersion: This subkey points to the currently used version of Windows NT settings.

- NetworkList: This key specifically stores information about all the network profiles your system has encountered


Most info regarding (Network Level Authentication)NLA will be stored under the NetworkList key above, and also:

**HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\HomeGroup**

Network Type, and First / Last Connected Times (find using the ProfileGuid key harvested from Signatures\Unmanaged):

HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles\{GUID}

HKLM\SOFTWARE\Microsoft\WZCSVC\Parameters\Interfaces\{GUID} → (XP only, use last write time of the key to determine the last time the network was connected)

0x06 = Wired

0x17 = Broadband

0x47 = Wireless

You will also find DateCreated and DateLastConnected under this key.

HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\EMDMgmt

• Key will ONLY be present if system drive is NOT an SSD

• Traditionally used for ReadyBoost

• Find Serial # to obtain the Volume Serial Number of the USB device

o The Volume Serial Number will be in decimal – convert to hex

o You can find complete history of Volume Serial Numbers here, even if the device has been formatted multiple times. The USB device’s Serial # will appear multiple times, each with a different Volume Serial Number generated on each format.

Using the Volume GUID found in SYSTEM\MountedDevices, you can find the user that actually mounted the USB device:

**HKCU\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Explorer\\Mountpoints2**

USB Times:

• First time device is connected

• Last time device is connected

• Removal time

While not a Registry artifact, note that USB First Time Device Connected Logs are also available:

XP: C:\Windows\setupapi.log

Vista+: C:\Windows\inf\setupapi.dev.log

Search for the device’s Serial # within these logs to determine the first time the device was connected.

All registry hives are present at

C:\Windows\System32\config
