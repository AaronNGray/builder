# builder
Software Builder

## builder

**builder** should have node npm like functionality as well as Visual Studio like solution / project structure.
dependant modules maybe all stored in one flattened two tier (project and vesion) heirachy in the users root directory instead of npm like spawl.

## directory structure


home
    modules
        <name>
            <vesion>

    projects
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

variables
    environment variables

        <environment>
            <variable>
                name
                optional mapping
                optional default
                optional value

    defines & defaults

        <define>
            <variable>
                name
                optional value

types
    bool
    string
    number
    enumeration
    struct ? do we really need this ?

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



<tool>
    parameters
    input(s)
    output(s)
    command line

        <command>...</command>

        <commands>
            <command>...</command>
            ...
        </commands>

<tool-chain>

    <tool name="...">
        ...
    </tool>

    <tool name="...">
        ...
    </tool>

</tool-chain>


solution and projects

    <solution>
        <project>


import - for libraries
export

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

### http(s) support
### ftp support

### implementation ###

