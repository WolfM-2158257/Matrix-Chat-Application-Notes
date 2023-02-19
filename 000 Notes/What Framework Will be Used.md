# Options
- Native Java
- Flutter
- React Native
- ~~Web App~~ (Not a mobile application, which is a requirement)

---

## Pros Native Development
- Performance
- Fast launch-time
- Easier access to device hardware
	- Camera
	- Microphone
	- Location
	- ...
- Stable
	- No need to worry if it will work in both android and IOS, because only android is targeted
	- Tend to have less bugs
- Devoid of third party integrations
- Platform's UI can be integrated

## Cons Native Development
- App will only work on android
- ~~Expenses~~ (doesn't matter, because IOS is not a requi)
- Slow debugging

---

## Pro's React native
- Faster development
	- [Hot Reloading](https://dev.to/jagroop2000/how-are-hot-reloading-and-live-reloading-in-react-native-different-3nj7)
	- Javascript, css
- Intuitive modular architecture
- Cross-platform
	- Android, IOS

## Cons React Native
- Slower performance
- Slower launch time
- Sometimes packages are not compatible
- Unable to always make full advantage of the device's hardware
- Less secure

---

## Pros Flutter
- Cross-platform:
	- Android, IOS, web, Windows and Linux
- Compiled into native
- Less UI development time
- Rich library of widgets
- Rich animations
- Material design
- Secure

## Cons Flutter
- Larger files
- Slower, but performance high enough

## Our Requirements

| Requirement (+/=/-)                    | Native Java | React Native | Flutter |
| -------------------------------------- | ----------- | ------------ | ------- |
| Fast development                       | =           | +            | =       |
| Matrix Integration                     | +           | =            | -       |
| Push notifications                     | +           | =            | =        |
| Hardware access                        | +           |               |         |
| Fast translation of messages           |             |              |         |
| Decent performance                     |             |              |         |
| Fast startup time                      |             |              |         |
| Good looking UI                        |             |              |         |
| Cross-platform mobile (extra)          |             |              |         |
| Mobile + desktop compatibility (extra) |             |              |         |

# References
1. https://www.toobler.com/blog/react-native-vs-native-app-development
2. https://aws.amazon.com/compare/the-difference-between-web-apps-native-apps-and-hybrid-apps/
3. https://www.codemotion.com/magazine/frontend/mobile-dev/native-vs-hybrid-which-mobile-app-platform-should-you-choose/
4. Flutter vs. Native performance: https://auberginesolutions.com/blog/comparing-the-performance-of-an-app-built-with-native-android-and-flutter/
5. https://surf.dev/flutter-vs-native/
6. https://inveritasoft.com/blog/flutter-vs-react-native-vs-native-deep-performance-comparison
7. Flutter push notification package: https://pub.dev/packages/push
8. RN push notifications: https://sendbird.com/developer/tutorials/implement-react-native-app-push-notifications
9. SDK's: https://matrix.org/sdks/#matrix-org-android-sdk
10. SDK Dart (flutter): 
	1. https://pub.dev/packages/matrix
11. https://docs.flutter.dev/development/ui/widgets