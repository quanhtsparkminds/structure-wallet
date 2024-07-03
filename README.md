# structure-wallet
version SDK : stable. 3.19.0
Java 18.0.2.1

# Run it for flavor

flutter pub run flutter_flavorizr -p assets:download,assets:extract,android:androidManifest,android:buildGradle,ios:xcconfig,ios:buildTargets,ios:schema,ios:plist,google:firebase,assets:clean,ide:config

# Run it for icons

gen assets: flutter packages pub run build_runner build
flutter pub run flutter_launcher_icons -f flutter_launcher_icons-dev.yaml
flutter pub run flutter_launcher_icons -f flutter_launcher_icons-stg.yaml
flutter pub run flutter_launcher_icons -f flutter_launcher_icons-prod.yaml

gen freezed: fvm flutter pub run build_runner build --delete-conflicting-outputs

run init flutterfire: fvm dart pub global run flutterfire_cli:flutterfire configure

gen assets: flutter packages pub run build_runner build --delete-conflicting-outputs

# Run release for android

flutter build appbundle --flavor prod -t lib/main_prod.dart
flutter build apk --flavor prod -t lib/main_prod.dart

run with software rendering: fvm flutter run --enable-software-rendering
Deprecated Gradle features were used in this build, making it incompatible with Gradle 8.0.

<https://developer.android.com/studio/publish/app-signing#sign-apk>
<https://docs.flutter.dev/deployment/android>

## Boilerplate Features:

* Onboarding (intro, name, image wallet)
* Wallet (home, chart, info)
* Routing
* Theme
* Dio
* Database
* MobX (to connect the reactive data of your application with the UI)
* Bloc cubit (State Management)
* Encryption
* Validation
* Code Generation
* User Notifications
* Dependency Injection
* Dark Theme Support 
* Multil language
* Flavor (dev, stg, prod)
* Common widgets (button, input text, droplist, chart(new), item) 

### Libraries & Tools Used

