# iOS-Code-Snippets

List of code snippets for iOS developers.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Debugging](#debugging)
    - [Log](#log)
    - [Alert](#alert)
- [GCD](#gcd)
    - [Timer](#timer)
- [MVC](#mvc)
    - [Singleton Object](#singleton-object)
- [Travis Ci](#travis-ci)
    - [Encrypt Certificates](#encrypt-certificates)
- [Update Build Number](#update-build-number)
- [OTA Install URL Prefix](#ota-install-url-prefix)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Debugging
### Log
```c
#define NSLog(__FORMAT__, ...) NSLog((@"[%@] [Line %d] -> " __FORMAT__), [[NSString stringWithUTF8String:__FILE__] lastPathComponent] , __LINE__, ##__VA_ARGS__)
```

### Alert
```c
#define DebugAlert(__FORMAT__, ...)  { UIAlertView *alert = [[UIAlertView alloc] initWithTitle:[NSString stringWithFormat:@"Debug Message"] message:[NSString stringWithFormat:@"[%@] \n [Line %d] \n" __FORMAT__, [[NSString stringWithUTF8String:__FILE__] lastPathComponent], __LINE__, ##__VA_ARGS__]  delegate:nil cancelButtonTitle:@"Dismiss" otherButtonTitles:nil]; dispatch_async(dispatch_get_main_queue(), ^{ [alert show]; }); }
```

# GCD
### Timer
~~~objectivec
dispatch_time_t popTime = dispatch_time(DISPATCH_TIME_NOW, 0.01 * NSEC_PER_SEC);
dispatch_after(popTime, dispatch_get_main_queue(), ^(void){
    // Do something...
});
~~~

# MVC

### Singleton Object
```objectivec
+ (instancetype)sharedInstance {
   static id sharedInstance = nil;

   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
      sharedInstance = [[self alloc] init];
   });

   return sharedInstance;
}
```

#Travis Ci

### Encrypt Certificates
```c
openssl aes-256-cbc -k "password" -in scripts/profile/name.mobileprovision -out scripts/profile/name.mobileprovision.enc -a
openssl aes-256-cbc -k "password" -in scripts/certs/developer.cer -out scripts/certs/developer.cer.enc -a
openssl aes-256-cbc -k "password" -in scripts/certs/developer.p12 -out scripts/certs/developer.cer.p12 -a
```

#Update Build Number
```ruby
if [ "${CONFIGURATION}" = "Release" ]; then
buildNumber=$(/usr/libexec/PlistBuddy -c "Print CFBundleVersion" "$INFOPLIST_FILE")
buildNumber=$(($buildNumber + 1))
/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $buildNumber" "$INFOPLIST_FILE"
/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $buildNumber" "${TARGET_BUILD_DIR}/${INFOPLIST_PATH}"
fi
```

# OTA Install URL Prefix
```html
itms-services://?action=download-manifest&url=<plist link>
```
