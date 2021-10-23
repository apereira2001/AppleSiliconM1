# CocoaPods on M1 (Apple Silicon) fails with ffi wrong architecture
<pre ">

When I tried to run 'pod install' on the M1 MacBook, I got the following error messages:

LoadError - dlopen(/opt/homebrew/lib/ruby/gems/3.0.0/gems/ffi-1.15.0/lib/ffi_c.bundle, 9): no suitable image found.  Did find:
    /opt/homebrew/lib/ruby/gems/3.0.0/gems/ffi-1.15.0/lib/ffi_c.bundle: mach-o, but wrong architecture
    /opt/homebrew/lib/ruby/gems/3.0.0/gems/ffi-1.15.0/lib/ffi_c.bundle: mach-o, but wrong architecture - /opt/homebrew/lib/ruby/gems/3.0.0/gems/ffi-1.15.0/lib/ffi_c.bundle

Searching for this error, I found some answers on the stackoverflow website,  which you can check on the following link:

https://stackoverflow.com/questions/66644365/cocoapods-on-m1-apple-silicon-fails-with-ffi-wrong-architecture

I've tested Datasun's, Burtsevyg and Rhys Broughton answers, but it still didn't work for me.

Then I tried to mix all and did the following:

I ran the following lines in terminal:

First uninstall gem

appleM1@appleM1-MacBook-Pro ~ % cd

appleM1@appleM1-MacBook-Pro ~ % gem list --local | grep cocoapods | awk '{print $1}' | xargs sudo gem uninstall

Then install cocoapods using brew, so I used:

brew install cocoapods

Now install ffi with:

sudo gem install ffi

Done!!!

Below I pasted a copy of what I ran in my terminal session:

appleM1@appleM1-MacBook-Pro ~ % flutter doctor -v

[✓] Flutter (Channel stable, 2.5.3, on macOS 11.6 20G165 darwin-arm, locale en-US)
    • Flutter version 2.5.3 at /Users/appleM1/Devel/flutter
    • Upstream repository https://github.com/flutter/flutter.git
    • Framework revision 18116933e7 (8 days ago), 2021-10-15 10:46:35 -0700
    • Engine revision d3ea636dc5
    • Dart version 2.14.4

[✓] Android toolchain - develop for Android devices (Android SDK version 31.0.0)
    • Android SDK at /Users/appleM1/Library/Android/sdk
    • Platform android-31, build-tools 31.0.0
    • Java binary at: /Applications/Android Studio.app/Contents/jre/Contents/Home/bin/java
    • Java version OpenJDK Runtime Environment (build 11.0.10+0-b96-7249189)
    • All Android licenses accepted.

[✓] Xcode - develop for iOS and macOS
    • Xcode at /Applications/Xcode.app/Contents/Developer
    • Xcode 13.0, Build version 13A233
    • CocoaPods version 1.11.2

[✓] Chrome - develop for the web
    • Chrome at /Applications/Google Chrome.app/Contents/MacOS/Google Chrome

[✓] Android Studio (version 2020.3)
    • Android Studio at /Applications/Android Studio.app/Contents
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart
    • Java version OpenJDK Runtime Environment (build 11.0.10+0-b96-7249189)

[✓] IntelliJ IDEA Community Edition (version 2021.2.1)
    • IntelliJ at /Applications/IntelliJ IDEA CE.app
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart

[✓] IntelliJ IDEA Ultimate Edition (version 2021.2)
    • IntelliJ at /Applications/IntelliJ IDEA Edu.app
    • Flutter plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/9212-flutter
    • Dart plugin can be installed from:
      🔨 https://plugins.jetbrains.com/plugin/6351-dart

[✓] VS Code (version 1.61.1)
    • VS Code at /Applications/Visual Studio Code.app/Contents
    • Flutter extension version 3.27.0

