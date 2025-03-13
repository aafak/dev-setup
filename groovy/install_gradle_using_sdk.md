# First Install SDKMAN!

```
aafak@aafak-vm:~/java_install$ curl -s "https://get.sdkman.io" | bash

                                -+syyyyyyys:
                            `/yho:`       -yd.
                         `/yh/`             +m.
                       .oho.                 hy                          .`
                     .sh/`                   :N`                `-/o`  `+dyyo:.
                   .yh:`                     `M-          `-/osysoym  :hs` `-+sys:      hhyssssssssy+
                 .sh:`                       `N:          ms/-``  yy.yh-      -hy.    `.N-````````+N.
               `od/`                         `N-       -/oM-      ddd+`     `sd:     hNNm        -N:
              :do`                           .M.       dMMM-     `ms.      /d+`     `NMMs       `do
            .yy-                             :N`    ```mMMM.      -      -hy.       /MMM:       yh
          `+d+`           `:/oo/`       `-/osyh/ossssssdNMM`           .sh:         yMMN`      /m.
         -dh-           :ymNMMMMy  `-/shmNm-`:N/-.``   `.sN            /N-         `NMMy      .m/
       `oNs`          -hysosmMMMMydmNmds+-.:ohm           :             sd`        :MMM/      yy
      .hN+           /d:    -MMMmhs/-.`   .MMMh   .ss+-                 `yy`       sMMN`     :N.
     :mN/           `N/     `o/-`         :MMMo   +MMMN-         .`      `ds       mMMh      do
    /NN/            `N+....--:/+oooosooo+:sMMM:   hMMMM:        `my       .m+     -MMM+     :N.
   /NMo              -+ooooo+/:-....`...:+hNMN.  `NMMMd`        .MM/       -m:    oMMN.     hs
  -NMd`                                    :mm   -MMMm- .s/     -MMm.       /m-   mMMd     -N.
 `mMM/                                      .-   /MMh. -dMo     -MMMy        od. .MMMs..---yh
 +MMM.                                           sNo`.sNMM+     :MMMM/        sh`+MMMNmNm+++-
 mMMM-                                           /--ohmMMM+     :MMMMm.       `hyymmmdddo
 MMMMh.                  ````                  `-+yy/`yMMM/     :MMMMMy       -sm:.``..-:-.`
 dMMMMmo-.``````..-:/osyhddddho.           `+shdh+.   hMMM:     :MmMMMM/   ./yy/` `:sys+/+sh/
 .dMMMMMMmdddddmmNMMMNNNNNMMMMMs           sNdo-      dMMM-  `-/yd/MMMMm-:sy+.   :hs-      /N`
  `/ymNNNNNNNmmdys+/::----/dMMm:          +m-         mMMM+ohmo/.` sMMMMdo-    .om:       `sh
     `.-----+/.`       `.-+hh/`         `od.          NMMNmds/     `mmy:`     +mMy      `:yy.
           /moyso+//+ossso:.           .yy`          `dy+:`         ..       :MMMN+---/oys:
         /+m:  `.-:::-`               /d+                                    +MMMMMMMNh:`
        +MN/                        -yh.                                     `+hddhy+.
       /MM+                       .sh:
      :NMo                      -sh/
     -NMs                    `/yy:
    .NMy                  `:sh+.
   `mMm`               ./yds-
  `dMMMmyo:-.````.-:oymNy:`
  +NMMMMMMMMMMMMMMMMms:`
    -+shmNMMMNmdy+:`


                                                                 Now attempting installation...


Looking for a previous installation of SDKMAN...
Looking for unzip...
Looking for zip...
Looking for tar...
Looking for curl...
Looking for sed...
Installing SDKMAN scripts...
Create distribution directories...
Getting available candidates...
Prime platform file...
Prime the config file...
Installing script cli archive...
* Downloading...
######################################################################## 100.0%
* Checking archive integrity...
* Extracting archive...
* Copying archive contents...
* Cleaning up...

Installing script cli archive...
* Downloading...
######################################################################## 100.0%
* Checking archive integrity...
* Extracting archive...
* Copying archive contents...
* Cleaning up...

Set version to 5.19.0 ...
Set native version to 0.6.0 ...
Attempt update of interactive bash profile on regular UNIX...
Added sdkman init snippet to /home/aafak/.bashrc
Attempt update of zsh profile...
Updated existing /home/aafak/.zshrc

All done!

You are subscribed to the STABLE channel.

Please open a new terminal, or run the following in the existing one:

    source "/home/aafak/.sdkman/bin/sdkman-init.sh"

Then issue the following command:

    sdk help

Enjoy!!!
aafak@aafak-vm:~/java_install$
```

# Load SDKMAN! in the Current Session

```
aafak@aafak-vm:~/java_install$ source "$HOME/.sdkman/bin/sdkman-init.sh"
```

# To make this persistent, add it to your .bashrc or .zshrc:
```
aafak@aafak-vm:~/java_install$ echo 'source "$HOME/.sdkman/bin/sdkman-init.sh"' >> ~/.bashrc
aafak@aafak-vm:~/java_install$ source ~/.bashrc
```

 #Verify SDKMAN!
 ```
 aafak@aafak-vm:~/java_install$ sdk version
SDKMAN!
script: 5.19.0
native: 0.6.0 (linux x86_64)
aafak@aafak-vm:~/java_install$
```

# Install java:
 - https://github.com/aafak/dev-setup/blob/main/java/install_java_using_sdk.md
   
#  Install Gradle 8.12.1

```
aafak@aafak-vm:~/java_install$ sdk install gradle 8.12.1

Downloading: gradle 8.12.1

In progress...

######################################################################################################################### 100.0%######################################################################################################################### 100.0%

Installing: gradle 8.12.1
Done installing!


Setting gradle 8.12.1 as default.
aafak@aafak-vm:~/java_install$

```

# After installation, use the installed version:

```
aafak@aafak-vm:~/java_install$ sdk use gradle 8.12.1

Using gradle version 8.12.1 in this shell.
aafak@aafak-vm:~/java_install$

```

# Verify Installation
```

aafak@aafak-vm:~/java_install$ gradle --version

Welcome to Gradle 8.12.1!

Here are the highlights of this release:
 - Enhanced error and warning reporting with the Problems API
 - File-system watching support on Alpine Linux
 - Build and test Swift 6 libraries and apps

For more details see https://docs.gradle.org/8.12.1/release-notes.html


------------------------------------------------------------
Gradle 8.12.1
------------------------------------------------------------

Build time:    2025-01-24 12:55:12 UTC
Revision:      0b1ee1ff81d1f4a26574ff4a362ac9180852b140

Kotlin:        2.0.21
Groovy:        3.0.22
Ant:           Apache Ant(TM) version 1.10.15 compiled on August 25 2024
Launcher JVM:  17.0.11 (JetBrains s.r.o. 17.0.11+1-b1207.20)
Daemon JVM:    /home/aafak/.sdkman/candidates/java/17.0.11-jbr (no JDK specified, using current Java home)
OS:            Linux 6.11.0-19-generic amd64

aafak@aafak-vm:~/java_install$

```
