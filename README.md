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
 3. **sof-elk_update.sh**: This is a slightly modified version of Phil Hagen's 'nfdump2sof-elk.sh' script (https://github.com/philhagen/sof-elk/blob/master/supporting-scripts/nfdump2sof-elk.sh. The purpose of this file is to convert NetFlow data in a format that SOF-ELK can ingest. This is a slightly modified version of Phil Hagen's 'nfdump2sof-elk.sh' script. The purpose of this file is to convert NetFlow data in a format that SOF-ELK can ingest. This file is used by NFPA_v1.sh to complete one of its evidence processing tasks.
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
