# builder
Software Builder

rough outline specification

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
 - RPM
 - .deb
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

## license
The MIT License (MIT) 
Copyright (c) 2016 Aaron N Gray

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