[✓] Connected device (3 available)
    • sdk gphone64 arm64 (mobile) • emulator-5554                        • android-arm64  • Android 12 (API 31) (emulator)
    • iPhone 13 (mobile)          • 470ACB9E-CA75-4069-93E4-2F8ED4605650 • ios            • com.apple.CoreSimulator.SimRuntime.iOS-15-0 (simulator)
    • Chrome (web)                • chrome                               • web-javascript • Google Chrome 95.0.4638.54

• No issues found!

appleM1@appleM1-MacBook-Pro ~ % gem list --local | grep cocoapods

cocoapods (1.11.2)
cocoapods-core (1.11.2)
cocoapods-deintegrate (1.0.5)
cocoapods-downloader (1.5.1)
cocoapods-plugins (1.0.0)
cocoapods-search (1.0.1)
cocoapods-trunk (1.6.0)
cocoapods-try (1.2.0)

appleM1@appleM1-MacBook-Pro ~ % brew uninstall --ignore-dependencies ruby

Error: No available formula or cask with the name "ruby". Did you mean jruby or mruby?

appleM1@appleM1s-MacBook-Pro ~ % gem list --local | grep cocoapods | awk '{print $1}' | xargs sudo gem uninstall

Password:
Removing pod
Removing sandbox-pod
Successfully uninstalled cocoapods-1.11.2
Successfully uninstalled cocoapods-try-1.2.0
Successfully uninstalled cocoapods-trunk-1.6.0
Successfully uninstalled cocoapods-search-1.0.1
Successfully uninstalled cocoapods-plugins-1.0.0
Successfully uninstalled cocoapods-downloader-1.5.1
Successfully uninstalled cocoapods-deintegrate-1.0.5
Successfully uninstalled cocoapods-core-1.11.2

appleM1@appleM1-MacBook-Pro ~ % brew install cocoapods

Updating Homebrew...
==> Auto-updated Homebrew!
Updated 1 tap (homebrew/core).
==> New Formulae
actionlint                   cmake-docs                   git-svn                      lastz                        lziprecover                  pkgconf                      terraform-rover
apache-pulsar                colima                       gomodifytags                 libavif                      microsocks                   postgresql@13                texlive
aws-sso-util                 cpufetch                     goproxy                      libnghttp2                   mmtabbarview                 python-tk@3.10               tfk8s
bat-extras                   cyral-gimme-db-token         gotests                      librist                      ncnn                         python@3.10                  tfupdate
bottom                       feroxbuster                  gtop                         lilypond                     neovim-qt                    qwt-qt5                      toml11
ca-certificates              fheroes2                     iproute2                     liqoctl                      node@16                      rbw                          vespa-cli
cassandra@3                  g2o                          jellyfish                    llvm@12                      openssl@3                    red-tldr                     viddy
clickhouse-cpp               git-cliff                    jpdfbookmarks                lunzip                       osc-cli                      selene                       viu
clickhouse-odbc              git-credential-libsecret     k2tf                         ly                           pkg-config-wrapper           solana
==> Updated Formulae
Updated 1872 formulae.
==> Renamed Formulae
selenium-server-standalone -> selenium-server
==> Deleted Formulae
ocamlsdl                                                            pandoc-citeproc                                                     vavrdiasm

