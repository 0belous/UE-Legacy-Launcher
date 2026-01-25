# UE Legacy Launcher

An integrated version manager/downgrader for Oculus VR games built with Unreal Engine.

[Repo Mirror](https://git.obelous.dev/obelous/A2-Legacy-Launcher)

## Dependencies
- Python 3

## Get started

<details>
   <summary>Windows instructions:</summary>

   <br>
   
**Install:**

1. Install pipx

   `py -m pip install --user pipx`

2. Add pipx to PATH

   `py -m pipx ensurepath`

3. **Close and re-open command prompt**

4. Install legacy launcher

   `pipx install a2-legacy-launcher`

5. Run Legacy Launcher

   Configure a manifest in 
   
   **Note that some versions can take up to 5 attempts to launch correctly**

</details>

<details>
   <summary>Debian instructions:</summary>
   
   <br>
   
   **Install:**

1. Insall pipx

   `sudo apt install pipx`

2. Add pipx to PATH

   `pipx ensurepath`

3. Install java

   `sudo apt install openjdk-21-jdk`

4. Install legacy launcher

   `pipx install a2-legacy-launcher`

5. Run Legacy Launcher

   Check `a2ll -ls` for available versions.

   **Note that some versions can take up to 5 attempts to launch correctly**

</details>

<details>
   <summary>MacOS instructions:</summary>
   
   <br>

   > Currently only Intel Macs are supported, if you own an ARM Mac please DM me
   
   **Install:**

1. Install homebrew

   `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

2. Install dependencies

   `brew install python3 pipx openjdk`

3. Add pipx to PATH

   `pipx ensurepath`

4. **Close and re-open terminal**

5. Add java to PATH

   `sudo ln -sfn /usr/local/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk`
   `echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc`
   `echo 'export CPPFLAGS="-I/opt/homebrew/opt/openjdk/include"' >> ~/.zshrc`
   `source ~/.zshrc`

6. Install legacy launcher

   `pipx install a2-legacy-launcher`

7. Run Legacy Launcher

   Check `a2ll -ls` for available versions.

   **Note that some versions can take up to 5 attempts to launch correctly**

</details>

<details>
   <summary>Quest instructions</summary>

   <br>

   Only follow these steps if you dont have access to a Windows/Linux/Mac computer:
   
   **Install:**

1. Connect to a computer or [android phone](https://play.google.com/store/apps/details?id=eu.sisik.hackendebug)

   Run `adb tcpip 5555`

3. Install termux

   [Termux APK](https://github.com/termux/termux-app/releases/download/v0.118.3/termux-app_v0.118.3+github-debug_arm64-v8a.apk)

4. Run the helper script in termux
   
   ```
   curl -L https://obelous.dev/a2ll.sh | bash
   ```
   
   I suggest opening this page on the quest browser and copy pasting this command.

   **Note that some versions can take up to 5 attempts to launch correctly**

</details>

## Usage

```
UE Legacy Launcher

positional arguments:
  download              Build version to download and install

options:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -a APK, --apk APK     Path/URL to an APK file
  -o OBB, --obb OBB     Path/URL to an OBB file
  -i INI, --ini INI     Path/URL/Preset for Engine.ini
                        Presets: Engine.ini, EngineVegas.ini, Engine4v4.ini, EngineNetworked.ini, EnginePlayerstart.ini
  -c COMMANDLINE, --commandline COMMANDLINE
                        Launch arguments for A2
  -so SO, --so SO       Inject a custom .so file
  -rn, --rename         Rename the package for parallel installs
  -p PATCH, --patch PATCH
                        Byte pattern to patch
  -rm, --remove         Uninstall all versions
  -l, --logs            Pull game logs from the headset
  -ls, --list           List available versions
  -op, --open           Launch the game once finished
  -sp, --strip          Strip permissions to skip pompts on first launch
  -sk, --skipdecompile  Reuse previously decompiled files
  -cc, --clearcache     Delete cached downloads
  -r, --restore         Restore to the latest version
```

#### Extra context:

- `a2ll [Date/version code/CL/1.0.CL]` This automatically downloads a version and uses the correct flags to install it, renaming if possible.

- `--clearcache` When providing a URL to the APK OBB or INI argument the script downloads and caches the file, to free up storage and delete cached downloads run the script with this argument.

- `--skipdecompile` When iterating on a single version you may wish to skip the decopilation step to save time by using the previously decompiled files, this also allows for manual modification of game files in the temp/decompiled folder.

- `--rename` This renames the package to com.LegacyLauncher.A2 to allow for multiple versions to be installed at once, but it must be used in conjunction with `-c="-useinsecure"` on a version where this argument exists.

   > If a renamed version is installed the `--log` argument pulls the logs of the last version to run.

- `--commandline` Various features can be unlocked through the use of commandline options, for example: `-c="-nullrhi"`

- `--ini` is unique because it can be ran on its own without rebuilding or reinstalling to almost instantly swap out an ini file

### Config:

The config.yml file located at `%USERPROFILE%/.a2-legacy-launcher/config.yml` currently has these settings:

```yml
autoupdate: true
manifest_url: (Manifest URL Here)
```

Auto update defaults to true so the script will update itself using update.bat or update.sh

Specifying a manifest allows the program to automatically select the arguments to install a desired version. See the example.json for how to format your own manifest.

<hr>
