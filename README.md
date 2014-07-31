# iOS-Code-Snippets

List of code snippets for iOS developers.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Debugging](#debugging)
    - [Log](#log)
    - [Alert](#alert)
- [MVC](#mvc)
    - [Singleton Object](#singleton-object)
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

# MVC

### Singleton Object
```objc
+ (instancetype)sharedInstance {
   static id sharedInstance = nil;

   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
      sharedInstance = [[self alloc] init];
   });

   return sharedInstance;
}
```

# OTA Install URL Prefix
```html
itms-services://?action=download-manifest&url=<plist link>
```