==> Downloading https://ghcr.io/v2/homebrew/core/libyaml/manifests/0.2.5
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/libyaml/blobs/sha256:fe1082f3475a144261b41e2c3e0728b9331911b1cbfadfbc1f3d70d454709154
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:fe1082f3475a144261b41e2c3e0728b9331911b1cbfadfbc1f3d70d454709154?se=2021-10-23T08%3A55%3A00Z&sig=8yRwR9eKL76b5sZKfoZYK9
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/ca-certificates/manifests/2021-09-30-1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/ca-certificates/blobs/sha256:47c9cd6ec69dbbf8a3f697e6b07df409a573c779aa86ceadc7d9575e8c2a5b10
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:47c9cd6ec69dbbf8a3f697e6b07df409a573c779aa86ceadc7d9575e8c2a5b10?se=2021-10-23T08%3A55%3A00Z&sig=cuCquXnuxK0dvlS5e4p22C
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/openssl/1.1/manifests/1.1.1l_1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/openssl/1.1/blobs/sha256:e3d8556cec907ad1e0ea00aebd0b0b516dde06ea3bf24308290ad785cb360a04
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:e3d8556cec907ad1e0ea00aebd0b0b516dde06ea3bf24308290ad785cb360a04?se=2021-10-23T08%3A55%3A00Z&sig=iiOh5yIOPh6yNG3SX2NwPN
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/readline/manifests/8.1.1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/readline/blobs/sha256:bcb228b99fcecebf6ecc2b2ac80ab96a396374a8d5bc13b21034ef501017254f
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:bcb228b99fcecebf6ecc2b2ac80ab96a396374a8d5bc13b21034ef501017254f?se=2021-10-23T09%3A00%3A00Z&sig=Y9xhWF0HQnC%2BJ25fQbyd
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/ruby/manifests/3.0.2_1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/ruby/blobs/sha256:86f9be3f7ac26e69e3c856776569b1c10039716f5787821944645c6d0f10fe87
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:86f9be3f7ac26e69e3c856776569b1c10039716f5787821944645c6d0f10fe87?se=2021-10-23T09%3A00%3A00Z&sig=UQr4sbAPIvi6qaPIyZDt30
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/cocoapods/manifests/1.11.2_1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/cocoapods/blobs/sha256:d792e6ff2dbbc51e436000addd1bcf86edb34feb4b53194e64f6889d48527ee0
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:d792e6ff2dbbc51e436000addd1bcf86edb34feb4b53194e64f6889d48527ee0?se=2021-10-23T09%3A00%3A00Z&sig=3J6qfglYW8t%2BSjthJnPQ
######################################################################## 100.0%
==> Installing dependencies for cocoapods: libyaml, ca-certificates, openssl@1.1, readline and ruby
==> Installing cocoapods dependency: libyaml
==> Pouring libyaml--0.2.5.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libyaml/0.2.5: 10 files, 369.9KB
==> Installing cocoapods dependency: ca-certificates
==> Pouring ca-certificates--2021-09-30.all.bottle.1.tar.gz
==> Regenerating CA certificate bundle from keychain, this may take a while...
🍺  /opt/homebrew/Cellar/ca-certificates/2021-09-30: 3 files, 203.5KB
==> Installing cocoapods dependency: openssl@1.1
==> Pouring openssl@1.1--1.1.1l_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/openssl@1.1/1.1.1l_1: 8,073 files, 18MB
==> Installing cocoapods dependency: readline
==> Pouring readline--8.1.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/readline/8.1.1: 48 files, 1.7MB
==> Installing cocoapods dependency: ruby
==> Pouring ruby--3.0.2_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/ruby/3.0.2_1: 16,390 files, 40.4MB
==> Installing cocoapods
==> Pouring cocoapods--1.11.2_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/cocoapods/1.11.2_1: 13,456 files, 28.3MB
==> `brew cleanup` has not been run in the last 30 days, running now...
Removing: /Users/appleM1/Library/Caches/Homebrew/automake--1.16.4... (967KB)
Removing: /Users/appleM1/Library/Caches/Homebrew/nghttp2--1.44.0... (938.5KB)
Removing: /Users/appleM1/Library/Caches/Homebrew/node--16.8.0... (12.5MB)
Removing: /opt/homebrew/Cellar/openssl@1.1/1.1.1l... (8,073 files, 18MB)
Removing: /Users/appleM1/Library/Logs/Homebrew/libtool... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/nghttp2... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/libpng... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/libuv... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/freetype... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/boost... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/jemalloc... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/brotli... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/icu4c... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/sdl2_ttf... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/c-ares... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/gputils... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/autoconf... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/m4... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/openssl@1.1... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/node... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/sdl2... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/libev... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/automake... (64B)
Removing: /Users/appleM1/Library/Logs/Homebrew/telnet... (64B)
Pruned 0 symbolic links and 9 directories from /opt/homebrew
==> Upgrading 2 dependents:
nghttp2 1.44.0 -> 1.46.0, node 16.8.0 -> 17.0.1
==> Downloading https://ghcr.io/v2/homebrew/core/libnghttp2/manifests/1.46.0
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/libnghttp2/blobs/sha256:f73eb0a7cec33617af3678052a930246107b6fa0d00fc480678718227fe661a4
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:f73eb0a7cec33617af3678052a930246107b6fa0d00fc480678718227fe661a4?se=2021-10-23T09%3A00%3A00Z&sig=r3Q8mqsE0x0AS7fHlvcH3b
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/nghttp2/manifests/1.46.0
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/nghttp2/blobs/sha256:d460789e9fd34f91aa1e9e4ca1b7f19a1d404bfe5a2436137da377316efbea93
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:d460789e9fd34f91aa1e9e4ca1b7f19a1d404bfe5a2436137da377316efbea93?se=2021-10-23T09%3A00%3A00Z&sig=2ovykYt8CRZQ3H8usgzqo%
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/libnghttp2/manifests/1.46.0
Already downloaded: /Users/appleM1/Library/Caches/Homebrew/downloads/d55a2f1fb62a2e27c224645798155f3226ca864134acd4e39dd7ddf4b8f79c50--libnghttp2-1.46.0.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/libnghttp2/blobs/sha256:f73eb0a7cec33617af3678052a930246107b6fa0d00fc480678718227fe661a4
Already downloaded: /Users/appleM1/Library/Caches/Homebrew/downloads/df7bc8aa9757c607c01638d46172bf78baaefae6d3e134e983aac2006844390a--libnghttp2--1.46.0.arm64_big_sur.bottle.tar.gz
==> Downloading https://ghcr.io/v2/homebrew/core/gdbm/manifests/1.21_1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/gdbm/blobs/sha256:fd3c1830264b732ad953e0ec41dd8325ac3c07fc8bf3b8a55a968f4f8947ecc5
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:fd3c1830264b732ad953e0ec41dd8325ac3c07fc8bf3b8a55a968f4f8947ecc5?se=2021-10-23T09%3A00%3A00Z&sig=D7sy0hsbN4anBj%2FBoVoL
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/mpdecimal/manifests/2.5.1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/mpdecimal/blobs/sha256:eebbc5c7e71710c848eb60b90f946aefdee1b5269c840c30b8098d6bb758500b
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:eebbc5c7e71710c848eb60b90f946aefdee1b5269c840c30b8098d6bb758500b?se=2021-10-23T09%3A00%3A00Z&sig=zQhXD8lTGdh1WZXyODycWC
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/sqlite/manifests/3.36.0
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/sqlite/blobs/sha256:b7d98dc89e39bfd68676ce9df2e58d78e790a2591ef204800b27a454c019024a
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:b7d98dc89e39bfd68676ce9df2e58d78e790a2591ef204800b27a454c019024a?se=2021-10-23T09%3A00%3A00Z&sig=9fxZ3w8fO3eawg8iV79Hr9
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/xz/manifests/5.2.5
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/xz/blobs/sha256:c84206005787304416ed81094bd3a0cdd2ae8eb62649db5a3a44fa14b276d09f
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:c84206005787304416ed81094bd3a0cdd2ae8eb62649db5a3a44fa14b276d09f?se=2021-10-23T09%3A00%3A00Z&sig=F4ia5BVjcT5ilDR%2F6YFd
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/python/3.9/manifests/3.9.7_1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/python/3.9/blobs/sha256:c1955f1d1cf37aa0f2db6bd7acc1ff4ede09d05ec470239d4b20704766445fda
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:c1955f1d1cf37aa0f2db6bd7acc1ff4ede09d05ec470239d4b20704766445fda?se=2021-10-23T09%3A00%3A00Z&sig=AzPmRiwDUPcQ%2BFHSStUl
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/node/manifests/17.0.1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/node/blobs/sha256:4fc5759b3008c9fdaf8a8103c3abd8dc5a3b7d66a967c3c31820943118498f6b
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:4fc5759b3008c9fdaf8a8103c3abd8dc5a3b7d66a967c3c31820943118498f6b?se=2021-10-23T09%3A00%3A00Z&sig=7%2Bwn2vpH%2FIAAB0rwzu
######################################################################## 100.0%
==> Upgrading nghttp2
  1.44.0 -> 1.46.0 

