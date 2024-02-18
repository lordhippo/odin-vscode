# odin-vscode
A bunch of helper files to improve workflows for developing [Odin](https://odin-lang.org/) programs in VS Code:
- Tasks
    - Building and cleaning
    - Checking
    - Memory profiling
- Show compiler errors and warnings as VS Code *Problems* on the correct file and line
- Launch tasks for debug and release
# Odin setup
In case you haven't done already.
1. Get and build the [compiler](https://github.com/odin-lang/Odin)
    - Add Odin root to path, and as `ODIN_ROOT`
2. Get and build the [language server]( https://github.com/DanielGavin/ols)
3. Install the [OLS extension](https://marketplace.visualstudio.com/items?itemName=DanielGavin.ols)
    - set the `ols.server.path` to the ols binary
4. In your project root
    - Create `ols.json` either from [OLS github](https://github.com/DanielGavin/ols?tab=readme-ov-file#configuration), or use the one included in this repo
    - Create `odinfmt.json` either from [OLS github](https://github.com/DanielGavin/ols?tab=readme-ov-file#odinfmt-configurations), or use the one included in this repo
5. Open the folder in VS code, ideally using the workspace file. This is important, as opening files individually won’t work.
# VS Code specifics
## Build tasks
To add debug and release build targets and get errors work with VS Code’s Problems, use this as the `.vscode\tasks.json` included in the repo.
There are 5 tasks in it:

1. **Build - Debug**: builds the package corresponding to the currently open file, in *debug* mode
2. **Build - Release**: builds the package corresponding to the currently open file, in *release* mode
3. **Check**: Runs Odin’s check command. It doesn’t produce any artifacts
4. **Clean**: Deletes the output folder
5. **Profile Memory**: Builds and memory profiles the binary using [MTuner](https://www.notion.so/How-to-profile-memory-b711ad9a7d3b4ceca28e10cb7f4ddce0?pvs=21)

Output folder is `[workspace-root]/out/[build-mode]`.

I also suggest using [Error Lens extension](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens) to show the errors inline.
## Debugging
If you have Visual Studio installed, you can use its cpp debugger on windows to debug Odin programs in VS Code. Use the `.vscode/launch.json` to add the corresponding launch tasks.
After that, use the **Launch - Debug** preset (mapped to **F5**) to debug the currently open package.
### Using RAD debugger
Alternatively, you can use [The RAD Debugger](https://github.com/EpicGames/raddebugger) to debug Odin programs.
1. Get and build the [debugger](https://github.com/EpicGames/raddebugger)
2. Build odin project with `-debug`. This generates the `.pdb` file. You can do it by using the **Build - Debug** task from this repo.
3. In RAD debugger, set `[package-name].main` as the **Custom Entry Point**
## Memory Profiling
1. Get the latest [MTuner](https://github.com/RudjiGames/MTuner/releases)
2. Add the unpacked folder to the `PATH` environment variable
3. Either
    - Open MTuner and drop the binary on it, or
    - Inside VS Code, use the **Profile Memory** task to build and profile