* [Dio](https://github.com/flutterchina/dio)
* [MobX](https://github.com/mobxjs/mobx.dart) (to connect the reactive data of your application with the UI)
* [Flutter_Bloc](https://pub.dev/packages/flutter_bloc) (State Management)
* [Encryption](https://github.com/xxtea/xxtea-dart)
* [Validation](https://github.com/dart-league/validators)
* [Notifications](https://github.com/AndreHaueisen/flushbar)
* [Json Serialization](https://github.com/dart-lang/json_serializable)
* [Dependency Injection](https://github.com/fluttercommunity/get_it)

### Folder Structure
Here is the core folder structure which flutter provides.

```
flutter-app/
|- android
|- build
|- ios
|- lib
|- test
```

### Struture

    .
    ├── /assets
    │   ├── /app_icon                                                # app-icon (png)
    │   │   └── ...
    │   ├── /fonts                                                   # font-family in app
    │   │   └── ...
    │   ├── /icons
    │   │   ├── ...
    │   │   ├── ...
    │   │   └── ...
    │   ├── /images
    │   │   ├── ...
    │   └── /svg
    │       └── ...
    └── /lib
    │   ├── /commands
    │   │   └── /core
    |   |      └── ...
    |   |   └── /api_client
    |   |      └── /interceptor
    │   │         └── auth_interceptor.dart
    │   │         └── dio_cache_interceptor.dart
    |   |      └── api_client.dart
    |   |      └── api_config.dart
    |   |      └── api_result.dart
    |   |      └── dio_client.dart
    |   |      └── dio_exception.dart
    │   │   └── navigate
    │   │   └── ...
    │   ├── /config
    │   │   └── main_app_service.dart
    │   │   └── app_initlize.dart
    │   │   └── sprefs.dart
    │   │   └── ...
    │   ├── /constants
    │   │   └── app_color.dart
    │   │   └── app_key.dart
    │   │   └── size.dart
    │   │   └── ...
    │   ├── /domain
    │   │   └── local_storage.dart
    │   │   └── model.dart
    |   |      └── /authe_model
    |   |      └── /profile_model
    │   │   └── respositories.dart
    |   |      └── auth_respository.dart
    |   |      └── ...
    │   ├── /event
    │   │   └── ...
    │   ├── /feature
    │   │   └── /launch
    |   |      └── /bloc-cubit
    |   |      └── /view
    |   |      └── /widgets
    |   |      └── launch_screen_view.dart
    │   │   └── /home
    |   |      └── /bloc-cubit
    |   |         └── home_cubit.dart
    |   |         └── home_state.dart
    |   |      └── /view
    |   |      └── /widgets
    |   |      └── home_screen_view.dart
    │   ├── /gen
    │   │   └── assets.gen.dart
    │   ├── /main_model
    │   │   └── main_app_state.dart                              # Load app and main state all in app
    │   │   └── network_connection.dart                          # Load app and main state all in app
    │   ├── /routing
    │   │   └── /page_configuration
    |   |      └── auth_page_configuration.dart
    |   |      └── launch_page_configuration.dart
    |   |      └── home_page_configuration.dart
    │   │   └── app_route_parser.dart
    │   │   └── app_router.dart
    │   │   └── page_configuration.dart
    │   ├── /shared
    │   │   └── /helps
    |   |      └── regex.dart
    |   |      └── spref.dart
    |   |      └── storage_secure.dart
    |   |      └── translations.dart
    │   │   └── /languages
    |   |      └── en.dart
    |   |      └── translation_key.dart
    |   |      └── vi.dart
    │   │   └── /mixins

    |   |      └── validator_mixin.dart
    │   │   └── /utils
    |   |      └── /universal_file
    |   |         └── ...
    |   |      └── /validator
    |   |         └── ...
    |   |      └── format.dart
    |   |      └── screen_size.dart
    |   |      └── time_utils.dart
    │   │   └── /widgets
    |   |      └── /app_text
    |   |      └── /app_dropdown
    |   |      └── ...
    |   └── app_initialized
    |   └── theme.dart
    |   └── flavor.dart
    |   └── main.dart
    |   └── main_dev.dart
    |   └── main_stg.dart
    |   └── main_prod.dart

```
1- constants - All the application level constants are defined in this directory with-in their respective files. This directory contains the constants for `theme`, `dimentions`, `api endpoints`, `preferences` and `strings`.
2- data - Contains the data layer of your project, includes directories for local, network and shared pref/cache.
3- stores - Contains store(s) for state-management of your application, to connect the reactive data of your application with the UI. 
4- feature — Contains all the ui, bloc, state, event of your project, contains sub directory for each screen.
5- util — Contains the utilities/common functions of your application.
6- widgets — Contains the common widgets for your applications. For example, Button, TextField etc.
7- routes.dart — This file contains all the routes for your application.
8- main.dart - This is the starting point of the application. All the application level configurations are defined in this file i.e, theme, routes, title, orientation.
```


### Routes

This file contains all the routes for your application.

```dart
import 'package:flutter/material.dart';

import 'ui/post/post_list.dart';
import 'ui/login/login.dart';
import 'ui/splash/splash.dart';

const String loginPagePath = '/login-page';
const String dashBoardPath = '/dashboard';

enum Pages {
  loginPage,
  dashBoard,
}

abstract class PageConfiguration {
  final String key;
  final String path;
  final Pages uiPage;
  var history = <PageConfiguration>[];
  get location => path;

  PageConfiguration({
    required this.key,
    required this.path,
    required this.uiPage,
  });

  factory PageConfiguration.fromLocation(String location) {
    location = Uri.decodeFull(location);
    final parsedUri = Uri.parse(location);
    final pathSegments = parsedUri.pathSegments;
    if (pathSegments.isEmpty) {
      return LoginPageConfiguration.fromLocation(location);
    }

    final path = pathSegments[0];

    print('path:$path');
    print(pathSegments);

    switch (path) {
      case loginPagePath:
        return LoginPageConfiguration.fromLocation(location);
      default:
        return DashBoardPageConfiguration.fromLocation(location);
    }
  }

  List<PageConfiguration> get pageTree => history;
}
```
### Main
This is the starting point of the application. All the application level configurations are defined in this file i.e, theme, routes, title, orientation etc.

```dart
Future<void> runMain() async {
  WidgetsFlutterBinding.ensureInitialized();

  await appInitialized();

  Application application = Application();
  await application.setup();

  /// Create core models & services
  MainAppState mainAppState =
      MainAppState(userRepository: application.userRepository);
  MainLoginState mainLoginState = MainLoginState();

  NetworkState networkState = NetworkState();
  await SentryFlutter.init(
    (options) {
      options.dsn = 'https://example@sentry.io/add-your-dsn-here';
    },
    appRunner: () => runApp(
      MultiProvider(
        providers: [
          Provider.value(value: application.userRepository),
          BlocProvider<LoginCubit>.value(
            value: LoginCubit(),
          ),
          ChangeNotifierProvider.value(value: mainAppState),
          ChangeNotifierProvider.value(value: mainLoginState),
          ChangeNotifierProvider.value(value: networkState)
        ],
        child: _AppBootstrapper(),
      ),
    ),
  );
}

final navigatorKey = GlobalKey<NavigatorState>();

class _AppBootstrapper extends StatefulWidget {
  @override
  _AppBootstrapperState createState() => _AppBootstrapperState();
}

class _AppBootstrapperState extends State<_AppBootstrapper> {
  AppRouteParser routeParser = AppRouteParser();
  late AppRouterDelegate router;

  @override
  void initState() {
    router = AppRouterDelegate(context.read<MainAppState>());
    SystemChrome.setPreferredOrientations([
      DeviceOrientation.portraitUp,
    ]);
    scheduleMicrotask(() {
      BootstrapCommand().run(context);
    });
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      routeInformationParser: routeParser,
      routerDelegate: router,
      debugShowCheckedModeBanner: false,
      theme: AppTheme.dark(),
      darkTheme: AppTheme.dark(),
      themeMode: ThemeMode.dark,
      supportedLocales: const [
        Locale('en', 'US'),
      ],
      localizationsDelegates: [
        AppLocalizations.delegate,
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
    );
  }
}

```