==> Installing dependencies for nghttp2: libnghttp2
==> Installing nghttp2 dependency: libnghttp2
==> Pouring libnghttp2--1.46.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libnghttp2/1.46.0: 13 files, 690.3KB
==> Installing nghttp2
==> Pouring nghttp2--1.46.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/nghttp2/1.46.0: 17 files, 2.3MB
Removing: /opt/homebrew/Cellar/nghttp2/1.44.0... (23 files, 2.8MB)
==> Upgrading node
  16.8.0 -> 17.0.1 

==> Installing dependencies for node: gdbm, mpdecimal, sqlite, xz and python@3.9
==> Installing node dependency: gdbm
==> Pouring gdbm--1.21_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/gdbm/1.21_1: 24 files, 991.2KB
==> Installing node dependency: mpdecimal
==> Pouring mpdecimal--2.5.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/mpdecimal/2.5.1: 71 files, 2.2MB
==> Installing node dependency: sqlite
==> Pouring sqlite--3.36.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/sqlite/3.36.0: 11 files, 4.3MB
==> Installing node dependency: xz
==> Pouring xz--5.2.5.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/xz/5.2.5: 95 files, 1.4MB
==> Installing node dependency: python@3.9
==> Pouring python@3.9--3.9.7_1.arm64_big_sur.bottle.tar.gz
==> /opt/homebrew/Cellar/python@3.9/3.9.7_1/bin/python3 -m ensurepip
==> /opt/homebrew/Cellar/python@3.9/3.9.7_1/bin/python3 -m pip install -v --no-deps --no-index --upgrade --isolated --target=/opt/homebrew/lib/python3.9/site-packages /opt/homebrew/Cellar/python@3.9/3.9.7
🍺  /opt/homebrew/Cellar/python@3.9/3.9.7_1: 3,082 files, 56.6MB
==> Installing node
==> Pouring node--17.0.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/node/17.0.1: 2,008 files, 43.9MB
Removing: /opt/homebrew/Cellar/node/16.8.0... (2,409 files, 47MB)
==> Checking for dependents of upgraded formulae...
==> No broken dependents found!

