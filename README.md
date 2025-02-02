## Java_IDX_Parser (idx-parser)
Updated for python 3 (now version 2.1)<br>

The original, and the best, Java Cache IDX parser.

This was written as a result of working quite a few Java malware infection cases. While I grew proficient at manually carving the Java IDX file, which retains download history of malicious Java archives, I learned that a tool may work better when teaching my coworkers how to do the same.

Java IDX files contain high-fidelity indicators about where a piece of malware originated from and how it got onto the infected system. Additionally, most analysis to this point was performed off the text-strings within the file, while ignoring the large blocks of binary data.

At the time of development, there was only one source available for this file, Corey Harrell's blog post from 2011 (http://journeyintoir.blogspot.com/2010/10/anatomy-of-drive-by-part-2.html) and a IDX to Timeline parser written by Sploit (http://sploited.blogspot.com/2012/08/java-forensics-using-tln-timelines.html).

The large blocks of binary data kept bugging me, so I wrote this tool. The initial release did just the basic text sections while I gathered the amount of interest in it. The latest releases perform decompression and basic binary analysis of Java serialization code. At first I used an existing Java serialization module, until I found that Oracle didn't follow their own file specifications, which broke the existing parsers, and required me to write my own.

The latest release removes all interpretation of the file, outputting just raw data to the screen. That way you get a more accurate portrayal of the data, and you can choose what data is relevant to your cause. Even though most Section 4 data appears to be junk to me, it's in there, and its relevance may come to light one day.

## Example usage

```bash

usage: idx_parser.py [-h] [-c] FILENAME

Java IDX Parser v2.1 -- by @bbaskin and digitalsleuth

positional arguments:
  FILENAME    IDX file to process

options:
  -h, --help  show this help message and exit
  -c, --csv   Generates pipe (|) separated file of results (to avoid comma
              collision)

idx-parser Samples\malware\1c20de82-1678cc50.idx

IDX file: O:\\java-idx-parser\\1c20de82-1678cc50.idx (IDX File Version 6.05.05)

[*] Section 1 (Metadata) found:
Content length: 7162
Last modified date: Thu, 26 Jul 2001 05:00:00 GMT (epoch: 996123600.0)
Section 2 length: 365
Section 3 length: 167
Section 4 length: 15
Blacklist Expiration date: Sun, 13 Jan 2013 15:22:26 GMT (epoch: 1358090546.335)

[*] Section 2 (Download History) found:
URL: http://80d3c146d3.gshjsewsf.su:82/forum/dare.php?hsh=6&key=b30a14e1c597bd7215d593d3f03bd1ab
IP: 50.7.219.70
<null>: HTTP/1.1 200 OK
content-length: 7162
last-modified: Mon, 26 Jul 2001 05:00:00 GMT
content-type: application/x-java-archive
date: Sun, 13 Jan 2013 16:22:01 GMT
server: nginx/1.0.15
deploy-request-content-type: application/x-java-archive

[*] Section 3 (Jar Manifest) found:
Manifest-Version: 1.0
Ant-Version: Apache Ant 1.8.3
X-COMMENT: Main-Class will be added automatically by build
Class-Path:
Created-By: 1.7.0_07-b11 (Oracle Corporation)

[*] Section 4 (Code Signer) found:
[*] Found: Data block. 
Length:  4
Data: b'\x00\x00\x00\x00'	Hex: 0x00000000
[*] Found: Data block. 
Length:  3
Data: b'0'      	Hex: 0x300d0a

```

## Copyright and license

Copyright 2013 Brian Baskin

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this work except in compliance with the License.
You may obtain a copy of the License in the LICENSE file, or at:

  [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
