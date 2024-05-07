# `makedeb` Installation via Source Code

`makedeb` is an essential tool in Arch Linux for creating packages from PKGBUILD files. Let's go step by step:

1. **Install the basic system dependencies**:
   Make sure you have the following packages installed:

   ```bash
   sudo apt install build-essential linux-headers-$(uname -r) git
   ```

2. **Install the necessary dependencies for `makedeb`**:
   Run the following command to install the dependencies:

   ```bash
   sudo apt install apt binutils curl fakeroot file gettext gawk libarchive-tools lsb-release zstd
   ```

3. **Install the compilation tools**:
   The following tools are necessary to compile `makedeb`:

   ```bash
   sudo apt install asciidoctor cargo git make jq
   ```

4. **Install `just` via Cargo**:
   `just` is a useful tool for automating tasks. Install it with the following command:

   ```bash
   cargo install just
   ```

5. **Configure the environment variable**:
   Add the `~/.cargo/bin` directory to your `PATH`:

   ```bash
   echo 'export PATH="$PATH:$HOME/.cargo/bin"' >> "$HOME/.bashrc"
   source "$HOME/.bashrc"  # Update the environment
   ```

6. **Download the `makedeb` source code**:
   Let's clone the `makedeb` repository:

   ```bash
   cd ~/Downloads/
   git clone 'https://github.com/makedeb/makedeb'
   cd makedeb
   ```

7. **Compile the package**:
   Run the following commands to compile `makedeb`:

   ```bash
   VERSION="16.1.0" RELEASE=alpha TARGET=apt BUILD_COMMIT="$(git rev-parse HEAD)" just prepare
   DPKG_ARCHITECTURE="$(dpkg --print-architecture)" just build
   ```

8. **Install `makedeb`**:
   Now, install `makedeb` on the system:

   ```bash
   sudo DESTDIR='/' ~/.cargo/bin/just package
   ```

9. **Optional: Create a .deb package for testing**:
   If you wish, you can create a .deb package for future use:

   ```bash
   cd PKGBUILD
   TARGET=apt RELEASE=alpha ./pkgbuild.sh > PKGBUILD
   makedeb -s
   ```

Now you should have `makedeb` installed and ready for use! Remember to check if the `~/cargo/bin` directory is correctly configured in your `PATH`¹[1](https://www.youtube.com/watch?v=dg0O8eoDlTI).

Sources:  
(1) Install from AUR using only makepkg. https://www.youtube.com/watch?v=dg0O8eoDlTI.  
(2) How to download and install PACOTE OFFICE for Free - Complete Video Lesson 2023. https://www.youtube.com/watch?v=kVyJ2BVUUSY.  
(3) How to install the Office 365 package for free - Word, PowerPoint, Excel, Outlook, and more. https://www.youtube.com/watch?v=d1ZDjEqJNcg.  
(4) Makepkg (Portuguese) - ArchWiki. https://wiki.archlinux.org/title/Makepkg_%28Portugu%C3%AAs%29.  
(5) makepkg(8) — Arch manual pages. https://man.archlinux.org/man/makepkg.8.pt_BR.  
(6) makepkg - ArchWiki. https://wiki.archlinux.org/title/Makepkg.  
(7) undefined. https://bing.com/search?q=.  
(8) How to Use the Command `makepkg` (with examples). https://commandmasters.com/commands/makepkg-linux/.  
(9) Creating a PKGBUILD to Make Packages for Arch Linux - It's FOSS. https://itsfoss.com/create-pkgbuild/.  
(10) makepkg Command Examples in Linux – The Geek Diary. https://www.thegeekdiary.com/makepkg-command-examples-in-linux/.
