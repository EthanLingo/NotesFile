#来源/转载 
#笔记 
#资料 

[[Octave]]
[[安装]]

Octave for macOS
================

[Jump to navigation](https://wiki.octave.org/Octave_for_macOS#mw-head)[Jump to search](https://wiki.octave.org/Octave_for_macOS#searchInput)

On macOS systems GNU Octave can be installed by:

1.  macOS App Bundles **"Octave.app"** (a single [dmg-file](https://en.wikipedia.org/wiki/Apple_Disk_Image))
2.  macOS [package managers](https://wiki.octave.org/Octave_for_macOS#Package_Managers).

macOS App Bundles\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=1 "Edit section: macOS App Bundles")\]
--------------------------------------------------------------------------------------------------------------------------------------------------

The [Octave.app project](https://octave-app.org/) provides an unofficial ready-to-use macOS App Bundle installer based on [Homebrew](https://wiki.octave.org/Octave_for_macOS#Homebrew) (see below).

-   [Download installer from GitHub](https://github.com/octave-app/octave-app/releases)

A **very old** installer is hosted on SourceForge.

-   [macOS App Bundle of Octave 4.0.3 (with GUI)](https://sourceforge.net/projects/octave/files/Octave%20MacOSX%20Binary/2016-07-11-binary-octave-4.0.3/octave_gui_403_appleblas.dmg/download) (OS X 10.9+)

Package Managers\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=2 "Edit section: Package Managers")\]
------------------------------------------------------------------------------------------------------------------------------------------------

All [package managers](https://en.wikipedia.org/wiki/Package_manager) below are given in alphabetical order. The Octave developers do not recommend a certain package manager.

### Homebrew\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=3 "Edit section: Homebrew")\]

→ _Link to [Octave package](https://formulae.brew.sh/formula/octave) there._

[Homebrew](https://brew.sh/) was written 2009 by Max Howell and has gained popularity in the Ruby on Rails community and earned praise for its extensibility.

**Install GNU Octave using Homebrew:**

1.  Install [Xcode](https://developer.apple.com/xcode/) via the **Mac App Store**.
    -   Install the **Command Line Tools** by [opening a terminal](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac) and type 
        
        sudo xcode-select --install
    
2.  Follow [Homebrew's installation instructions](https://brew.sh/).
3.  Ensure brew itself has the latest definitions 
    
    brew update
    
4.  Install Octave [\[1\]](https://wiki.octave.org/Octave_for_macOS#cite_note-1)
    
    brew install octave
    

#### Further reading\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=4 "Edit section: Further reading")\]

The default charting package in Octave is straight qt. However, on the Mac gnuplot often works better. To switch to gnuplot, place the following text in your ~/.octaverc file:

setenv('GNUTERM','qt')
graphics\_toolkit("gnuplot")

Note: If brew complains about:

Linking /usr/local/Cellar/ghostscript/9.14...
Error: Could not symlink share/ghostscript/Resource
/usr/local/share/ghostscript is not writable.

This is telling you the user permissions for ghostscript are not setup in a way that your user profile can use. You need to change those permissions to your user profile. The following command will repair the issue:

sudo chown -R \`whoami\` /usr/local/share/ghostscript
brew link --overwrite ghostscript

Then run the `brew install octave` command again.

Note: If brew complains about not having a formula for octave, the following command should fix it:

brew tap --repair

The command below upgrades Octave and its dependencies to the latest Homebrew-supported versions:

brew update && brew upgrade octave

Octave has a built-in GUI (developed using Qt lib) installed by default so that gnuplot and other tools can use it directly. This GUI is always installed when installing Octave using Homebrew.

In case of trouble, see the [Homebrew Troubleshooting Guide](https://docs.brew.sh/Troubleshooting), which assists in diagnosing problems and craft useful bug reports. Bugs may be reported at [Homebrew-core's issue tracker](https://github.com/Homebrew/homebrew-core/issues).

### MacPorts\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=5 "Edit section: MacPorts")\]

→ _Link to [Octave package](https://github.com/macports/macports-ports/blob/master/math/octave/Portfile) there._

[MacPorts](http://www.macports.org/), formerly called DarwinPorts, was started in 2002 as part of the OpenDarwin project, with the involvement of a number of Apple Inc. employees including Landon Fuller, Kevin Van Vechten, and Jordan Hubbard.

**Install GNU Octave using MacPorts:**

1.  Install [Xcode](https://developer.apple.com/xcode/) via the **Mac App Store**.
    -   Install the **Command Line Tools** by [opening a terminal](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac) and type 
        
        sudo xcode-select --install
    
2.  Follow [MacPorts' installation instructions](https://www.macports.org/install.php).
3.  Update your installation 
    
    sudo port selfupdate
    sudo port upgrade outdated
    
4.  Install Octave 
    
    sudo port install octave
    

### Spack\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=6 "Edit section: Spack")\]

→ _Link to [Octave package](https://github.com/spack/spack/blob/develop/var/spack/repos/builtin/packages/octave/package.py) there._

[Spack](https://spack.io/) is a package management tool that supports the installation of multiple versions of software on macOS and other operating systems. It was created 2013 by Todd Gamblin and is currently being updated and developed by a large list of contributors (mainly via [GitHub](https://github.com/spack/spack)).

**Install GNU Octave using Spack:**

1.  Install [Xcode](https://developer.apple.com/xcode/) via the **Mac App Store**.
    -   Install the **Command Line Tools** by [opening a terminal](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac) and type 
        
        sudo xcode-select --install
    
2.  Follow [Spack tutorial](https://spack-tutorial.readthedocs.io/en/latest/).
3.  Update Spack by going to the local Spack repository (develop branch) folder and run 
    
    git pull
    
4.  Install Octave 
    
    spack install octave
    
5.  To use Octave we need to first load the package 
    
    spack load octave
    

[![Info icon.svg](https://wiki.octave.org/wiki/images/thumb/a/ae/Info_icon.svg/26px-Info_icon.svg.png)](https://wiki.octave.org/File:Info_icon.svg)

The entire installation process can **take up to a few hours**. Octave has many dependencies which will be downloaded and installed prior to Octave.

In case of trouble, please visit the [Spack repo issues list](https://github.com/spack/spack/issues), and browse through Octave related issues by writing `is:issue octave` in the filters box.

Create a launcher app with AppleScript\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=7 "Edit section: Create a launcher app with AppleScript")\]
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Open the "AppleScript Editor" application and write the following text in the editor window:

tell application "Terminal"
 do script "/path/to/octave; exit"
end tell

(e.g. Homebrew installs Octave to /usr/local/bin/octave by default) or if Octave is in your default path:

tell application "Terminal"
 do script "\`which octave\`; exit"
end tell

or if you wish to start the GUI by default, without a terminal:

do shell script "/path/to/octave --force-gui”

> 上面那一句不适用于新版本，改为如下：
>
> do shell script "/path/to/octave --gui"

Then:

-   Select "Save as ..." from the "File" menu
-   In the menu that appears, select "Application" from the "File format" menu, then navigate to the "Applications" folder and save your script there as "Octave.app"

To change the application icon:

-   Open [this link](https://wiki.octave.org/File:Icon.png "File:Icon.png") in a web browser, right-click and select "copy image".
-   Select "Octave.app" in the Finder, then press command-i to bring up the file info dialog.
-   In the file info dialog, select the icon (in the top left) and press command-v to paste the Octave icon over it.

See also\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=8 "Edit section: See also")\]
--------------------------------------------------------------------------------------------------------------------------------

-   [Octave for macOS (outdated)](https://wiki.octave.org/Octave_for_macOS_(outdated) "Octave for macOS (outdated)") contains old installation instructions.

Footnotes\[[edit](https://wiki.octave.org/wiki/index.php?title=Octave_for_macOS&action=edit&section=9 "Edit section: Footnotes")\]
----------------------------------------------------------------------------------------------------------------------------------

1.  [↑](https://wiki.octave.org/Octave_for_macOS#cite_ref-1) Homebrew has updated some of its scripts. To install Octave as of May 14, 2020, provide the migrated full path by running `brew install homebrew/core/octave`instead. \[Citation needed!\]