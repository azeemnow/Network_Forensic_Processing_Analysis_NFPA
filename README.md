# **Network Forensic Processing & Analysis (NFPA)**

*NFPA helps optimize investigations by reducing errors that are typically involved in manually processing and analyzing network-based evidence through various tools and command-line options.*

# Overview
The purpose of NFPA tool is to provide Cybersecurity analysts a more efficient and automated (“click & forget”) means of executing commonly-used network forensics utilities and analysis queries against network evidence (PCAP).

# How NFPA Will Help Optimize Your Network Investigations?
NFPA tool helps optimize investigations by reducing errors that are typically involved in manually processing and analyzing network-based evidence through various popular tools and command-line options. 

### Using NFPA, an analyst can:
 1. quickly process case evidence through  various popular tools and utilities all by a simple script execution 
 2. review results from 60+ individual, multi-purpose queries pre-ran again the evidence
 3. view the native output from all of the evidence process utilities - providing the opportunity for any validation or further analysis

All of the above is organized in an easy-to-understand structure which allows the analyst to quickly find answers as well as the authoritative source of those answers. 

# Dependecies
A key requirement when designing NFPA was to keep dependencies as minimum as possible. I wanted to make sure I leverage a platform that is already commonly used by analysts which is pre-configured with all of the necessary tools and capabilities. This would allow analysts to instantly begin their work on investigations and not have to deal with the underlying system engineering. 

