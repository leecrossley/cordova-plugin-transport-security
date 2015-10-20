## App Transport Security Plugin for Apache Cordova [![npm version](https://badge.fury.io/js/cordova-plugin-transport-security.svg)](http://badge.fury.io/js/cordova-plugin-transport-security)

**Cordova / PhoneGap Plugin to allow 'Arbitrary Loads' by adding a declaration to the Info.plist file to bypass the iOS 9 App Transport Security**

## Install

#### Latest published version on npm (with Cordova CLI >= 5.0.0)

```
cordova plugin add cordova-plugin-transport-security
```

#### Latest version from GitHub

```
cordova plugin add https://github.com/leecrossley/cordova-plugin-transport-security.git
```

## Apple guidance

> App Transport Security (ATS) enforces best practices in the secure connections between an app and its back end. ATS prevents accidental disclosure, provides secure default behavior, and is easy to adopt; it is also on by default in iOS 9 and OS X v10.11. You should adopt ATS as soon as possible, regardless of whether you’re creating a new app or updating an existing one.

> If you’re developing a new app, you should use HTTPS exclusively. If you have an existing app, you should use HTTPS as much as you can right now, and create a plan for migrating the rest of your app as soon as possible. In addition, your communication through higher-level APIs needs to be encrypted using TLS version 1.2 with forward secrecy. If you try to make a connection that doesn't follow this requirement, an error is thrown. If your app needs to make a request to an insecure domain, you have to specify this domain in your app's Info.plist file.

Source: [iOS Developer Library](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14)

It's important to note that this does not impact apps built with Xcode < 7 running on iOS 9.

## Usage
In case you want specify your domain as an exception domain in ATS, open `plugin.xml`, set `NSAllowsArbitraryLoads` value (line:17) to `false` and add `NSExceptionDomains` just like this:

```
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <false/>
    <key>NSExceptionDomains</key>
    <dict>
      <key>www.github.com</key>
      <dict>
        <key>NSExceptionAllowsInsecureHTTPLoads</key>
        <true/>
        <key>NSIncludesSubdomains</key>
        <true/>
      </dict>
    </dict>
</dict>
```
For the changes to `plugin.xml` to take effect, you must refresh the `ios.json` file (inside the `/plugin` folder):
```
$ cordova platform rm ios
$ cordova platform add ios
```

Find more about App Transport Security:  
https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/



## Platforms

Applies to iOS (9+) only.

## License

[MIT License](http://ilee.mit-license.org)
