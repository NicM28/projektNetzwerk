```
--- lxc-debian	2022-05-23 22:36:10.000000000 +0000
+++ lxc-debian+	2024-05-03 12:49:26.560681616 +0000
@@ -204,6 +204,8 @@
 
     # set initial timezone as on host
     if [ -f /etc/timezone ]; then
+        localtime=$(readlink /etc/localtime)
+        chroot "${rootfs}" ln -sf ${localtime} /etc/localtime
         cat /etc/timezone > "$rootfs/etc/timezone"
         rm -f "$rootfs/etc/localtime"
         chroot "$rootfs" dpkg-reconfigure -f noninteractive tzdata
@@ -444,9 +446,24 @@
                 "wheezy")
                     gpgkeyname="archive-key-7.0"
                     ;;
-                *)
+                "jessie")
                     gpgkeyname="archive-key-8"
                     ;;
+                "stretch")
+                    gpgkeyname="archive-key-9"
+                    ;;
+                "buster"|"oldoldstable")
+                    gpgkeyname="archive-key-10"
+                    ;;
+                "bullseye"|"oldstable")
+                    gpgkeyname="archive-key-11"
+                    ;;
+                "bookworm"|"stable")
+                    gpgkeyname="archive-key-11"
+                    ;;
+                *)
+                    gpgkeyname="archive-key-12"
+                    ;;
             esac
             wget https://ftp-master.debian.org/keys/${gpgkeyname}.asc -O - --quiet \
                 | gpg --import --no-default-keyring --keyring="${lreleasekeyring}"
@@ -675,7 +692,7 @@
     if [[ -f "${rootfs}/root/.profile" ]]; then
        sed -i -e 's/^mesg n/test -t 0 \&\& mesg n/g' ${rootfs}/root/.profile
     fi
-    
+
     # end
 }
```