To that end, here is the only dependency:
 - SANS SIFT Ubuntu Workstation (https://digital-forensics.sans.org/community/downloads)

Additionally, the NFPA is built-in Bash. Which means you do not have to import any specific libraries or run a certain version. Another advantage of using Bash is that you will most likely be able to run NFPA on other Linux distributions (may need to install some purpose-built network forensic tools separately).

# **Getting Started**

Here is what you need to know to get started:

### Components
NFPA is made of the 4 required components:

 1. **NFPA_v1.sh:** is the main Bash script. You can consider it as the brains of the whole operation. It is the only script that you will interact with by simply launching it.
 2. **sift_tools.txt**: This is the first file that NFPA_v1.sh calls. The purpose of this file is to provide NFPA with a list of all of the evidence processing tasks that need to be performed. If you view the file, it cleanly lists each task along with the specific tool and its respected command options.
 3. **sof-elk_update.sh**: This is a slightly modified version of Phil Hagen's 'nfdump2sof-elk.sh' script (https://github.com/philhagen/sof-elk/blob/master/supporting-scripts/nfdump2sof-elk.sh. The purpose of this file is to convert NetFlow data in a format that SOF-ELK can ingest. The purpose of this file is to convert NetFlow data in a format that SOF-ELK can ingest. This file is used by NFPA_v1.sh to complete one of its evidence processing tasks.
 4. **acommands.txt**: This file is very similar to sift_tools.txt in that its simply a text file that lists a series commands on each line. However, this file is used to perform various analysis tasks on the evidence that sift_tools.txt has helped to process. There are over 60 individual tasks that this file processes but due to its simple one-line format, analysts can easily see details of each task and understand certain commands options that are used to generate outputs.
 
 ### Install
 - [ ] Download the Zip File (NEPA_v1.zip)
	 - [ ] Click on the green “Clone or download” towards to top-right of the page
	 - [ ] This will download all of 4 component that you need in a ZIP compressed format.
	 - [ ] Unzip the archive to a location of your choosing 
	 - [ ] Modify the permission of the NEPA_v1.sh file
	 - [ ] Chmod +x NEPA_v1.sh

### Usage
Confirm that you have successfully completed the last step of the Install setup - Modify the permission of the NEPA-v1.sh

Run the script using:
 - ./NEPA-v1.sh
 - The script will ask you to provide a unique case number.
 - The script will ask you to provide a full-path to the evidence PCAP file.
	 - Please note, tab-complete option is not available It is advised that you collect the full-path to your evidence prior launching the script.

# Fail Safe Design
As mentioned earlier, one of the key requirements for NFPA was "click & forget". However, I understood that there are situations where you may not want to process the evidence through all of the available tools. 

To provide this flexibility, I incorporated the 10-second rule. Essentially, during the evidence processing phase of the tool, you are given 10-seconds to script any particular task before it begins. The name of the task is highlighted on the screen, and you can type-in "no" to skip that particular task. However, if no response is received, the default is to run all of the tasks.

One important note about skipping tasks. If you skip any of the evidence processing tasks, then any of the analysis tasks that were depended on that task would not run. Additionally, any of the associated analysis reports will be saved empty.

# Demo
coming...

# Tools Incorporated
## Evidence Processing Tools

Following tools are run against the evidence during the processing stage:

  1. **Capinfos:** “capinfos gets metadata about a packet capture. You can be very granular about what pieces of data you want displayed and the output format.” (https://tshark.dev/analyze/get_info/capinfos/)
 2. **Zeek (Bro):** “A powerful framework for network traffic analysis and security monitoring.” (https://github.com/zeek/zeek)
 3. **PassiveDNS:** “PassiveDNS sniffs traffic from an interface or reads a pcap-file and outputs the DNS-server answers to a log file. (https://github.com/gamelinux/passivedns)
 4. **NFPcapd:** “ create netflow data from precollected pcap traffic.” (https://github.com/phaag/nfdump)
 5. **sof-elk_update.sh:** The purpose of this file is to convert NetFlow data in a format that SOF-ELK can ingest. This is a slightly modified version of Phil Hagen's : (https://github.com/philhagen/sof-elk/blob/master/supporting-scripts/nfdump2sof-elk.sh)
 
 ## Evidence Analysis Tools
 
 Following tools are run against the processed-evidence to generate the various analysis reports:
 
 1. **NFDump:** “process netflow and sflow data.” (https://github.com/phaag/nfdump)
 2. **TShark:** “ terminal oriented version of Wireshark designed for capturing and displaying packets” (https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html)
 3. **TCPdump**: “prints out a description of the contents of packets on a network interface that match the boolean expression” (https://www.tcpdump.org/manpages/tcpdump.1.html)
 4. **Ngrep:** “allows you to specify an extended regular or hexadecimal expression to match against data payloads of packets.” (https://github.com/jpr5/ngrep)
 5. **TCPflow:** “useful tool for understanding network packet flows and performing network forensics. Unlike programs such as WireShark, which show lots of packets or a single TCP connection, tcpflow can show hundreds, thousands, or hundreds of thousands of TCP connections in context.” (https://github.com/simsong/tcpflow)
 6. **Egrep:** “scans a specified file line by line, returning lines that contain a pattern matching a given regular expression”
 
 # Future Development
 The NFPA tool was designed with future development in mind.
 
The unique structure of having the brains of the tool (**NFPA_V1.sh**) separate from the evidence processing code (**sift_tools.txt**) and the analysis/reporting code (**acommands.txt**), not only makes it easy to understand but also presents endless opportunities for expansion. 

Anyone can easily modify either of the supporting code-bases (**sift_tools.txt**, **acommands.txt**) to meet their specific needs. 

For instance, if you want to add another processing task, simply append it with the appropriate command-line options to the **sift_tools.txt** file. 

Similarly, if you want to change any of the analysis commands, simply append your updates to the **acommands.txt** file.

The main **NFPA_v1.sh** should automatically recognize and incorporate the updates.

# Tested Configuration

NFPA has been developed and tested on **SIFTv3**:
*Linux siftworkstation 4.4.0-131-generic #157-Ubuntu SMP Thu Jul 12 15:51:36 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux*

# Inspirations and References

 1. https://github.com/packetrat/packethunting/blob/master/README.md 
 2. https://401trg.com/triaging-large-packet-captures-4-key-tshark-commands-to-start-your-investigation/
 3. https://github.com/mitchellkrogza/nginx-ultimate-bad-bot-blocker/blob/master/_generator_lists/bad-user-agents.list 
 4. https://www.securitynik.com/2015/12/some-tshark-examples-mix-of-basic-and.html
