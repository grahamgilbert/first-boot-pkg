# first-boot-pkg
``first-boot-pkg`` is a tool to create a flat package that will install a series of packages when a Mac boots for the first time. This is designed for use with tools like AutoDMG, when you need to interact with the booted volume (for example, when binding to Active Directory or setting the Mac's hostname).

## Features

- Is designed with scripting and automation in mind, with options able to be configured with a configuration plist or via options on the command line (or a mixture of both)
- Will re-try failed packages (in case of Active Directory not being available, for example)
- Will wait for the network to be available before installing (optional, can be disabled if desired)

Run with ``--help`` for the full list of options.

## Examples

```bash
$ sudo ./first-boot-pkg --pkg /path/to/a/package.pkg --pkg /path/to/another.pkg
Valdating packages:
----------------------------------------------------------------
package.pkg looks good.
another.pkg looks good.
----------------------------------------------------------------
pkgbuild: Inferring bundle components from contents of /tmp/tmpCfcNTg
pkgbuild: Adding component at usr/local/first-boot/packages/package.pkg
pkgbuild: Adding component at Library/PrivilegedHelperTools/LoginLog.app
pkgbuild: Wrote package to /Users/grahamgilbert/src/Mine/first-boot-pkg/first-boot.pkg
```

Setting common defaults via a plist, and overriding the version via the command line:

```bash
 sudo ./first-boot-pkg --plist /Users/grahamgilbert/Desktop/first-boot-config.plist --version 2.3
 ```
 
##Configuration plist
 
 ```xml
 <?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN"      "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Packages</key>
    <array>
        <string>/Users/grahamgilbert/src/ClearReg/ClearReg.pkg</string>
        <string>/Users/grahamgilbert/Desktop/create_grahamgilbert-1.0.pkg</string>
    </array>
    <key>Name</key>
    <string>package-name.pkg</string>
    <key>Identifier</key>
    <string>com.grahamgilbert.test.pkg</string>
    <key>Version</key>
    <string>2.4</string>
    <key>Network</key>
    </false>
    <key>Output</key>
    <string>/Users/Shared/firstboot</string>
</dict>
</plist>
```