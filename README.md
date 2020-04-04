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
