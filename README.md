# Isetta-Game
The sample, demo game for the IsettaEngine

# Setup Steps
Choose **one** of the following two options to set up:
### Option 1: To setup using our template project
- Download this repo as a zip
- Retarget the solution:
    - Open up the `.sln`
    - Right-click the solution (GameTemplate Solution)
    - Select `Retarget Solution`, then just select ok
- In /GameTemplate/GameTemplate, create a `user.cfg` file, we will introduce how to use it later.

### Option 2: To setup a new project using the IsettaEngine:
- Create a Visual Studio Project
- Create a `.cpp` file to start the engine, copy:
    ```cpp
    #include <EngineLoop.h>

    int main() {
        Isetta::Application::Start();
        return 0;
    }
    ```
- Download zip file of the [engine](https://github.com/Isetta-Team/Isetta-GameTemplate/releases/tag/gamejam) (includes `.dll` and `.h`)
    - Extract in `.sln` directory
- Project Properties:
    - Configuration Manager > Active solution platform: > <Edit...> > Click x86 > Remove
    - Configuration Manager > Active solution configuration: > <New...> > Put "ReleaseEditor" in name > OK
    - (Make sure you do the following changes with "All Configurations" selected as Configuration)
    - Debugging > Change Working Directory to "$(TargetDir)"
    - C/C++ (you will need a .cpp file to view this section)
        - General > Additional Includes: > Add `$(SolutionDir)Engine; $(SolutionDir)Engine\External;`
        - Language > C++ Language Standard > `ISO C++17 Standard (/std:c++17)`
    - Linker > Input > Add `$(SolutionDir)Engine\Build\*.lib;`
        - This will need to be different for `Debug` and `Release` builds (not currently setup)
    - Build Events
        - Pre-Build Event > Command Line > Add `XCOPY /Y /R "$(SolutionDir)Engine\Build\*.dll" "$(TargetDir)"`
        - Post-Build Event > Command Line > Add:
        ```
        XCOPY /Y /R /S /I "$(SolutionDir)Engine\Resources\*" "$(TargetDir)Resources"
        XCOPY /Y /R /S /I "$(ProjectDir)Resources\*" "$(TargetDir)Resources"
        XCOPY /Y /R "$(ProjectDir)*.cfg" "$(TargetDir)"
        ```
- Configuration files
    - Create a `config.cfg` or copy a premade one (see Engine/Resources/Config/)
        - No `.cfg` in Engine/Resources/Config/ currently
    - Create a `user.cfg` for any other custom options
        - This file is not mandatory

## Prebuilt/Packaged Engine Levels
|  Level Name       |   Level Description                                           |   Level Inputs    |
|      :-:          |           :-:                                                 |       :-:         |
|  `EmptyLevel`    |   A level with only a camera and nothing else   | N/A |

## For more information, look at [our website](https://isetta.io/engine_docs/home)
