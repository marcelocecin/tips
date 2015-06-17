convert .p12 (mac) to .p12 (win)
(mac) download & install developer.cer
(mac) export mac.p12 @ keychain 
(win) download & install developer.cer
(win) openssl x509 -in developer.cer -inform DER -out developer.pem -outform PEM
(win) openssl pkcs12 -nocerts -in mac.p12 -out mac.pem
(win) notepad mac.pem then save only private key as mac.key
(win) openssl pkcs12 -export -inkey mac.key -in developer.pem -out win.p12

install the alchemy toolkit for cygwin on windows 7
1) download cygwin install it with the following packages: perl, zip (archive) and gcc/g++ (dev)
2) you must have java installed
3) download alchemy @ adobe labs
4) download flex 3.2 sdk @ adobe opensource
5) unzip alchemy to c:\cygwin\home\<USER>\alchemy\ and unzip flex sdk to c:\cygwin\home\<USER>\flex\
6) copy c:\program files (x86)\java\jdk\bin\java.exe and javac.exe to c:\cygwin\bin
7) open c:\cygwin\home\<USER>.bashrc and write: export FLEX_HOME=/home/<USER>/flex/bin
8) open cygwin.exe and type: a) cd alchemy b) ./config c) exit
9) open c:\cygwin\home\<USER>\alchemy\alchemy-setup and write: export ADL=/home/<USER>/flex/adl.exe
10) open c:\cygwin\home\<USER>.bashrc and write: a) export ALCHEMY_HOME=/home/<USER>/alchemy b) source /home/<USER>/alchemy/alchemy-setup c) PATH=$ALCHEMY_HOME/achacks:/home/<USER>/flex/bin:$PATH d) export PATH 
11) open c:\cygwin\home\<USER>\alchemy\achacks\hacks.pl and change the line “if(`uname` =~ /CYGWIN/)” to “if(`/bin/uname` =~ /CYGWIN/)”
12) open cygwin.exe and type a) cd alchemy b) ln -s llvm-stub llvm-stub.exe c) alc-on; which gcc d) gcc stringecho.c -O3 -Wall -swc -o stringecho.swc
13) check if c:\cygwin\home\<USER>\alchemy\samples\stringecho\stringecho.swc was created
* win7-64bits * cygwin-1.7.9-1 * java-jdk1.6.0_23 * alchemy_p1_121008 * flex sdk 3.2.0.3958 * 
