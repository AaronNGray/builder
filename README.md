# builder
Software Builder

outline specification

lift modules to package level ?

## builder

**builder** should have node npm like functionality as well as Visual Studio like solution / project structure.

## investigation
 - MSBuild import/reference with mappings
 - npm import/reference
 - visual studio import/export with mappings
 - XCode projects
 - GNU AUTOCONF/AUTOMAKE projects
 - make & nmake file export

## directory structure
dependant modules maybe all stored in one flattened two tier (project and vesion) heirachy in the users root directory instead of npm like spawl. Or they maybe via mappings to external directory structures, that maybe found constants, 'which' relative, OS directory structure based or via environmental variables.

```
<working-directory>
    .builder
    .signatures
    **.modules**
        <name>
            <version>
                ...

    **projects**
        <solution-root>
            <projects-name>
                .builder
                .signatures
                include
                src
                build
                    <platform>
                        debug
                        development
                        test
                        release
            .modules
                <name>
                    <version>
                        ...
```
Normalized set of packaged modules, either in user home directory or system root directory.
```
<home-or-root-directory>
    .signatures
    .modules
        <name>
            <version>
                ...
```    

## git interop
git interop should be implicit

    b clone <git-project>
    b init
    
```
<home-directory>
    .builder
    .git
    ...
```

## platforms
This should allow the definition of a platform.

### file type and file extensions
platform independent and platform specific file extention to file type mapping should be able to be defined and attached to tools to allow implicit behaviour for different platforms and tools. These should also be able to be attached to MIME types.

### variables
#### environment variables
A global set of environmental variable maybe specified and inherit and map the calling processes environment variables.
```
<environment>
    <variable name="...">
        optional value
        optional mapping
        optional default
    <variable name="PATH">
        ...mappings - domain restriction...
```

### defines & defaults
```
<define>
    <variable name="..." [value]="..." default="...">
    <scope name="...">
        <variable>
```
## types
 -  bool
 -  string
 -  number
 -  enumeration
 -  struct

### type specification
```
<types>
    <type>
        <bool name="..." default="...">
        <string>
        <number>
        <enum>
        <struct>
```
### types
```
<enum name="..." type="..." default="...">
    <value name="..." value="..."/>
</enum>

<struct name="...">
```

## templates

All constructs should be able to parameterizable in order to reduce repetitoin and allow larger possible implementaion domains.

```
<template name="...">
    <parameter name="..." type="..."/>
    <body>
        ...
    </body>
</template>
```
instatiation of a template

```
<instatiate-template name="..." ...parameters...>
    <parameter name="..." value="..."/>
    ...
</instatiate-template>    

```

## tools

A set of standard generic tools can be defined as an abstract tool chain. This can be mapped on to individual platform tool chains.