appleM1@appleM1-MacBook-Pro ~ % 

appleM1@appleM1-MacBook-Pro ~ % gem list --local | grep cocoapods | awk '{print $1}'                           

appleM1@appleM1-MacBook-Pro ~ % pod install

[!] No `Podfile' found in the project directory.

appleM1@appleM1-MacBook-Pro ~ % sudo gem install ffi

Building native extensions. This could take a while...
Successfully installed ffi-1.15.4
Parsing documentation for ffi-1.15.4
Done installing documentation for ffi after 1 seconds
1 gem installed

appleM1@appleM1-MacBook-Pro ~ % gem list --local | grep cocoapods | awk '{print $1}'

appleM1@appleM1-MacBook-Pro ~ % gem list

*** LOCAL GEMS ***

activesupport (6.1.4.1)
addressable (2.8.0)
algoliasearch (1.27.5)
atomos (0.1.3)
bigdecimal (default: 1.4.1)
bundler (default: 1.17.2)
CFPropertyList (2.3.6)
claide (1.0.3)
cmath (default: 1.0.0)
colored2 (3.1.2)
concurrent-ruby (1.1.9)
csv (default: 3.0.9)
date (default: 2.0.0)
dbm (default: 1.0.0)
did_you_mean (1.3.0)
e2mmap (default: 0.1.0)
escape (0.0.4)
etc (default: 1.0.1)
ethon (0.14.0)
fcntl (default: 1.0.0)
ffi (1.15.4)
fiddle (default: 1.0.0)
fileutils (default: 1.1.0)
forwardable (default: 1.2.0)
fourflusher (2.3.1)
fuzzy_match (2.0.4)
gh_inspector (1.1.3)
httpclient (2.8.3)
i18n (1.8.10)
io-console (default: 0.4.7)
ipaddr (default: 1.2.2)
irb (default: 1.0.0)
json (default: 2.1.0)
libxml-ruby (3.2.1)
logger (default: 1.3.0)
matrix (default: 0.1.0)
mini_portile2 (2.4.0)
minitest (5.11.3)
molinillo (0.8.0)
mutex_m (default: 0.1.0)
nanaimo (0.3.0)
nap (1.1.0)
net-telnet (0.2.0)
netrc (0.11.0)
nokogiri (1.10.1)
openssl (default: 2.1.2)
ostruct (default: 0.1.0)
power_assert (1.1.3)
prime (default: 0.1.0)
psych (default: 3.1.0)
public_suffix (4.0.6)
rake (12.3.2)
rdoc (default: 6.1.0)
rexml (3.2.5, default: 3.1.9)
rss (default: 0.2.7)
ruby-macho (2.5.1)
scanf (default: 1.0.0)
sdbm (default: 1.0.0)
shell (default: 0.7)
sqlite3 (1.3.13)
stringio (default: 0.0.2)
strscan (default: 1.0.0)
sync (default: 0.5.0)
test-unit (3.2.9)
thwait (default: 0.1.0)
tracer (default: 0.1.0)
typhoeus (1.4.0)
tzinfo (2.0.4)
webrick (default: 1.4.2)
xcodeproj (1.21.0)
xmlrpc (0.3.0)
zeitwerk (2.4.2)
zlib (default: 1.0.0)

appleM1@appleM1-MacBook-Pro ~ % 

appleM1@appleM1-MacBook-Pro ~ % cd Devel/flutter.apps/shop 

appleM1@appleM1-MacBook-Pro shop % flutter devices 

3 connected devices:
sdk gphone64 arm64 (mobile) • emulator-5554                        • android-arm64  • Android 12 (API 31) (emulator)
iPhone 13 (mobile)          • 470ACB9E-CA75-4069-93E4-2F8ED4605650 • ios            • com.apple.CoreSimulator.SimRuntime.iOS-15-0 (simulator)
Chrome (web)                • chrome                               • web-javascript • Google Chrome 95.0.4638.54


appleM1@appleM1-MacBook-Pro shop % flutter -d 470ACB9E-CA75-4069-93E4-2F8ED4605650 run

Launching lib/main.dart on iPhone 13 in debug mode...
Running pod install...                                             699ms
Running Xcode build...
 └─Compiling, linking and signing...                         3.7s
Xcode build done.                                           26.0s
Syncing files to device iPhone 13...                               266ms

Flutter run key commands.
r Hot reload. 🔥🔥🔥
R Hot restart.
h List all available interactive commands.
d Detach (terminate "flutter run" but leave application running).
c Clear the screen
q Quit (terminate the application on the device).

💪 Running with sound null safety 💪

An Observatory debugger and profiler on iPhone 13 is available at: http://127.0.0.1:54075/14sLzZDZbrk=/
The Flutter DevTools debugger and profiler on iPhone 13 is available at: http://127.0.0.1:9102?uri=http://127.0.0.1:54075/14sLzZDZbrk=/

Application finished.

appleM1@appleM1s-MacBook-Pro shop % 
</pre>
