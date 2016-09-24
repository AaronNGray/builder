# builder
Software Builder

## builder

**builder** should have node npm like functionality as well as Visual Studio like solution / project structure.
dependant modules maybe all stored in one flattened two tier (project and vesion) heirachy in the users root directory instead of npm like spawl.

## investigation
 - MSBuild import/reference with mappings
 - npm import/reference
 - visual studio import/export with mappings
 - make & nmake file export

## directory structure

    <home>
        **modules**
            <name>
                <vesion>

        **projects**
            <solution-root>
                <projects-name>
                    include
                    src
                    build
                        debug
                        release
                modules
                    <name>
                        <version>
                            ...


## git interop
git interop should be implicit

## file format
Files are either in a XML or a scoped format [files maybe either XML or YAML or probably just YAML with XML conversion. ]

## variables
### environment variables

        <environment>
            <variable>
                name
                optional mapping
                optional default
                optional value

### defines & defaults

        <define>
            <variable>
                name
                optional value

## types
 -  bool
 -  string
 -  number
 -  enumeration
 -  struct ? do we really need this ?

    <types>
        <type>
            <bool name="..." default="...">
            <string>
            <number>
            <enum>

                <enum name="..." type="..." default="...">
                    <value name="..." value="..."/>
                </enum>

            <struct name="...">

## tools

<tool>
    parameters
    input(s)
    output(s)
    command line

    <tool name="...">
        <command>...</command>
    </tool>

    <tool name="...">
        <commands>
            <command>...</command>
            <command>...</command>
            ...
        </commands>
    </tool>

## tool chain

    <tool-chain name="...">
        <tool name="...">
            ...
        </tool>
        <tool name="...">
            ...
        </tool>
    </tool-chain>

## solution and projects

    <solution>
        <project>

## rules

    <rules name="...">
        <rule name="...">
            <destinations>
                <destination name="..." path="...">
            </destinations>
            <sources>
                <source name="..." path="...">
            </source>
            <command|commands>
        </rule>
    </rules>

## import - for libraries
## export

    <export>
        <includes>
        <libraries>
            <debug>
            <release>


### bulider command line

#### new project

    mkdir <project name>
    cd <project name>
    b init

or just

    b init <project name>
    cd <project name>

#### git support

    b init <project name> <blank-git-repo>
    cd <project name>

#### http(s) support
#### ftp support

## implementation

## license
The MIT License (MIT) 
Copyright (c) 2016 Aaron N Gray

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