mapping of options as enums, and augmeneted enums (think ADT's) to command line switches.

 - parameters
 - input(s)
 - output(s)
 - command line

```
<tool name="...">
    <parameters>
        <parameter />
    </parameters>
    <parameter>

    <inputs>
        <input>
    </inputs>
    <input>

    <outputs>
        <output>
    <outputs>
    <output>

    <commands>
        <command>...</command>
        <command>...</command>
        ...
    </commands>
</tool>
```
## tool chain

```
<tool-chain name="..." platform="...">
     <tool name="...">
         ...
     </tool>
     <tool name="...">
         ...
     </tool>
 </tool-chain>
```

## tools

 - copy
 - move
 - rename
 - delete
 
 - mkdir
 - cd|chdir
 - rmdir
 
 - compile
 - link
 - lib
 
 - p|packager
 - b|builder
 - c|commander
 
## solution and projects
```
<solution name="..." [tool-chain="..."]>
    <project name="..." [tool-chain="..."]>
        <group name="..." [tool-chain="..."]>
        <source name="..." path="..." [tool-chain="..."] [tool="..."]>
```
implicit tool selection from file extension

## rules
```
<rules name="..." [tool-chain="..."]>
    <rule name="..." [tool-chain="..."]>
        <dependencies>
            <dependency name="..." />
        </dependencies>                
        <destinations>
            <destination name="..." path="..." />
            ...
        </destinations>
        <sources>
            <source name="..." path="..." />
            ...
        </source>
        
        <tool>
        <tools>
            <tool>
        </tools>
        <command|commands>
    </rule>
</rules>
```

# file formats
Standard package description files are either in a XML or a scoped textual format.

## Standard packaging model
Need work out how to allow a standard packaging model to be created that allows creation of packages for various packaging systems like. This is done with plugin backends.

 - .zip
 - .tar.gz
 - .jar
 - .msi
 - RPM - .deb
 - GNU AUTOCONF/AUTOMAKE packaging model
 - ...
 
### package
### module
### unit

## imports
import of modules from 
 - .git
 - .zip
 - .tar.gz
 - .jar
 - .msi
 - RPM
 - .deb
 - GNU AUTOCONF/AUTOMAKE packaging model
 - ...
 
from
  - module:
  - http: - undesirable but okay if the source has a validated signature that is in trusted signature list.
  - https:
  - git:

```
<imports>
    <module name="..." version="..." path="..." />
    ...
    <platform name="...">
        <module name="..." version="..." path="..." />
    </platform>
    ...
</imports>
```

## export
```
<export>
    <includes>
    <libraries>
        <debug>
        <release>
```
deployment to :-
  - module:
  - http: - undesirable but okay if the source has a validated signature that is in trusted signature list.
  - https:
  - git:

## versioning system

## signature system

### bulider command line

#### new project

    mkdir <project name>
    cd <project name>
    b init

or just

    b init <project name>
    cd <project name>

#### install
#
    b install
    b clean
    b <command>

## commands
commands invoke tools

#### git support

    b init <project name> <blank-git-repo>
    cd <project name>

#### http(s) support
#### ftp support

## implementation
### initial prototype
files maybe either XML or YML or probably just YML with XML conversion.
#### XML
XSLT maybe used to do a prototype implementation of a subset of target platform tools and tool chains.
stanard make files should be a very easy initial target.

#### YML
https://fdik.org/yml/
The whole system may be able to be prototyped with either YSLT.

#### Dedicated builder programs.

### tools
Ideally builder will have
 - command line tool
 - GUI IDE with optional background/foreground building
 - dedicated builder app with :-
     - progress bars for overall progress
     - folding progress bars for individual build process
     - disk space indicator bar, optional hiding
 - background server application with HTTP REST API

## Copyright
Copyright Aaron N Gray 2016

## Design License
Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International Public License
By exercising the Licensed Rights (defined below), You accept and agree to be bound by the terms and conditions of this Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International Public License ("Public License"). To the extent this Public License may be interpreted as a contract, You are granted the Licensed Rights in consideration of Your acceptance of these terms and conditions, and the Licensor grants You such rights in consideration of benefits the Licensor receives from making the Licensed Material available under these terms and conditions.
Section 1 – Definitions.
Adapted Material means material subject to Copyright and Similar Rights that is derived from or based upon the Licensed Material and in which the Licensed Material is translated, altered, arranged, transformed, or otherwise modified in a manner requiring permission under the Copyright and Similar Rights held by the Licensor. For purposes of this Public License, where the Licensed Material is a musical work, performance, or sound recording, Adapted Material is always produced where the Licensed Material is synched in timed relation with a moving image.
Copyright and Similar Rights means copyright and/or similar rights closely related to copyright including, without limitation, performance, broadcast, sound recording, and Sui Generis Database Rights, without regard to how the rights are labeled or categorized. For purposes of this Public License, the rights specified in Section 2(b)(1)-(2) are not Copyright and Similar Rights.
Effective Technological Measures means those measures that, in the absence of proper authority, may not be circumvented under laws fulfilling obligations under Article 11 of the WIPO Copyright Treaty adopted on December 20, 1996, and/or similar international agreements.
Exceptions and Limitations means fair use, fair dealing, and/or any other exception or limitation to Copyright and Similar Rights that applies to Your use of the Licensed Material.
Licensed Material means the artistic or literary work, database, or other material to which the Licensor applied this Public License.
Licensed Rights means the rights granted to You subject to the terms and conditions of this Public License, which are limited to all Copyright and Similar Rights that apply to Your use of the Licensed Material and that the Licensor has authority to license.
Licensor means the individual(s) or entity(ies) granting rights under this Public License.
NonCommercial means not primarily intended for or directed towards commercial advantage or monetary compensation. For purposes of this Public License, the exchange of the Licensed Material for other material subject to Copyright and Similar Rights by digital file-sharing or similar means is NonCommercial provided there is no payment of monetary compensation in connection with the exchange.
Share means to provide material to the public by any means or process that requires permission under the Licensed Rights, such as reproduction, public display, public performance, distribution, dissemination, communication, or importation, and to make material available to the public including in ways that members of the public may access the material from a place and at a time individually chosen by them.
Sui Generis Database Rights means rights other than copyright resulting from Directive 96/9/EC of the European Parliament and of the Council of 11 March 1996 on the legal protection of databases, as amended and/or succeeded, as well as other essentially equivalent rights anywhere in the world.
You means the individual or entity exercising the Licensed Rights under this Public License. Your has a corresponding meaning.
Section 2 – Scope.
License grant. 
Subject to the terms and conditions of this Public License, the Licensor hereby grants You a worldwide, royalty-free, non-sublicensable, non-exclusive, irrevocable license to exercise the Licensed Rights in the Licensed Material to: 
reproduce and Share the Licensed Material, in whole or in part, for NonCommercial purposes only; and
produce and reproduce, but not Share, Adapted Material for NonCommercial purposes only.
Exceptions and Limitations. For the avoidance of doubt, where Exceptions and Limitations apply to Your use, this Public License does not apply, and You do not need to comply with its terms and conditions.
Term. The term of this Public License is specified in Section 6(a).
Media and formats; technical modifications allowed. The Licensor authorizes You to exercise the Licensed Rights in all media and formats whether now known or hereafter created, and to make technical modifications necessary to do so. The Licensor waives and/or agrees not to assert any right or authority to forbid You from making technical modifications necessary to exercise the Licensed Rights, including technical modifications necessary to circumvent Effective Technological Measures. For purposes of this Public License, simply making modifications authorized by this Section 2(a)(4) never produces Adapted Material.
Downstream recipients. 
Offer from the Licensor – Licensed Material. Every recipient of the Licensed Material automatically receives an offer from the Licensor to exercise the Licensed Rights under the terms and conditions of this Public License.
No downstream restrictions. You may not offer or impose any additional or different terms or conditions on, or apply any Effective Technological Measures to, the Licensed Material if doing so restricts exercise of the Licensed Rights by any recipient of the Licensed Material.
No endorsement. Nothing in this Public License constitutes or may be construed as permission to assert or imply that You are, or that Your use of the Licensed Material is, connected with, or sponsored, endorsed, or granted official status by, the Licensor or others designated to receive attribution as provided in Section 3(a)(1)(A)(i).
Other rights.
Moral rights, such as the right of integrity, are not licensed under this Public License, nor are publicity, privacy, and/or other similar personality rights; however, to the extent possible, the Licensor waives and/or agrees not to assert any such rights held by the Licensor to the limited extent necessary to allow You to exercise the Licensed Rights, but not otherwise.
Patent and trademark rights are not licensed under this Public License.
To the extent possible, the Licensor waives any right to collect royalties from You for the exercise of the Licensed Rights, whether directly or through a collecting society under any voluntary or waivable statutory or compulsory licensing scheme. In all other cases the Licensor expressly reserves any right to collect such royalties, including when the Licensed Material is used other than for NonCommercial purposes.
Section 3 – License Conditions.
Your exercise of the Licensed Rights is expressly made subject to the following conditions.
Attribution.
If You Share the Licensed Material, You must:
retain the following if it is supplied by the Licensor with the Licensed Material: 
identification of the creator(s) of the Licensed Material and any others designated to receive attribution, in any reasonable manner requested by the Licensor (including by pseudonym if designated);
a copyright notice;
a notice that refers to this Public License; 
a notice that refers to the disclaimer of warranties;
a URI or hyperlink to the Licensed Material to the extent reasonably practicable;
indicate if You modified the Licensed Material and retain an indication of any previous modifications; and
indicate the Licensed Material is licensed under this Public License, and include the text of, or the URI or hyperlink to, this Public License.
For the avoidance of doubt, You do not have permission under this Public License to Share Adapted Material. 
You may satisfy the conditions in Section 3(a)(1) in any reasonable manner based on the medium, means, and context in which You Share the Licensed Material. For example, it may be reasonable to satisfy the conditions by providing a URI or hyperlink to a resource that includes the required information.
If requested by the Licensor, You must remove any of the information required by Section 3(a)(1)(A) to the extent reasonably practicable.
Section 4 – Sui Generis Database Rights.
Where the Licensed Rights include Sui Generis Database Rights that apply to Your use of the Licensed Material:
for the avoidance of doubt, Section 2(a)(1) grants You the right to extract, reuse, reproduce, and Share all or a substantial portion of the contents of the database for NonCommercial purposes only and provided You do not Share Adapted Material;
if You include all or a substantial portion of the database contents in a database in which You have Sui Generis Database Rights, then the database in which You have Sui Generis Database Rights (but not its individual contents) is Adapted Material; and
You must comply with the conditions in Section 3(a) if You Share all or a substantial portion of the contents of the database.
For the avoidance of doubt, this Section 4 supplements and does not replace Your obligations under this Public License where the Licensed Rights include other Copyright and Similar Rights. 
Section 5 – Disclaimer of Warranties and Limitation of Liability.
Unless otherwise separately undertaken by the Licensor, to the extent possible, the Licensor offers the Licensed Material as-is and as-available, and makes no representations or warranties of any kind concerning the Licensed Material, whether express, implied, statutory, or other. This includes, without limitation, warranties of title, merchantability, fitness for a particular purpose, non-infringement, absence of latent or other defects, accuracy, or the presence or absence of errors, whether or not known or discoverable. Where disclaimers of warranties are not allowed in full or in part, this disclaimer may not apply to You.
To the extent possible, in no event will the Licensor be liable to You on any legal theory (including, without limitation, negligence) or otherwise for any direct, special, indirect, incidental, consequential, punitive, exemplary, or other losses, costs, expenses, or damages arising out of this Public License or use of the Licensed Material, even if the Licensor has been advised of the possibility of such losses, costs, expenses, or damages. Where a limitation of liability is not allowed in full or in part, this limitation may not apply to You.
The disclaimer of warranties and limitation of liability provided above shall be interpreted in a manner that, to the extent possible, most closely approximates an absolute disclaimer and waiver of all liability.
Section 6 – Term and Termination.
This Public License applies for the term of the Copyright and Similar Rights licensed here. However, if You fail to comply with this Public License, then Your rights under this Public License terminate automatically.
Where Your right to use the Licensed Material has terminated under Section 6(a), it reinstates:
automatically as of the date the violation is cured, provided it is cured within 30 days of Your discovery of the violation; or
upon express reinstatement by the Licensor.
For the avoidance of doubt, this Section 6(b) does not affect any right the Licensor may have to seek remedies for Your violations of this Public License.
For the avoidance of doubt, the Licensor may also offer the Licensed Material under separate terms or conditions or stop distributing the Licensed Material at any time; however, doing so will not terminate this Public License.
Sections 1, 5, 6, 7, and 8 survive termination of this Public License.
Section 7 – Other Terms and Conditions.
The Licensor shall not be bound by any additional or different terms or conditions communicated by You unless expressly agreed.
Any arrangements, understandings, or agreements regarding the Licensed Material not stated herein are separate from and independent of the terms and conditions of this Public License.
Section 8 – Interpretation.
For the avoidance of doubt, this Public License does not, and shall not be interpreted to, reduce, limit, restrict, or impose conditions on any use of the Licensed Material that could lawfully be made without permission under this Public License.
To the extent possible, if any provision of this Public License is deemed unenforceable, it shall be automatically reformed to the minimum extent necessary to make it enforceable. If the provision cannot be reformed, it shall be severed from this Public License without affecting the enforceability of the remaining terms and conditions.
No term or condition of this Public License will be waived and no failure to comply consented to unless expressly agreed to by the Licensor.
Nothing in this Public License constitutes or may be interpreted as a limitation upon, or waiver of, any privileges and immunities that apply to the Licensor or You, including from the legal processes of any jurisdiction or authority.
Creative Commons is not a party to its public licenses. Notwithstanding, Creative Commons may elect to apply one of its public licenses to material it publishes and in those instances will be considered the “Licensor.” The text of the Creative Commons public licenses is dedicated to the public domain under the CC0 Public Domain Dedication. Except for the limited purpose of indicating that material is shared under a Creative Commons public license or as otherwise permitted by the Creative Commons policies published at creativecommons.org/policies, Creative Commons does not authorize the use of the trademark “Creative Commons” or any other trademark or logo of Creative Commons without its prior written consent including, without limitation, in connection with any unauthorized modifications to any of its public licenses or any other arrangements, understandings, or agreements concerning use of licensed material. For the avoidance of doubt, this paragraph does not form part of the public licenses.

Creative Commons may be contacted at creativecommons.org.
## Software License
The MIT License (MIT) 
Copyright (c) 2016 Aaron N Gray

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
