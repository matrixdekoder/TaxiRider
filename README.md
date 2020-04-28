# Taxi

Passo-a-passo para desenvolver um app tipo *Uber* no *Flutter*. Este app será para os passageiros.

## Estrutura do Projeto

O nosso projeto *Flutter* irá possuir esta estrutura:
```
taxi_rider
 |-android
 | |-app
 | | |-src
 | | | |-debug
 | | | |  |-AndroidManifest.xml 
 | | | |-main
 | | | |  |-java
 | | | |  |  |- io.flutter.plugins
 | | | |  |       |-GeneratedPluginRegistrant.java 
 | | | |  |-kotlin
 | | | |  |  |-com.example.taxidriver
 | | | |  |     |-MainActivity.kt
 | | | |  |-res
 | | | |  |  |-drawable
 | | | |  |  |   |-launch_background.xml
 | | | |  |  |-mipmap-hdpi
 | | | |  |  |  |-ic_launcher.png
 | | | |  |  |-mipmap-mdpi
 | | | |  |  |  |-ic_launcher.png
 | | | |  |  |-mipmap-xhdpi
 | | | |  |  |  |-ic_launcher.png
 | | | |  |  |-mipmap-xxhdpi
 | | | |  |  |  |-ic_launcher.png
 | | | |  |  |-mipmap-xxxhdpi
 | | | |  |  |  |-ic_launcher.png
 | | | |  |  |-values
 | | | |  |  |  |-styles.xml
 | | | |  |  |-AndroidManifest.xml
 | | | |-profile
 | | | |  |-AndroidManifest.xml
 | | |-build.gradle
 | |-gradle
 | |  |-wrapper
 | |  |  |-gradle-wrapper.jar
 | |  |  |-gradle-wrapper.properties
 | |-.gitignore
 | |-build.gradle
 | |-gradle.properties
 | |-gradlew
 | |-gradlew.bat
 | |-local.properties
 | |-settings.gradle
 | |-taxidriver_android.iml
 |-ios
 | |-Flutter
 | |  |-AppFrameworkInfo.plist
 | |  |-Debug.xcconfig
 | |  |-flutter_export_environment.sh
 | |  |-Generated.xcconfig
 | |  |-Release.xcconfig
 | |-Runner
 | |  |-Assets.xcassets
 | |  |  |-AppIcon.appiconset
 | |  |  |   |-Contents.json
 | |  |  |   |-Icon-App-20x20@1x.png
 | |  |  |   |-Icon-App-20x20@2x.png
 | |  |  |   |-Icon-App-20x20@3x.png
 | |  |  |   |-Icon-App-29x29@1x.png
 | |  |  |   |-Icon-App-29x29@2x.png
 | |  |  |   |-Icon-App-29x29@3x.png
 | |  |  |   |-Icon-App-40x40@1x.png
 | |  |  |   |-Icon-App-40x40@2x.png
 | |  |  |   |-Icon-App-40x40@3x.png
 | |  |  |   |-Icon-App-60x60@2x.png
 | |  |  |   |-Icon-App-60x60@3x.png
 | |  |  |   |-Icon-App-76x76@1x.png
 | |  |  |   |-Icon-App-76x76@2x.png
 | |  |  |   |-Icon-App-83.5x83.5@2x.png
 | |  |  |   |-Icon-App-1024x1024@1x.png
 | |  |  |-LaunchImage.imageset
 | |  |  |  |-Contents.json
 | |  |  |  |-LaunchImage.png
 | |  |  |  |-LaunchImage@2x.png
 | |  |  |  |-LaunchImage@3x.png
 | |  |  |  |-README.md
 | |  |-Base.Iproj
 | |  |  |-LaunchScreen.storyboard
 | |  |  |-Main.storyboard
 | |  |-AppDelegate.swift
 | |  |-GeneratedPluginRegistrant.h
 | |  |-GeneratedPluginRegistrant.m
 | |  |-Info.plist
 | |  |-Runner-Bridging-Header.h
 | |-Runner.xcodeproj
 | |  |-project.xcworkspace
 | |  |   |-contents.xcworkspacedata
 | |  |-xcshareddata
 | |  |  |-xcschemes
 | |  |  |  |-Runner.xcscheme
 | |  |  |-project.pbxproj
 | |  |-project.pbxproj
 | |-Runner.xcworkspace
 | |  |-contents.xcworkspacedata
 | |-.gitignore
 |-lib
 | |-main.dart
 |-test
 | |-widget_test.dart
 |-.gitignore
 |-.metadata
 |-.packages
 |-pubspec.lock
 |-pubspec.yaml
 |-README.md
 |-taxidriver.iml
```
## Dependências 

Primeiramente, vamos em `pubspec.yaml` e chamaremos o `google_maps_flutter`
```
dependencies:
  flutter:
    sdk: flutter
  google_maps_flutter: ^0.5.7 # Adicione esta linha
  
  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^0.1.2
```
Feito isso podemos clicar em `Pub get` para instalar os novos pacotes referênciados.

## API 

Vamos em [Google Cloud Platform](href="https://cloud.google.com/console/google/maps-apis/overview"), se necessario crie um novo projeto, ou use um já existente.

Na opção do menu vamos em credencias, se tudo estive correto vamos usar uma api gerada para ser usada neste [tutorial do flutter](https://codelabs.developers.google.com/codelabs/google-maps-in-flutter/#0). No meu caso vou usar a API já configurada.

Com a API em mãos vamos em `taxi_driver/ android/ app/ src / main / AndroidManifest.xml` e adicionaremos a linha
```
<meta-data android:name="com.google.android.geo.API_KEY" android:value="O VALOR DA SUA API"/>
```
E em `taxi_driver/ios/Runner/AppDelegate.swift` adicionaremos a seguinte linha
```
GMSServices.provideAPIKey("O VALOR DA SUA API AQUI")
```
**NOTA:** Não vou testar este aplicativo na plataforma IOS, entretanto, adicionando esta linha ao `AppDelegate.swift` já é meio caminho andado:)

## Firebase

Neste app vamos usar o Banco de dados **NoSQL Firebase**, portanto vamos em [Cloud Firestore](https://firebase.google.com/products/firestore/) e clicaremos em "Ir para o console". Usaremo o plano gratis, mas fique claro que no plano pago poderiamos fazer autenticação do usario usando **sms**. Então baixaremos o documento `google-services.json`. Colocar o documento baixado em `android/app/`.

Em `pubspec.yaml` adicionaremos as dependencias `cloud firestore`, `google_sign_in`, `firebase_databas`, `http`, `google_maps_webservice`, `location`e `firebase_auth`
```
dependencies:
  flutter:
    sdk: flutter
  cloud_firestore: ^0.13.0+1
  google_sign_in: ^4.4.4
  firebase_auth: ^0.11.1+12 # Nesta versão não dá erro
  #firebase_auth: ^0.16.0 Nesta versão dá um erro
  firebase_database: ^3.0.5
  http: ^0.12.0+2
  google_maps_webservice: ^0.0.14
  location: ^2.3.5
```
Em `android/app/build.gradle`, procuraremos por `minSdkVersion 16` e mudaremos está linha para `minSdkVersion 21`.

Ainda em `android/app/build.gradle`, adicionaremos a linha
```
apply plugin: 'com.google.gms.google-services'
```
E em `android/build.gradle` dentro da `buildscript`tag, adicionaremos uma nova dependencia
```
buildscript {
   repositories {
       // ...
   }

   dependencies {
       // ...
       classpath 'com.google.gms:google-services:4.3.3'   // new
   }
}
```

## Erro com o `firebase_auth: ^0.16.0`

Apos atualizar esta dependencia, o metodo signIn retorna `AuthResult` em vez de `FirebaseUser`
```
FirebaseAuth.instance
               .createUserWithEmailAndPassword(
                  email: email_entry.text,
                  password: password_entry.text)
               .then((authResult) => Firestore.instance
                  .collection("users")
                  .document(authResult.user.uid) //returns auth result so you should get user.uid from auth result
                  .setData({
                    "uid": authResult.user.uid,
                    "fname": first_entry.text,
                    "surname": last_entry.text,
                    "email": email_entry.text,
           })
           .then((result) =>  {
               Navigator.pushAndRemoveUntil(
               context,
               MaterialPageRoute(
                   builder: (context) => MyHomePage(
                     title:
                     first_entry
                         .text +
                         "'s Tasks",
                     uid: authResult.user.uid,
                   )),
                   (_) => false),
               first_entry.clear(),
               last_entry.clear(),
               email_entry.clear(),
               password_entry.clear(),
               }));
```
É preciso adaptar a versão mais recente para o que já foi feito, se quiser, pois vai que não é importante.

## Assets 

Em `taxi_driver` eu havia feito diferente no documento `pubspec.yaml` referenciando cada imagem o que não seria nada inteligente caso tivessemos um montão de imagens, então aqui iremos fazer certo e colocar no `pubspec.yaml` somente
```
assets:
    - assets/img/
```
## Modificando a Estrutura

Depois de tudo configurado dentro de `taxi_driver/lib/` vamos criar as seguintes pasta com os seguintes documentos
```
taxi_driver
 |-android
 |-ios
 |-lib
 |  |-src
 |  |  |-blocs
 |  |  |  |-auth_bloc.dart
 |  |  |  |-place_bloc.dart
 |  |  |-config
 |  |  |  |-configs.dart
 |  |  |-fire_base
 |  |  |  |-fire_base_auth.dart
 |  |  |-model
 |  |  |  |-place_item_res.dart
 |  |  |  |-step_res.dart
 |  |  |-repository
 |  |  |  |-place_service.dart
 |  |  |-ui
 |  |  |  |-pages
 |  |  |  |  |-add_card.dart
 |  |  |  |  |-add_payment_method.dart
 |  |  |  |  |-free_rides.dart
 |  |  |  |  |-help.dart
 |  |  |  |  |-home.dart
 |  |  |  |  |-instant_pay.dart
 |  |  |  |  |-login.dart
 |  |  |  |  |-payment.dart
 |  |  |  |  |-register.dart
 |  |  |  |  |-ride_picker_page.dart
 |  |  |  |  |-select_issue.dart
 |  |  |  |  |-settings.dart
 |  |  |  |  |-your_trips.dart
 |  |  |  |-widgets
 |  |  |  |  |-exhibition_bottom_sheet.dart
 |  |  |  |  |-functionalButton.dart
 |  |  |  |  |-home_menu_drawer.dart
 |  |  |  |  |-loading_dialog.dart
 |  |  |  |  |-msg_dialog.dart
 |  |  |  |  |-ride_picker.dart
 |  |  |-util
 |  |  |  |-map_util.dart
 |  |-main.dart
 ...

```

Pois bem, começaremos a codificar pelos pacotes internos que são:

- auth_bloc;
- place_bloc;
- configs;
- fire_base;
- place_item_res;
- step_res;
- place_service;
- exhibition_bottom_sheet;
- functionalButton;
- home_menu_drawer;
- loading_dialog;
- msg_dialog;
- ride_picker;
- map_util.

Para então codificarmos as paginas.

## Firebase

`fire_base_auth.dart`
```
import 'package:firebase_auth/firebase_auth.dart';
import 'package:firebase_database/firebase_database.dart';

class FireAuth {
  FirebaseAuth _firebaseAuth = FirebaseAuth.instance;

  void signUp(String email, String pass, String name, String phone, Function onSuccess, Function(String) onRegisterError) {
    _firebaseAuth.createUserWithEmailAndPassword(email: email, password: pass).then((user) {
      _createUser(user.uid, name, phone, onSuccess, onRegisterError);
      print(user);
    }).catchError((err) {
      _onSignupError(err.code, onRegisterError);
    });
  }

  _createUser(String userId, String name, String phone, Function onSuccess, Function(String) onRegisterError) {
    var user = {
      "name": name,
      "phone": phone,
    };

    var ref = FirebaseDatabase.instance.reference().child("users");

    ref.child(userId).set(user).then((user) {
      // success
      onSuccess();
    }).catchError((err) {
      // TODO
      onRegisterError("Signup Fail, please try again");
    });
  }

  void signIn(String email, String pass, Function onSuccess, Function(String) onSignInError) {
    _firebaseAuth.signInWithEmailAndPassword(email: email, password: pass).then((user) {
      print("on SignIn in success");
      onSuccess();
    }).catchError((err) {
      onSignInError("SignIn fail, please try again");
    });
  }

  void _onSignupError(String code, Function(String) onRegisterError) {
    switch (code) {
      case "ERROR_INVALID_EMAIL":
      case "ERROR_INVALID_CREDENTIAL":
        onRegisterError("Invalid Email");
        break;
      case "ERROR_EMAIL_ALREADY_IN_USE":
        onRegisterError("Email has existed");
        break;
      case "ERROR_WEAK_PASSWORD":
        onRegisterError("The password is not strong enough");
        break;
      default:
        onRegisterError("Signup fail, please try again");
        break;
    }
  }
}
```
Usando o codigo acima o banco de dados é gerado a partir da autenticação do usuario, bem diferente do que modelar o banco para depois codificar as classes modelos, para só então poder ser feito o registro, exclusão, alteração e visualização no banco de dados.


## Model

`place_item_res.dart`
```
class PlaceItemRes {
  String name;
  String address;
  double lat;
  double lng;
  PlaceItemRes(this.name, this.address, this.lat, this.lng);

  static List<PlaceItemRes> fromJson(Map<String, dynamic> json) {
    print("parsing data");
    List<PlaceItemRes> rs = List();

    var results = json['results'] as List;
    for (var item in results) {
      var p = PlaceItemRes(item['name'], item['formatted_address'], item['geometry']['location']['lat'], item['geometry']['location']['lng']);

      rs.add(p);
    }

    return rs;
  }
}
```
O algoritmo acima permite carregar os lugares em uma lista.

`step_res.dart`
```
import 'package:google_maps_flutter/google_maps_flutter.dart';

class StepRes {
  LatLng startLocation;
  LatLng endLocation;
  StepRes({this.startLocation, this.endLocation});

  factory StepRes.fromJson(Map<String, dynamic> json) {
    return StepRes(
      startLocation: LatLng(
        json["start_location"]["lat"], json["start_location"]["lng"]
      ),
      endLocation:
        LatLng(json["end_location"]["lat"], json["end_location"]["lng"])
    );
  }
}
```
'-'

## Repository

`place_service.dart`
```
import 'dart:async';
import 'package:taxidriver/src/model/place_item_res.dart';
import 'package:taxidriver/src/model/step_res.dart';
import 'package:taxidriver/src/config/configs.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

String dsfsdfadf =
    "https://maps.googleapis.com/maps/api/directions/json?origin=Toronto&destination=Montreal&sensor=false&mode=driving&key=SUA API AQUI";

class PlaceService {
  static Future<List<PlaceItemRes>> searchPlace(String keyWord) async {
    String url =
        "https://maps.googleapis.com/maps/api/place/textsearch/json?key=SUA API AQUI=" +
            Uri.encodeQueryComponent(keyWord);

    print("search >>: " + url);
    var res = await http.get(url);
    if (res.statusCode == 200) {
      print(res.body);
      return PlaceItemRes.fromJson(json.decode(res.body));
    } else {
      return List();
    }
  }

  static Future<dynamic> getStep(
      double lat, double lng, double tolat, double tolng) async {
    String str_origin = "origin=" + lat.toString() + "," + lng.toString();

    // destination of route
    String str_dest =
        "destinationo=" + tolat.toString() + "," + tolng.toString();

    // sensor enabled
    String sensor = "sensor=false";
    String mode = "mode=driving";

    // building the parameters to the web service
    String parameters = str_origin + "&" + str_dest + "&" + sensor + "&" + mode;

    // output format
    String output = "json";

    // building the url to the webservice
    String url = "https://maps.googleapis.com/maps/api/directions/" +
    output +
    "?origin=" +
    parameters +
    "&key=SUA API AQUI";
    final JsonDecoder _decoder = JsonDecoder();
    return http.get(url).then((http.Response response) {
      String res = response.body;
      int statusCode = response.statusCode;
      if (statusCode < 200 || statusCode > 400 || json == null) {
        res = "{\"status\":" +
      statusCode.toString() +
      ",\"message\":\"error\",\"response\":" +
      res +
      "}";
        throw Exception(res);
      }

      List<StepRes> steps;
      try {
        steps =
            _parseSteps(_decoder.convert(res)["routes"][0]["legs"][0]["steps"]);
      } catch (e) {
        throw new Exception(res);
      }
    });
  }

  static List<StepRes> _parseSteps(final responseBody) {
    var list =
        responseBody.map<StepRes>((json) => StepRes.fromJson(json)).toList();

    return list;
  }
}

```
Este algoritmo usa os dois algoritmos anteriores para carregar os lugares.

## Blocs

Neste repositorio vamos colocar os seguintes codigos

`auth_bloc.dart`
```
import 'dart:async';

import 'package:taxidriver/src/fire_base/fire_base_auth.dart';

class AuthBloc {
  var _fireAuth = FireAuth();
  StreamController _nameController = StreamController();
  StreamController _emailController = StreamController();
  StreamController _passController = StreamController();
  StreamController _phoneController = StreamController();

  Stream get nameStream => _nameController.stream;
  Stream get emailStream => _emailController.stream;
  Stream get passStream => _passController.stream;
  Stream get phoneStream => _phoneController.stream;

  bool isValid(String name, String email, String pass, String phone) {
    if (name == null || name.length == 0) {
      _nameController.sink.addError("Insert your name");
      return false;
    }
    _nameController.sink.add("");

    if (phone == null || phone.length == 0) {
      _phoneController.sink.addError("Insert your phone");
      return false;
    }
    _phoneController.sink.add("");

    if (email == null || email.length == 0) {
      _emailController.sink.addError("Insert your email");
      return false;
    }
    _emailController.sink.add("");

    if (pass == null || pass.length == 0) {
      _passController.sink.addError("Your password must contain more than 6 characters");
      return false;
    }
    _passController.sink.add("");
    return true;
  }

  void signUp(String email, String pass, String phone, String name, Function onSuccess, Function(String) onRegisterError) {
    _fireAuth.signUp(email, pass, name, phone, onSuccess, onRegisterError);
  }

  void signIn(String email, String pass, Function onSuccess, Function(String) onSignInError) {
    _fireAuth.signIn(email, pass, onSuccess, onSignInError);
  }

  void dispose() {
    _nameController.close();
    _emailController.close();
    _passController.close();
    _phoneController.close();
  }
}
```
Este algoritmo usa o algoritmo de banco de dados para poder cadastrar, autenticar, permitir o **sign in** e **sign up** do usuario.

`place_bloc.dart`
```
import 'dart:async';

import 'package:taxidriver/src/repository/place_service.dart';

class PlaceBloc {
  var _placeController = StreamController.broadcast();
  Stream get placeStream => _placeController.stream;

  void searchPlace(String keyword) {
    _placeController.sink.add("start");
    PlaceService.searchPlace(keyword).then((rs) {
      _placeController.sink.add(rs);
    }).catchError(() {
      // sink stop
    });
  }

  void dispose() {
    _placeController.close();
  }
}
```
Usa o algoritmo `place_service.dart` para coloca-lo dentro da arquitera.

## Util

`map_util.dart`
```
import 'dart:async';
import 'package:google_maps_flutter/google_maps_flutter.dart';
import 'package:google_maps_webservice/geolocation.dart' as APIGeolocatio;
import 'package:google_maps_webservice/directions.dart' as APIDirections;

class MapUtil {
  final directions = APIDirections.GoogleMapsDirections(apiKey: 'SUA API AQUI');
  final geolocation = APIGeolocatio.GoogleMapsGeolocation(apiKey: 'SUA API AQUI');

  Future<LatLng> getCurrentLocation() async {
    LatLng currentLocation;
    APIGeolocatio.GeolocationResponse resLocation = await geolocation.getGeolocation();
    if (resLocation.isOkay) {
      currentLocation = new LatLng(resLocation.location.lat, resLocation.location.lng);
    } else {
      print(resLocation.errorMessage);
    }
    return currentLocation;
  }

  Future<List<LatLng>> getRoutePath(LatLng origin, LatLng destin) async{
    List<LatLng> locationsSteps = [];
    APIDirections.DirectionsResponse resDirections = await directions.directionsWithLocation(
      new APIDirections.Location(origin.latitude, origin.latitude),
      new APIDirections.Location(origin.longitude, origin.longitude),
      travelMode: APIDirections.TravelMode.driving
      );
    if (resDirections.isOkay) {
      for (var r in resDirections.routes) {
        for (var l in r.legs) {
          for (var s in l.steps) {
            locationsSteps.addAll(decodePoly(s.polyline.points));
          }
        }
      }
  } else {
      print(resDirections.errorMessage);
  }
    return locationsSteps;
  }

  List<LatLng> decodePoly(String encoded) {
    List<LatLng> poly = new List<LatLng>();
    int index = 0, len = encoded.length;
    num lat = 0, lng = 0;

    while (index < len) {
      int b, shift = 0, result = 0;
      do {
        b = encoded.codeUnitAt(index++) - 63;
        result |= (b & 0x1f) << shift;
        shift += 5;
      } while (b >= 0x20);
      int dlat = ((result & 1) != 0 ? ~(result >> 1) : (result >> 1));
      lat += dlat;

      shift = 0;
      result = 0;
      do {
        b = encoded.codeUnitAt(index++) - 63;
        result |= (b & 0x1f) << shift;
        shift += 5;
      } while (b >= 0x20);
      int dlng = ((result & 1) != 0 ? ~(result >> 1) : (result >> 1));
      lng += dlng;

      LatLng p = new LatLng(((lat / 1E5)),
          ((lng / 1E5)));
      poly.add(p);
    }
    return poly;
  }
}

class CompositeSubscription {
  Set<StreamSubscription> _subscriptions = new Set();

  void cancel() {
    for (var n in this._subscriptions) {
      n.cancel();
    }
    this._subscriptions = new Set();
  }

  void add(StreamSubscription subscription) {
    this._subscriptions.add(subscription);
  }

  void addAll(Iterable<StreamSubscription> subs) {
    _subscriptions.addAll(subs);
  }

  bool remove(StreamSubscription subscription){
    return this._subscriptions.remove(subscription);
  }

  bool contains(StreamSubscription subscription) {
    return this._subscriptions.contains(subscription);
  }

  List<StreamSubscription> toList() {
    return this._subscriptions.toList();
  }
}
```
Pelo o que eu entendi desse algoritmo, o principal objetivo dele é trabalhar com informações em tempo real do usuario (GPS) e tambem para poder desenhar o traçado.

## Interface Do Usuario

A interface está divida em dois pacotes: `widgets` e `pages`

### Widgets

`exhibition_bottom_sheet.dart`
```
import 'dart:ui';
import 'dart:math' as math;
import 'package:flutter/material.dart';
import 'package:taxidriver/main.dart';
import 'package:taxidriver/src/ui/pages/home.dart';
import 'package:taxidriver/src/ui/pages/register.dart';
import 'package:taxidriver/src/ui/widgets/loading_dialog.dart';
import 'package:taxidriver/src/ui/widgets/msg_dialog.dart';

const double minHeight = 220;

class ExhibitionBottomSheet extends StatefulWidget {
  @override
  _ExhibitionBottomSheetState createState() => _ExhibitionBottomSheetState();
}

TextEditingController emailTextController;
TextEditingController passwordTextController;
String passText;
String emailText;
FocusNode focusNode;
FocusNode focusNodePassword;

class _ExhibitionBottomSheetState extends State<ExhibitionBottomSheet>
    with SingleTickerProviderStateMixin {
  AnimationController _controller;

  double get headerTopMargin =>
      lerp(20, 20 + MediaQuery.of(context).padding.top);

  double get headerFontSize => lerp(24, 34);
  double get maxHeight => MediaQuery.of(context).size.height;
  double get itemBorderRadius => lerp(8, 24);
  double get iconLeftBorderRadius => itemBorderRadius;
  double get iconRightBorderRadius => lerp(8, 0);

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
        vsync: this, duration: Duration(milliseconds: 3600));
    focusNode = FocusNode();
    focusNodePassword = FocusNode();
  }

  double lerp(double min, double max) =>
      lerpDouble(min, max, _controller.value);

  int _timesTapped = 0;

  @override
  void dispose() {
    _controller.dispose();
    emailTextController.dispose();
    passwordTextController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _controller,
      builder: (context, child) {
        return Positioned(
          height: lerp(minHeight, maxHeight),
          left: 0,
          right: 0,
          bottom: 0,
          child: GestureDetector(
            onVerticalDragUpdate: _handleDragUpdate,
            onVerticalDragEnd: _handleDragEnd,
            child: Container(
              decoration: const BoxDecoration(
                color: Colors.white,
              ),
              child: Stack(
                children: <Widget>[
                  _builtPassField(),
                  Padding(
                    padding: EdgeInsets.all(24),
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: <Widget>[
                        SizedBox(
                          height: 50,
                        ),
                        Expanded(
                            child: GestureDetector(
                              onTap: _toogle,
                              child: Container(
                                color: Colors.transparent,
                                child: IgnorePointer(
                                  child: TextField(
                                      onChanged: (text) {
                                        setState(() {
                                          emailText = text;
                                        });
                                      },
                                      focusNode: focusNode,
                                      controller: emailTextController,
                                      keyboardType: TextInputType.emailAddress,
                                      onSubmitted: (text) {
                                        FocusScope.of(context)
                                            .requestFocus(focusNodePassword);
                                      },
                                      decoration: InputDecoration(
                                          prefixIcon: Container(
                                            width: 50,
                                            child: Icon(Icons.email),
                                          ),
                                          border: InputBorder.none,
                                          labelText: "Enter your email",
                                          labelStyle: TextStyle(fontSize: 20))),
                                ),
                              ),
                            )),
                      ],
                    ),
                  ),
                  _builtFloatingButton(),
                  //_builtCreateAccount(),
                  //MenuButton(),
                  _builtGetMoving(),
                  _builtSocial(),
                ],
              ),
            ),
          ),
        );
      },
    );
  }

  Widget _builtFloatingButton() {
    return FloatinButtonLogin(
      isVisible: _controller.status == AnimationStatus.completed,
    );
  }

  Widget _builtCreateAccount() {
    return CreateAccountLabel(
      isVisible: _controller.status == AnimationStatus.completed,
    );
  }

  Widget _builtGetMoving() {
    return CreateGetMoving(
      isVisible: _controller.status != AnimationStatus.completed,
    );
  }

  Widget _builtPassField() {
    return CreatePassField(
      isVisible: _controller.status == AnimationStatus.completed,
    );
  }

  Widget _builtSocial() {
    return CreateSocialNetwork(
      isVisible: _controller.status != AnimationStatus.completed,
    );
  }

  void _handleDragUpdate(DragUpdateDetails details) {
    _controller.value -= details.primaryDelta / maxHeight;
  }

  void _handleDragEnd(DragEndDetails details) {
    if (_controller.isAnimating ||
        _controller.status == AnimationStatus.completed) return;

    final double flingVelocity =
        details.velocity.pixelsPerSecond.dy / maxHeight;

    if (flingVelocity < 0.0) {
      _controller.fling(velocity: math.max(2.0, -flingVelocity));
    } else if (flingVelocity > 0.0) {
      _controller.fling(velocity: math.min(-2.0, -flingVelocity));
    } else {
      _controller.fling(velocity: _controller.value < 0.5 ? -2.0 : 2.0);
    }
  }

  void _toogle() {
    print("test");
    final bool isOpen = _controller.status == AnimationStatus.completed;
    print(isOpen.toString());
    _controller.fling(velocity: 0.1); //isOpen ? -2 :

    FocusScope.of(context).requestFocus(focusNode);
  }
}

final List<Event> events = [
  Event('steve-johnson.jpeg', 'Shenzhen GLOBAL DESIGN AWARD 2018', '4.20-30'),
  Event('efe-kurnaz.jpg', 'Shenzhen GLOBAL DESIGN AWARD 2018', '4.20-30'),
  Event('rodion-kutsaev.jpeg', 'Dawan District Guangdong Hong Kong', '4.28-31'),
];

class Event {
  final String assetName;
  final String title;
  final String date;

  Event(this.assetName, this.title, this.date);
}

class FloatinButtonLogin extends StatelessWidget {
  final double bottomMargin;
  final bool isVisible;

  const FloatinButtonLogin({Key key, this.bottomMargin, this.isVisible})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Positioned(
      bottom: 30,
      right: 20,
      child: AnimatedOpacity(
        opacity: isVisible ? 1 : 0,
        duration: Duration(milliseconds: 200),
        child: RawMaterialButton(
          onPressed: () => _onLoginClick(context),
          splashColor: Colors.white,
          fillColor: Colors.black,
          elevation: 15.0,
          shape: CircleBorder(),
          child: Padding(
            padding: const EdgeInsets.all(20.0),
            child: Icon(
              Icons.arrow_forward,
              size: 30.0,
              color: Colors.white,
            ),
          ),
        ),
      ),
    );
  }
}

void _onLoginClick(BuildContext context) {
  String email = emailText;
  String pass = passText;
  var authBloc = MyApp.of(context).authBloc;
  LoadingDialog.showLoadingDialog(context, "Loading . . .");
  authBloc.signIn(email, pass, () {
    LoadingDialog.hideLoadingDialog(context);
    Navigator.of(context)
        .push(MaterialPageRoute(builder: (context) => MyHomePage()));
  }, (msg) {
    LoadingDialog.hideLoadingDialog(context);
    MsgDialog.showMsgDialog(context, "Login", msg);
  });
}

class CreateAccountLabel extends StatelessWidget {
  final bool isVisible;

  const CreateAccountLabel({Key key, this.isVisible}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Positioned(
      bottom: 30,
      left: 20,
      child: AnimatedOpacity(
        opacity: isVisible ? 1 : 0,
        duration: Duration(milliseconds: 200),
        child: GestureDetector(
            onTap: () {
              Navigator.push(context,
                  MaterialPageRoute(builder: (context) => RegisterPage()));
            },
            child: Text("Create an Account",
                style: TextStyle(fontSize: 18, color: Colors.blue))),
      ),
    );
  }
}

class CreateGetMoving extends StatelessWidget {
  final bool isVisible;

  const CreateGetMoving({Key key, this.isVisible}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Positioned(
        top: 20,
        left: 30,
        child: AnimatedOpacity(
            opacity: isVisible ? 1 : 0,
            duration: Duration(milliseconds: 200),
            child: Text("Get moving with Uber",
                style: TextStyle(fontSize: 26, fontWeight: FontWeight.w500))));
  }
}

class CreatePassField extends StatefulWidget {
  final bool isVisible;

  const CreatePassField({Key key, this.isVisible}) : super(key: key);

  @override
  _CreatePassFieldState createState() => _CreatePassFieldState();
}

class _CreatePassFieldState extends State<CreatePassField> {
  @override
  Widget build(BuildContext context) {
    void _reqFocusPassword() {
      FocusScope.of(context).requestFocus(focusNodePassword);
    }

    return Positioned(
        top: 160,
        left: 30,
        child: AnimatedOpacity(
            opacity: widget.isVisible ? 1 : 0,
            duration: Duration(milliseconds: 200),
            child: GestureDetector(
              onTap: _reqFocusPassword,
              child: Container(
                width: 600,
                child: IgnorePointer(
                  child: TextField(
                      focusNode: focusNodePassword,
                      controller: passwordTextController,
                      onChanged: (text) {
                        setState(() {
                          passText = text;
                        });
                      },
                      onSubmitted: (text) {
                        _onLoginClick(context);
                      },
                      keyboardType: TextInputType.text,
                      obscureText: true,
                      decoration: InputDecoration(
                          prefixIcon: Container(
                            width: 50,
                            child: Icon(Icons.lock),
                          ),
                          border: InputBorder.none,
                          labelText: "Enter your password",
                          labelStyle: TextStyle(fontSize: 20))),
                ),
              ),
            )));
  }
}

class CreateSocialNetwork extends StatelessWidget {
  final bool isVisible;

  const CreateSocialNetwork({Key key, this.isVisible}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Positioned(
        bottom: 30,
        left: 30,
        child: AnimatedOpacity(
          opacity: isVisible ? 1 : 0,
          duration: Duration(milliseconds: 200),
          child: GestureDetector(
              onTap: () {
                Navigator.push(context,
                    MaterialPageRoute(builder: (context) => RegisterPage()));
              },
              child: Text("Or create an account",
                  style: TextStyle(fontSize: 18, color: Colors.blue))),
        ));
  }
}
```
Este algoritmo irá ser usado no login e registro do usuario.


`functionalButton.dart`
```
import "package:flutter/material.dart";

class FunctionalButton extends StatefulWidget {
  final String title;
  final IconData icon;
  final Function() onPressed;

  const FunctionalButton({Key key, this.title, this.icon, this.onPressed})
      : super(key: key);

  @override
  _FunctionalButtonState createState() => _FunctionalButtonState();
}

class _FunctionalButtonState extends State<FunctionalButton> {
  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.start,
      crossAxisAlignment: CrossAxisAlignment.center,
      mainAxisSize: MainAxisSize.min,
      children: <Widget>[
        RawMaterialButton(
          onPressed: widget.onPressed,
          splashColor: Colors.black,
          fillColor: Colors.white,
          elevation: 15.0,
          shape: CircleBorder(),
          child: Padding(
              padding: EdgeInsets.all(10.0),
              child: Icon(
                widget.icon,
                size: 30.0,
                color: Colors.black,
              )),
        ),
        Container(
          margin: EdgeInsets.symmetric(vertical: 5.0, horizontal: 2.0),
          child: Text(
            widget.title,
            style: TextStyle(fontSize: 15.0, color: Colors.black),
          ),
        )
      ],
    );
  }
}
```
Algoritmo para poder ser feito botões, assim como o botão 'GO' em `taxi_driver`

`home_menu_drawer.dart`
```
import 'package:flutter/material.dart';

class HomeMenuDrawer extends StatefulWidget {
  HomeMenuDrawer({Key key}) : super(key: key);

  _HomeMenuDrawerState createState() => _HomeMenuDrawerState();
}

class _HomeMenuDrawerState extends State<HomeMenuDrawer> {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return ListView(
      children: <Widget>[
        UserAccountsDrawerHeader(
          decoration: BoxDecoration(color: Colors.black),
          accountName: Text("Iris"),
          accountEmail: Row(
            children: <Widget>[
              Text("5.0"),
              Icon(
                Icons.star,
                color: Colors.white,
                size: 12,
              )
            ],
          ),
          currentAccountPicture: ClipOval(
            child: Image.asset("assets/img/user_profile.jpg", width: 10, height: 10, fit: BoxFit.cover,),
          ),
        ),
        Column(crossAxisAlignment: CrossAxisAlignment.start, children: <Widget>[
          linkMenuDrawer('Payment', () {
            Navigator.pushNamed(context, '/payment');
          }),
          linkMenuDrawer('Your Trips', () {
            Navigator.pushNamed(context, '/your_trip');
          }),
          linkMenuDrawer('Free Rides', () {
            Navigator.pushNamed(context, '/free_rides');
          }),
          linkMenuDrawer('Settings', () {
            Navigator.pushNamed(context, '/settings');
          }),
          linkMenuDrawer('Help', () {
            Navigator.pushNamed(context, '/help');
          }),
        ]),
      ],
    );
  }
}

Widget linkMenuDrawer(String title, Function onPressed) {
  return InkWell(
    onTap: onPressed,
    splashColor: Colors.black,
    child: Container(
      padding: EdgeInsets.symmetric(vertical: 13, horizontal: 15),
      width: double.infinity,
      child: Text(
        title,
        style: TextStyle(fontSize: 15.0),
      ),
    ),
  );
}
```
Menu que ficará na pagina principal do passageiro.

`loading_dialogs.dart`
```
import 'package:flutter/material.dart';

class LoadingDialog {
  static void showLoadingDialog(BuildContext context, String msg) {
    showDialog(
      context: context,
      barrierDismissible: false,
      builder: (context) => Dialog(
        child: Container(
          height: 100,
          color: Colors.white,
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              CircularProgressIndicator(),
              Padding(
                padding: EdgeInsets.fromLTRB(0, 10, 0, 0),
                child: Text(
                  msg,
                  style: TextStyle(fontSize: 18),
                ),
              )
            ],
          ),
        ),
      ));
  }

  static void hideLoadingDialog(BuildContext context) {
    Navigator.of(context).pop(LoadingDialog);
  }
}
```
Algoritmo para ser feito as animações de carregamento (Aquela bolinha girando).

`msg_dialog.dart`
```
import 'package:flutter/material.dart';

class MsgDialog {
  static void showMsgDialog(BuildContext context, String title, String msg) {
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text(title),
        content: Text(msg),
        actions: <Widget>[
          FlatButton(
            onPressed: () {
              Navigator.of(context).pop(MsgDialog);
            },
            child: Text("OK"),
          )
        ],
      ));
  }
}
```
Algoritmo para pipocar um caixa de dialogo na tela.

`ride_picker.dart`
```
import 'package:flutter/material.dart';
import 'package:taxidriver/src/model/place_item_res.dart';
import 'package:taxidriver/src/ui/pages/ride_picker_page.dart';

class RidePicker extends StatefulWidget {
  final Function(PlaceItemRes, bool) onSelected;
  RidePicker(this.onSelected);

  _RidePickerState createState() => _RidePickerState();
}

class _RidePickerState extends State<RidePicker> {
  PlaceItemRes fromAddress;
  PlaceItemRes toAddress;
  @override
  Widget build(BuildContext context) {
    return Container(
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.all(Radius.circular(10)),
        boxShadow: [
          BoxShadow(
              color: Color(0x88999999), offset: Offset(0, 5), blurRadius: 5.0)
        ],
      ),
      child: Column(
        children: <Widget>[
          Container(
            width: double.infinity,
            height: 50,
            child: FlatButton(
              onPressed: () {
                Navigator.of(context).push(MaterialPageRoute(
                    builder: (context) => RidePickerPage(
                        fromAddress == null ? "" : fromAddress.name,
                            (place, isFrom) {

                          widget.onSelected(place, isFrom);
                          fromAddress = place;
                          setState(() {});
                        }, true)));
              },
              child: SizedBox(
                width: double.infinity,
                height: double.infinity,
                child: Stack(
                  alignment: AlignmentDirectional.centerStart,
                  children: <Widget>[
                    SizedBox(
                      height: 40.0,
                      width: 50.0,
                      child: Center(
                        child: Container(
                            margin: EdgeInsets.only(top: 2),
                            width: 10,
                            height: 10,
                            decoration: BoxDecoration(color: Colors.black)),
                      ),
                    ),
                    Positioned(
                      right: 0,
                      top: 0,
                      width: 40,
                      height: 50,
                      child: Center(
                        child: Icon(
                          Icons.close,
                          size: 18,
                        ),
                      ),
                    ),
                    Padding(
                      padding: EdgeInsets.only(left: 40.0, right: 50.0),
                      child: Text(
                        fromAddress == null ? "pickup location" : fromAddress.name,
                        overflow: TextOverflow.ellipsis,
                        style: TextStyle(fontSize: 16, color: fromAddress == null ? Colors.grey : Colors.black),
                      ),
                    )
                  ],
                ),
              ),
            ),
          ),
          Divider(),
          Container(
            width: double.infinity,
            height: 50,
            child: FlatButton(
              onPressed: () {
                Navigator.of(context).push(MaterialPageRoute(
                    builder: (context) =>
                        RidePickerPage(toAddress == null ? '' : toAddress.name,
                                (place, isFrom) {
                              widget.onSelected(place, isFrom);
                              toAddress = place;
                              setState(() {});
                            }, false)));
              },
              child: SizedBox(
                width: double.infinity,
                height: double.infinity,
                child: Stack(
                  alignment: AlignmentDirectional.centerStart,
                  children: <Widget>[
                    SizedBox(
                      height: 40.0,
                      width: 50.0,
                      child: Center(
                        child: Container(
                            margin: EdgeInsets.only(top: 2),
                            width: 10,
                            height: 10,
                            decoration: BoxDecoration(color: Colors.blue)),
                      ),
                    ),
                    Positioned(
                      right: 0,
                      top: 0,
                      width: 40,
                      height: 50,
                      child: Center(
                        child: Icon(
                          Icons.close,
                          size: 18,
                        ),
                      ),
                    ),
                    Padding(
                      padding: EdgeInsets.only(left: 40.0, right: 50.0),
                      child: Text(
                        toAddress == null ? "where to go ?" : toAddress.name,
                        overflow: TextOverflow.ellipsis,
                        style: TextStyle(fontSize: 16, color: toAddress == null ? Colors.grey: Colors.black),
                      ),
                    )
                  ],
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```
Algoritmo para o passageiro digitar para onde ele quer ir e também para escolher um motorista (categoria // recurso a ser implementado).

### Pages

`add_cart.dart`
```
import 'package:flutter/material.dart';

class AddCardPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return AddCardView();
  }
}

class AddCardView extends StatefulWidget {
  @override
  _AddCardViewState createState() => _AddCardViewState();
}

class _AddCardViewState extends State<AddCardView> {
  DateTime selectedDate = DateTime.now();

  Future<Null> _selectDate(BuildContext context) async {
    final DateTime picked = await showDatePicker(
        context: context,
        initialDate: selectedDate,
        firstDate: DateTime(2020, 04),
        lastDate: DateTime(2030)
    );
    if (picked != null && picked != selectedDate) {
      setState(() {
        selectedDate = picked;
      });
    }
  }
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.black,
        title: Text("Add Card"),
      ),
      body: Container(
        decoration: BoxDecoration(
          color: Colors.white,
        ),
        child: ListView(
          padding: EdgeInsets.symmetric(horizontal: 20),
          children: <Widget>[
            TextField(decoration: InputDecoration(prefixIcon: Icon(Icons.credit_card), labelText: "Card Number")),
            Row(
              children: <Widget>[
                Flexible(child: TextField(decoration: InputDecoration(hintText: "MM/YY"))),
                SizedBox(width: 40),
                Flexible(child: TextField(decoration: InputDecoration(hintText: "CVV"))),
              ],
            ),
            TextField(decoration: InputDecoration(prefixIcon: Icon(Icons.flag), labelText: "Country")),
            TextField(decoration: InputDecoration(prefixIcon: Icon(Icons.confirmation_number), labelText: "ZIP Code")),
          ],
        ),
      ),
    );
  }
}
```
Pagina para adicionar um cartão.

`add_payment_method.dart`
```
import 'package:flutter/material.dart';

class AddPaymentMethodPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return AddPaymentMethodView();
  }
}

class AddPaymentMethodView extends StatefulWidget {
  @override
  _AddPaymentMethodViewState createState() => _AddPaymentMethodViewState();
}

class _AddPaymentMethodViewState extends State<AddPaymentMethodView> {
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.black,
        title: Text("Add Payment Method"),
      ),
      body: Container(
        decoration: BoxDecoration(
          color: Colors.white,
        ),
        child: ListView(
          padding: EdgeInsets.only(left: 20),
          children: <Widget>[
            Padding(
              padding: EdgeInsets.only(top: 40),
              child: Row(
                children: <Widget>[
                  Icon(Icons.payment),
                  SizedBox(
                    width: 10,
                  ),
                  GestureDetector(onTap: () {Navigator.pushNamed(context, "/add_card");}, child: Text("Credit or Debit Card")),
                ],
              ),
            ),
            Padding(
              padding: EdgeInsets.only(top: 30),
              child: Row(
                children: <Widget>[
                  Icon(Icons.payment),
                  SizedBox(
                    width: 10,
                  ),
                  Text("Paypal"),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```
Pagina para definir o metodo de pagamento.

`free_rides.dart`
```
import 'package:flutter/material.dart';

class FreeRidesPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return FreeRidesView();
  }
}

class FreeRidesView extends StatefulWidget {
  @override
  _FreeRidesViewState createState() => _FreeRidesViewState();
}

class _FreeRidesViewState extends State<FreeRidesView> {
  @override
  void initState() {
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.black,
          title: Text("Free Rides"),
        ),
        body: Container(
          padding: EdgeInsets.symmetric(horizontal: 20),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.start,
            crossAxisAlignment: CrossAxisAlignment.start,
            children: <Widget>[
              SizedBox(
                height: 50,
              ),
              Text(
                "Want more Uber",
                style: TextStyle(fontSize: 36),
              ),
              SizedBox(
                height: 20,
              ),
              Text(
                "for less?",
                style: TextStyle(fontSize: 36),
              ),
              SizedBox(
                height: 20,
              ),
              Text(
                "Get a free ride worth up to \$20 when you refer a friend to try Uber.",
                style: TextStyle(height: 1.4, fontSize: 20, color: Colors.grey),
              ),
              SizedBox(
                height: 12,
              ),
              GestureDetector(
                  onTap: () {
                    print("How Invites work tapped");
                  },
                  child: Text(
                    "How Invites work",
                    style: TextStyle(
                        height: 1.4, fontSize: 20, color: Colors.blue),
                  )),
              Container(
                width: double.infinity,
                height: 160,
                child: Row(
                  mainAxisAlignment: MainAxisAlignment.end,
                  crossAxisAlignment: CrossAxisAlignment.end,
                  children: <Widget>[
                    Icon(
                      Icons.person_outline,
                      size: 110,
                    ),
                    Icon(
                      Icons.chat_bubble_outline,
                      size: 110,
                    ),
                    Icon(
                      Icons.person_outline,
                      size: 110,
                    ),
                  ],
                ),
              ),
              SizedBox(
                height: 10,
              ),
              Text(
                "Your Invite Code",
                style: TextStyle(height: 1.4, fontSize: 20, color: Colors.grey),
              ),
              SizedBox(
                height: 10,
              ),
              TextField(
                  decoration: InputDecoration(border: OutlineInputBorder(), hintText: "q1yzx", hintStyle: TextStyle(color: Colors.black,))),
              SizedBox(
                height: 14,
              ),
              GestureDetector(
                onTap: (){},
                child: Container(
                  width: double.infinity,
                  height: 60,
                  margin: EdgeInsets.only(bottom: 10),
                  alignment: FractionalOffset.center,
                  decoration: BoxDecoration(
                    color: Colors.black,
                    borderRadius:
                    BorderRadius.all(const Radius.circular(4.0)),
                  ),
                  child: Text('SEND INVITES',
                      style: TextStyle(color: Colors.white, fontSize: 18)),
                ),
              ),
            ],
          ),
        ));
  }
}
```
Pagina para o usuario mandar convites para os seus amigos para conseguir viagens gratis ou descontos.

`help.dart`
```
import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';
import 'dart:async';

class HelpPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return HelpView();
  }
}

class HelpView extends StatefulWidget {
  @override
  _HelpViewState createState() => _HelpViewState();
}

class _HelpViewState extends State<HelpView> {
  Completer<GoogleMapController> _controller = Completer();
  Map<PolylineId, Polyline> polylines = <PolylineId, Polyline>{};
  int _polylineIdCounter = 1;
  static final CameraPosition _cameraPosition = CameraPosition(
    target: LatLng(-8.913455, 13.203063),
    zoom: 17.18,
  );

  @override
  void initState() {
    super.initState();
    _addtripPoly();
  }

  void _addtripPoly() {
    final String polylineIdVal = 'polyline_id_$_polylineIdCounter';
    _polylineIdCounter++;
    final PolylineId polylineId = PolylineId(polylineIdVal);

    final Polyline polyline = Polyline(
      polylineId: polylineId,
      consumeTapEvents: true,
      color: Colors.black,
      width: 5,
      points: _createTripPoints(),
      onTap: () {},
    );

    setState(() {
      polylines[polylineId] = polyline;
    });
  }

  LatLng _createLatLng(double lat, double lng) {
    return LatLng(lat, lng);
  }

  List<LatLng> _createTripPoints() {
    final List<LatLng> points = <LatLng>[];
    points.add(_createLatLng(-8.913012, 13.202450));
    points.add(_createLatLng(-8.913297, 13.202253));
    points.add(_createLatLng(-8.913752, 13.202803));
    points.add(_createLatLng(-8.913455, 13.203063));
    return points;
  }

  DateTime selectedDate = DateTime.now();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.black,
          title: Text("Help"),
        ),
        body: ListView(
          children: <Widget>[
            Container(
              height: 80,
              padding: EdgeInsets.symmetric(horizontal: 20),
              color: Colors.grey.withOpacity(0.15),
              child: Align(
                  alignment: Alignment.centerLeft,
                  child: Text(
                    "Your last trip",
                    style: TextStyle(fontSize: 18),
                  )),
            ),
            ListTile(
              leading: ClipOval(
                child: Image.asset(
                  "assets/images/user_profile.jpg",
                  width: 60,
                  height: 60,
                  fit: BoxFit.cover,
                ),
              ),
              title: Text("Today at 1:05 AM"),
              subtitle: Row(
                children: <Widget>[
                  Text("Infinity G Coupe"),
                  SizedBox(
                    width: 10,
                  ),
                  Text("ABC123",
                      style: TextStyle(
                        fontWeight: FontWeight.bold,
                      ))
                ],
              ),
              trailing: Text("\$7.42"),
            ),
            Container(
              height: 150,
              width: double.infinity,
              child: GoogleMap(
                polylines: Set<Polyline>.of(polylines.values),
                mapType: MapType.normal,
                initialCameraPosition: _cameraPosition,
                onTap: (LatLng location) {
                  Navigator.pushNamed(context, "/select_issue");
                },
                onMapCreated: (GoogleMapController controller) {
                  _controller.complete(controller);
                },
              ),
            ),
            SizedBox(
              height: 20,
            ),
            Container(
              padding: EdgeInsets.symmetric(horizontal: 20),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: <Widget>[
                  SizedBox(
                    height: 10,
                  ),
                  Text(
                    "Report an issue with this trip",
                    style: TextStyle(fontSize: 18),
                  ),
                  SizedBox(
                    height: 30,
                  ),
                  Container(
                    height: 80,
                    width: double.infinity,
                    padding: EdgeInsets.symmetric(horizontal: 20),
                    color: Colors.grey.withOpacity(0.15),
                    child: Align(
                        alignment: Alignment.centerLeft,
                        child: Text(
                          "Additional topics",
                          style: TextStyle(fontSize: 18),
                        )),
                  ),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "Trips and Fare Review",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "A Guide to Uber",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "Accessibility",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "Acount and Payment",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "Driving with Uber",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "Delivery",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "Events and Inquiries",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "I was envolved in an acident",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "UberPOOL issues",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  Divider(),
                  ListTile(
                    onTap: () {},
                    title: Text(
                      "Critical Safety Response Line",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                ],
              ),
            )
          ],
        ));
  }
}
```
Tela de ajuda do App.

`home.dart`. No codigo abaixo eu tive que recorrer a uma solução diferente da original portanto não posso garantir se a logica do algoritmo foi alterada.
```
import 'dart:async';
import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';
import 'package:location/location.dart';
import 'package:flutter/services.dart';
import 'package:taxidriver/src/model/place_item_res.dart';
import 'package:taxidriver/src/ui/widgets/functionalButton.dart';
import 'package:taxidriver/src/ui/widgets/home_menu_drawer.dart';
import 'package:taxidriver/src/ui/widgets/ride_picker.dart';
import 'package:taxidriver/src/util/map_util.dart';

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
  final String title;
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  _MyHomePageState();
  GlobalKey<ScaffoldState> _scaffoldKey = new GlobalKey();
  Completer<GoogleMapController> _completer = Completer();
  MapUtil mapUtil = MapUtil();
  Location _locationService = Location();
  LatLng currentLocation;
  LatLng _center = LatLng(-8.913025, 13.202462);
  PermissionStatus _permission;
  List<Marker> _markers = List();
  List<Polyline> routes = new List();
  bool done = false;
  String error;

  @override
  void initState() {
    super.initState();
    initPlatformState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      resizeToAvoidBottomInset: false,
      key: _scaffoldKey,
      bottomSheet: Container(
        height: 300,
        decoration: BoxDecoration(color: Colors.black),
        child: Column(),
      ),
      drawer: Drawer(
        child: HomeMenuDrawer(),
      ),
      body: Stack(
        children: <Widget>[
          GoogleMap(
            mapType: MapType.normal,
            initialCameraPosition: CameraPosition(
              target: _center,
              zoom: 13.0,
            ),
            onMapCreated: (GoogleMapController controller) {
              _completer.complete(controller);
            },
            markers: Set<Marker>.of(_markers),
            polylines: Set<Polyline>.of(routes),
          ),
          Positioned(
            left: 0,
            top: 0,
            right: 0,
            child: Column(
              children: <Widget>[
                AppBar(
                  backgroundColor: Colors.transparent,
                  elevation: 0.0,
                  leading: FlatButton(
                    onPressed: () {
                      _scaffoldKey.currentState.openDrawer();
                    },
                    child: Icon(
                      Icons.menu,
                      color: Colors.black,
                    ),
                  ),
                ),
                Padding(
                  padding: EdgeInsets.only(top: 20, left: 20, right: 20),
                  child: RidePicker(onPlaceSelected),
                )
              ],
            ),
          ),
          Positioned(
            child: Align(
              alignment: Alignment.bottomCenter,
              child: Row(
                crossAxisAlignment: CrossAxisAlignment.center,
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  FunctionalButton(
                    icon: Icons.work,
                    title: "Work",
                    onPressed: () {},
                  ),
                  FunctionalButton(
                    icon: Icons.home,
                    title: "Home",
                    onPressed: () {},
                  ),
                  FunctionalButton(
                    icon: Icons.timer,
                    title: "Zinc Gym",
                    onPressed: () {},
                  ),
                ],
              ),
            ),
          )
        ],
      ),
    );
  }

  void onPlaceSelected(PlaceItemRes place, bool fromAddress) {
    var mkId = fromAddress ? "from_address" : "to_address";
    _addMarker(mkId, place);
    addPolyline();
  }

  void _addMarker(String mkId, PlaceItemRes place) async {
    // remove old
    _markers.remove(mkId);
    //_mapController.clearMarkers();

    Marker marker = Marker(
      markerId: MarkerId(mkId),
      draggable: true,
      position: LatLng(place.lat, place.lng),
      infoWindow: InfoWindow(title: mkId),
    );

    setState(() {
      if (mkId == "from_address") {
        _markers[0] = (marker);
        List mmmm = _markers;
        print(mmmm);
      } else if (mkId == "to_address") {
        _markers.add(marker);
        List mmmm = _markers;
        print(mmmm);
      }
    });
  }

  getCurrentLocation() async {
    currentLocation = await mapUtil.getCurrentLocation();
    _center = LatLng(currentLocation.latitude, currentLocation.longitude);
    Marker marker = Marker(
      markerId: MarkerId('location'),
      position: _center,
      infoWindow: InfoWindow(title: 'My Location'),
    );
    setState(() {
      _markers.add(marker);
    });
  }

  addPolyline() async {
    //routes.clear();
    if (_markers.length > 1) {
      mapUtil
          .getRoutePath(
          LatLng(_markers[0].position.latitude,
              _markers[0].position.longitude),
          LatLng(_markers[1].position.latitude,
              _markers[1].position.longitude))
          .then((locations) {
        List<LatLng> path = new List();

        locations.forEach((location) {
          path.add(new LatLng(location.latitude, location.longitude));
        });

        final Polyline polyline = Polyline(
          polylineId: PolylineId(_markers[1].position.latitude.toString() +
              _markers[1].position.longitude.toString()),
          consumeTapEvents: true,
          color: Colors.black,
          width: 2,
          points: path,
        );

        setState(() {
          routes.add(polyline);
        });
      });
    }
  }

  initPlatformState() async {
    await _locationService.changeSettings(
        accuracy: LocationAccuracy.HIGH, interval: 1000);

    LocationData location;
    // Platform messages may fail, so we use a try/catch PlatformException.
    try {
      bool serviceStatus = await _locationService.serviceEnabled();
      print("Service status: $serviceStatus");
      if (!serviceStatus) {
        _permission = await _locationService.requestPermission();
        print("Permission: $_permission");
        if (serviceStatus) {
          location = await _locationService.getLocation();
          Marker marker = Marker(
            markerId: MarkerId('from_address'),
            position: LatLng(location.latitude, location.longitude),
            infoWindow: InfoWindow(title: 'My location'),
          );
          if (mounted) {
            setState(() {
              currentLocation = LatLng(location.latitude, location.longitude);
              _center =
                  LatLng(currentLocation.latitude, currentLocation.longitude);
              _markers.add(marker);
              done = true;
            });
          }
        }
      } else {
        bool serviceStatusResult = await _locationService.requestService();
        print("Service status activated after request: $serviceStatusResult");
        if (serviceStatusResult) {
          initPlatformState();
        }
      }
    } on PlatformException catch (e) {
      print(e);
      if (e.code == 'PERMISSION_DENIED') {
        error = e.message;
      } else if (e.code == 'SERVICE_STATUS_ERROR') {
        error = e.message;
      }
      //location = null;
    }
  }
}
```
Tela principal do App.

`instant_pay.dart`
```
import 'package:flutter/material.dart';

class InstanstPayPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return InstanstPayView();
  }
}

class InstanstPayView extends StatefulWidget {
  @override
  _InstanstPayViewState createState() => _InstanstPayViewState();
}

class _InstanstPayViewState extends State<InstanstPayView> {
  @override
  void initState() {
    super.initState();
  }


  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.black,
          title: Text("Instant Pay"),
        ),
        body: ListView(
          children: <Widget>[
          ],
        ));
  }
}
```
Pagamento instantaneo, incompleto

`login.dart`
```
import 'package:flutter/material.dart';
import 'package:taxidriver/src/ui/widgets/exhibition_bottom_sheet.dart';

class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return LoginView();
  }
}

class LoginView extends StatefulWidget {
  @override
  _LoginViewState createState() => _LoginViewState();
}

class _LoginViewState extends State<LoginView> {
  @override
  void initState() {
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      resizeToAvoidBottomPadding: false,
      body: Stack(
        children: <Widget>[
          Container(
            decoration: BoxDecoration(
                image: DecorationImage(
                    image: AssetImage(
                      "assets/images/bg.jpg",
                    ),
                    fit: BoxFit.cover)),
            child: Center(
              child: Container(
                decoration: BoxDecoration(
                  color: Colors.white,
                  boxShadow: [
                    BoxShadow(
                        color: Colors.black38,
                        offset: Offset(1.0, 1.0),
                        blurRadius: 15,
                        spreadRadius: 1)
                  ],
                ),
                width: 120,
                height: 120,
                margin: EdgeInsets.only(bottom: 190),
                child: Center(
                    child: Text("UBER",
                        style: TextStyle(
                            fontWeight: FontWeight.bold, fontSize: 26))),
              ),
            ),
          ),
          ExhibitionBottomSheet(),
        ],
      ),
    );
  }
}
```
Tela de login. 

`payment.dart`
```
import 'package:flutter/material.dart';

class PaymentPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return PaymentView();
  }
}

class PaymentView extends StatefulWidget {
  @override
  _PaymentViewState createState() => _PaymentViewState();
}

class _PaymentViewState extends State<PaymentView> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.black,
        title: Text("Payment"),
      ),
      body: Container(
        decoration: BoxDecoration(
          color: Colors.white,
        ),
        child: ListView(
          padding: EdgeInsets.only(left: 20),
          children: <Widget>[
            Padding(
                padding: EdgeInsets.symmetric(vertical: 26),
                child: Text(
                  "Payment Methods",
                  style: TextStyle(color: Colors.grey),
                )),
            Row(
              children: <Widget>[
                Icon(Icons.payment),
                SizedBox(
                  width: 10,
                ),
                Text("Paypal"),
              ],
            ),
            SizedBox(
              height: 20,
            ),
            GestureDetector(
                onTap: () {Navigator.pushNamed(context, '/add_payment');},
                child: Text(
                  "Add Payment Method",
                  style: TextStyle(color: Colors.blue),
                )),
            Divider(),
            Padding(
                padding: EdgeInsets.symmetric(vertical: 20),
                child: Text(
                  "Promotions",
                  style: TextStyle(color: Colors.grey),
                )),
            Row(
              children: <Widget>[
                Icon(Icons.card_giftcard),
                SizedBox(
                  width: 10,
                ),
                Text("Rewards"),
                Spacer(),
                Text("1"),
                SizedBox(width: 20,)
              ],
            ),
            SizedBox(
              height: 20,
            ),
            GestureDetector(
                onTap: () {print("Payment Method");},
                child: Text(
                  "Add Promo/Gift Code",
                  style: TextStyle(color: Colors.blue),
                )),
          ],
        ),
      ),
    );
  }
}
```
Tela de Pagamento da viagem.

`register.dart`
```
import 'package:taxidriver/src/blocs/auth_bloc.dart';
import 'package:flutter/material.dart';
import 'package:taxidriver/src/ui/pages/home.dart';
import 'package:taxidriver/src/ui/widgets/loading_dialog.dart';
import 'package:taxidriver/src/ui/widgets/msg_dialog.dart';

class RegisterPage extends StatefulWidget {
  RegisterPage({Key key}) : super(key: key);

  _RegisterPageState createState() => _RegisterPageState();
}

class _RegisterPageState extends State<RegisterPage> {
  AuthBloc authBloc = AuthBloc();

  TextEditingController _nameController = TextEditingController();
  TextEditingController _emailController = TextEditingController();
  TextEditingController _passController = TextEditingController();
  TextEditingController _phoneController = TextEditingController();

  @override
  void dispose() {
    authBloc.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        padding: EdgeInsets.fromLTRB(30, 0, 30, 0),
        constraints: BoxConstraints.expand(),
        color: Colors.white,
        child: SingleChildScrollView(
          child: Column(
            children: <Widget>[
              SizedBox(
                height: 100,
              ),
              Text("Signup with Uber in simple steps",
                  style: TextStyle(
                      fontSize: 18,
                      fontWeight: FontWeight.bold,
                      color: Colors.black)),
              Padding(
                padding: const EdgeInsets.fromLTRB(0, 80, 0, 10),
                child: StreamBuilder(
                  stream: authBloc.nameStream,
                  builder: (context, snapshot) => TextField(
                      controller: _nameController,
                      style: TextStyle(fontSize: 18),
                      keyboardType: TextInputType.text,
                      decoration: InputDecoration(
                          errorText: snapshot.hasError ? snapshot.error : null,
                          border: InputBorder.none,
                          labelText: "Name",
                          prefixIcon: Container(
                            width: 50,
                            child: Icon(Icons.person),
                          ),
                          labelStyle: TextStyle(fontSize: 20))),
                ),
              ),
              StreamBuilder(
                stream: authBloc.phoneStream,
                builder: (context, snapshot) => TextField(
                    controller: _phoneController,
                    style: TextStyle(fontSize: 18),
                    keyboardType: TextInputType.number,
                    decoration: InputDecoration(
                        errorText: snapshot.hasError ? snapshot.error : null,
                        border: InputBorder.none,
                        labelText: "Phone Number",
                        prefixIcon: Container(
                          width: 50,
                          child: Icon(Icons.phone),
                        ),
                        labelStyle: TextStyle(fontSize: 20))),
              ),
              Padding(
                padding: const EdgeInsets.fromLTRB(0, 10, 0, 10),
                child: StreamBuilder(
                  stream: authBloc.emailStream,
                  builder: (context, snapshot) => TextField(
                      controller: _emailController,
                      style: TextStyle(fontSize: 18),
                      keyboardType: TextInputType.emailAddress,
                      decoration: InputDecoration(
                          errorText: snapshot.hasError ? snapshot.error : null,
                          border: InputBorder.none,
                          labelText: "Email",
                          prefixIcon: Container(
                            width: 50,
                            child: Icon(Icons.email),
                          ),
                          labelStyle: TextStyle(fontSize: 20))),
                ),
              ),
              StreamBuilder(
                stream: authBloc.passStream,
                builder: (context, snapshot) => TextField(
                    controller: _passController,
                    style: TextStyle(fontSize: 18),
                    keyboardType: TextInputType.text,
                    obscureText: true,
                    decoration: InputDecoration(
                        errorText: snapshot.hasError ? snapshot.error : null,
                        border: InputBorder.none,
                        labelText: "Password",
                        prefixIcon: Container(
                          width: 50,
                          child: Icon(Icons.security),
                        ),
                        labelStyle: TextStyle(fontSize: 20))),
              ),
              Padding(
                padding: const EdgeInsets.fromLTRB(0, 40, 0, 50),
                child: SizedBox(
                  width: double.infinity,
                  height: 52,
                  child: RawMaterialButton(
                    fillColor: Colors.black,
                    elevation: 5.0,
                    onPressed: () => _onSignupClicked(),
                    child: Text(
                      "Signup",
                      style: TextStyle(color: Colors.white),
                    ),
                    shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.all(Radius.circular(26))),
                  ),
                ),
              ),
              Padding(
                padding: const EdgeInsets.fromLTRB(0, 0, 0, 40),
                child: RichText(
                  text: TextSpan(
                      text: "Already a User ? ",
                      style: TextStyle(color: Colors.grey, fontSize: 16),
                      children: <TextSpan>[
                        TextSpan(
                            text: "Login now",
                            style: TextStyle(color: Colors.blue, fontSize: 16))
                      ]),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  void _onSignupClicked() {
    //print("teste");
    var isValid = authBloc.isValid(_nameController.text, _emailController.text,
        _passController.text, _phoneController.text);
    print(isValid);
    if (isValid) {
      //print(isValid);
      // create user
      //loadgin dialog
      LoadingDialog.showLoadingDialog(context, "Loading...");
      return authBloc.signUp(_emailController.text, _passController.text,
          _phoneController.text, _nameController.text, () {
            LoadingDialog.hideLoadingDialog(context);
            Navigator.push(
                context, MaterialPageRoute(builder: (context) => MyHomePage()));
          }, (msg) {
            //show msg dialog
            LoadingDialog.hideLoadingDialog(context);
            MsgDialog.showMsgDialog(context, "SignUp", msg);
          });
    }
    return;
  }
}
```
Tela de registro do usuario

`ride_picker_page.dart`
```
import 'dart:async';
import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';
import 'package:taxidriver/src/blocs/place_bloc.dart';
import 'package:taxidriver/src/model/place_item_res.dart';
import 'package:taxidriver/src/ui/widgets/home_menu_drawer.dart';

class RidePickerPage extends StatefulWidget {
  final String selectedAddress;
  final Function(PlaceItemRes, bool) onSelected;
  final bool _isFromAddress;
  RidePickerPage(this.selectedAddress, this.onSelected, this._isFromAddress);

  @override
  _RidePickerPageState createState() => _RidePickerPageState();
}

class _RidePickerPageState extends State<RidePickerPage> {
  var _addressController;
  var placeBloc = PlaceBloc();
  _RidePickerPageState();
  Completer<GoogleMapController> _controller = Completer();

  static final CameraPosition _cameraPosition = CameraPosition(
    target: LatLng(-8.913025, 13.202462),
    zoom: 17.0,
  );

  @override
  void initState() {
    _addressController = TextEditingController(text: "");
    super.initState();
  }

  @override
  void dispose() {
    placeBloc.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      resizeToAvoidBottomInset: false,
      bottomSheet: Container(
        height: 100,
        decoration: BoxDecoration(color: Colors.black),
        child: Column(),
      ),
      drawer: Drawer(
        child: HomeMenuDrawer(),
      ),
      body: Stack(
        children: <Widget>[
          GoogleMap(
            mapType: MapType.normal,
            initialCameraPosition: _cameraPosition,
            onMapCreated: (GoogleMapController controller) {
              _controller.complete(controller);
            },
          ),
          Positioned(
            left: 0,
            top: 0,
            right: 0,
            child: Column(
              children: <Widget>[
                AppBar(
                  backgroundColor: Colors.transparent,
                  elevation: 0.0,
                  leading: IconButton(
                    icon: Icon(
                      Icons.arrow_back,
                      color: Colors.black,
                    ),
                    onPressed: () {
                      Navigator.pop(context);
                    },
                  ),
                ),
                Padding(
                  padding: EdgeInsets.only(top: 20, left: 20, right: 20),
                  child: Container(
                    decoration: BoxDecoration(
                      color: Colors.white,
                      borderRadius: BorderRadius.all(Radius.circular(10)),
                      boxShadow: [
                        BoxShadow(
                            color: Color(0x88999999),
                            offset: Offset(0, 5),
                            blurRadius: 5.0)
                      ],
                    ),
                    child: Column(
                      children: <Widget>[
                        Container(
                          width: double.infinity,
                          height: 50,
                          child: FlatButton(
                            onPressed: () {},
                            child: SizedBox(
                              width: double.infinity,
                              height: double.infinity,
                              child: Stack(
                                alignment: AlignmentDirectional.centerStart,
                                children: <Widget>[
                                  SizedBox(
                                    height: 40.0,
                                    width: 50.0,
                                    child: Center(
                                      child: Container(
                                          margin: EdgeInsets.only(top: 2),
                                          width: 10,
                                          height: 10,
                                          decoration: BoxDecoration(
                                              color: Colors.black)),
                                    ),
                                  ),
                                  Positioned(
                                    right: 0,
                                    top: 0,
                                    width: 40,
                                    height: 50,
                                    child: Center(
                                      child: Icon(
                                        Icons.close,
                                        size: 18,
                                      ),
                                    ),
                                  ),
                                  Column(
                                    children: <Widget>[
                                      Padding(
                                          padding: EdgeInsets.only(
                                              left: 40.0, right: 50.0, top: 14),
                                          child: TextField(
                                            style: TextStyle(fontSize: 16),
                                            controller: _addressController,
                                            textInputAction:
                                            TextInputAction.search,
                                            onChanged: (str) {
                                              placeBloc.searchPlace(str);
                                            },
                                            decoration:
                                            InputDecoration.collapsed(
                                                hintText: ""),
                                          )),
                                    ],
                                  ),
                                ],
                              ),
                            ),
                          ),
                        ),
                      ],
                    ),
                  ),
                ),
                Container(
                  margin: EdgeInsets.symmetric(horizontal: 20),
                  child: StreamBuilder(
                    stream: placeBloc.placeStream,
                    builder: (context, snapshot) {
                      if (snapshot.hasData) {
                        if (snapshot.data == "start") {
                          return Center(
                            child: CircularProgressIndicator(),
                          );
                        }

                        List<PlaceItemRes> places = snapshot.data;
                        return Container(
                          child: ListView.separated(
                            shrinkWrap: true,
                            scrollDirection: Axis.vertical,
                            itemBuilder: (context, index) {
                              return Container(
                                decoration: BoxDecoration(
                                  color: Colors.white,
                                  borderRadius:
                                  BorderRadius.all(Radius.circular(10)),
                                  boxShadow: [
                                    BoxShadow(
                                        color: Color(0x88999999),
                                        offset: Offset(0, 5),
                                        blurRadius: 5.0)
                                  ],
                                ),
                                child: ListTile(
                                  title: Text(
                                    places.elementAt(index).name,
                                    style: TextStyle(color: Colors.black),
                                  ),
                                  subtitle:
                                  Text(places.elementAt(index).address),
                                  onTap: () {
                                    print("ontap");
                                    Navigator.of(context).pop();
                                    widget.onSelected(places.elementAt(index),
                                        widget._isFromAddress);
                                  },
                                ),
                              );
                            },
                            separatorBuilder: (context, index) => Divider(
                              height: 1,
                              color: Colors.grey,
                            ),
                            itemCount: places.length,
                          ),
                        );
                      } else {
                        return Container();
                      }
                    },
                  ),
                )
              ],
            ),
          ),
        ],
      ),
    );
  }
}
```
Tela para escolher o motorista

`select_issue.dart`
```
import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';
import 'dart:async';

class SelectIssuePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SelectIssueView();
  }
}

class SelectIssueView extends StatefulWidget {
  @override
  _SelectIssueViewState createState() => _SelectIssueViewState();
}

class _SelectIssueViewState extends State<SelectIssueView> {
  Completer<GoogleMapController> _controller = Completer();
  Map<PolylineId, Polyline> polylines = <PolylineId, Polyline>{};
  int _polylineIdCounter = 1;
  static final CameraPosition _cameraPosition = CameraPosition(
    target: LatLng(-8.913455, 13.203063),
    zoom: 17.18,
  );

  @override
  void initState() {
    super.initState();
    _addtripPoly();
  }

  void _addtripPoly() {
    final String polylineIdVal = 'polyline_id_$_polylineIdCounter';
    _polylineIdCounter++;
    final PolylineId polylineId = PolylineId(polylineIdVal);

    final Polyline polyline = Polyline(
      polylineId: polylineId,
      consumeTapEvents: true,
      color: Colors.black,
      width: 5,
      points: _createTripPoints(),
      onTap: () {},
    );

    setState(() {
      polylines[polylineId] = polyline;
    });
  }

  LatLng _createLatLng(double lat, double lng) {
    return LatLng(lat, lng);
  }

  List<LatLng> _createTripPoints() {
    final List<LatLng> points = <LatLng>[];
    points.add(_createLatLng(-8.913012, 13.202450));
    points.add(_createLatLng(-8.913297, 13.202253));
    points.add(_createLatLng(-8.913752, 13.202803));
    points.add(_createLatLng(-8.913455, 13.203063));
    return points;
  }

  DateTime selectedDate = DateTime.now();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.black,
          title: Text("Select an Issue"),
          actions: <Widget>[
            Column(
              mainAxisAlignment: MainAxisAlignment.center,
              crossAxisAlignment: CrossAxisAlignment.center,
              children: <Widget>[
                Container(
                    padding: EdgeInsets.only(right: 10),
                    child: Text(
                      "RECEIPT",
                      style: TextStyle(color: Colors.white),
                    ))
              ],
            )
          ],
        ),
        body: ListView(
          children: <Widget>[
            Container(
              height: 150,
              width: double.infinity,
              child: GoogleMap(
                polylines: Set<Polyline>.of(polylines.values),
                mapType: MapType.normal,
                initialCameraPosition: _cameraPosition,
                onMapCreated: (GoogleMapController controller) {
                  _controller.complete(controller);
                },
              ),
            ),
            SizedBox(
              height: 20,
            ),
            Container(
              padding: EdgeInsets.symmetric(horizontal: 20),
              child: Column(
                children: <Widget>[
                  ListTile(
                    leading: ClipOval(
                      child: Image.asset(
                        "assets/images/user_profile.jpg",
                        width: 60,
                        height: 60,
                        fit: BoxFit.cover,
                      ),
                    ),
                    title: Text("Today at 1:05 AM"),
                    subtitle: Row(
                      children: <Widget>[
                        Text("Infinity G Coupe"),
                        SizedBox(
                          width: 10,
                        ),
                        Text("ABC123",
                            style: TextStyle(
                              fontWeight: FontWeight.bold,
                            ))
                      ],
                    ),
                    trailing: Text("\$7.42"),
                  ),
                  Divider(),
                  SizedBox(
                    height: 10,
                  ),
                  Row(
                    children: <Widget>[
                      SizedBox(
                        width: 30,
                      ),
                      ClipOval(
                          child: Container(
                            color: Colors.black,
                            width: 10,
                            height: 10,
                          )),
                      SizedBox(width: 20,),
                      Text("Lenox PKwy, Atlanta, GA 30326, USA")
                    ],
                  ),
                  SizedBox(
                    height: 10,
                  ),
                  Row(
                    children: <Widget>[
                      SizedBox(
                        width: 30,
                      ),
                      Container(
                        color: Colors.black,
                        width: 10,
                        height: 10,
                      ),
                      SizedBox(width: 20,),
                      Text("4040 Peachtree Rd NE, Atlanta, GA 30319, USA")
                    ],
                  ),
                  SizedBox(height: 10,),
                  LinearProgressIndicator(backgroundColor: Colors.black, valueColor: null,),
                  SizedBox(height: 30,),
                  ListTile(
                    onTap: (){},
                    title: Text("I lost an item",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("I was incorrectly charged a cancellation fee",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("I would like a refund",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("My driver was unprofessional",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("My vehicle wasn't what I expected",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("I had an issue with receipt or payment option",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("I had an issue with my promo code or payment option",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("I was envolved in an acident",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("UberPOOL issues",style: TextStyle(fontSize: 18),),
                  ),
                  Divider(),
                  ListTile(
                    onTap: (){},
                    title: Text("Critical Safety Response Line",style: TextStyle(fontSize: 18),),
                  ),
                ],
              ),
            )
          ],
        ));
  }
}
```
Pagina para abrir reclamações.

`settings.dart`
```
import 'package:flutter/material.dart';

class SettingsPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SettingsView();
  }
}

class SettingsView extends StatefulWidget {
  @override
  _SettingsViewState createState() => _SettingsViewState();
}

class _SettingsViewState extends State<SettingsView> {
  @override
  void initState() {
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.black,
          title: Text("Account Settings"),
        ),
        body: ListView(
          children: <Widget>[
            SizedBox(
              height: 40,
            ),
            ListTile(
              leading: ClipOval(
                child: Image.asset(
                  "assets/img/user_profile.jpg",
                  width: 80,
                  height: 80,
                  fit: BoxFit.cover,
                ),
              ),
              title: Text("Iris"),
              subtitle: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: <Widget>[
                  Text("+244 922 88 40 32"),
                  SizedBox(
                    height: 1,
                  ),
                  Text("iris@taxidriver.com",
                      style: TextStyle(
                        fontWeight: FontWeight.bold,
                      ))
                ],
              ),
            ),
            SizedBox(
              height: 20,
            ),
            Divider(),
            SizedBox(
              height: 40,
            ),
            Container(
              padding: EdgeInsets.symmetric(horizontal: 20),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: <Widget>[
                  Text(
                    "Favorites",
                    style: TextStyle(fontSize: 22, color: Colors.grey),
                  ),
                  SizedBox(
                    height: 20,
                  ),
                  ListTile(
                    leading: Icon(Icons.home),
                    title: Text(
                      "Add Home",
                      style: TextStyle(fontSize: 18),
                    ),
                  ),
                  ListTile(
                    leading: Icon(Icons.work),
                    title: Text(
                      "Add Work",
                      style: TextStyle(fontSize: 18),
                    ),
                  )
                ],
              ),
            ),
            SizedBox(height: 20,),
            Divider(),
            Container(
              padding: EdgeInsets.symmetric(horizontal: 20),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: <Widget>[
                  Text(
                    "Profiles",
                    style: TextStyle(fontSize: 22, color: Colors.grey),
                  ),
                  SizedBox(
                    height: 20,
                  ),
                  ListTile(
                    title: Text(
                      "Add Home",
                      style: TextStyle(fontSize: 18, color: Colors.blue),
                    ),
                    subtitle: Text("Separate work and personal receips"),
                  ),
                  ListTile(
                    title: Text(
                      "Add Family Profile",
                      style: TextStyle(fontSize: 18, color: Colors.blue),
                    ),
                    subtitle: Text("Pay for loved ones track their rides"),
                  ),
                ],
              ),
            ),
          ],
        ));
  }
}
```
Tela para configurar o perfil do passageiro.

`your_trips.dart`
```
import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';
import 'dart:async';



class YourTripPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return YourTripView();
  }
}

class YourTripView extends StatefulWidget {
  @override
  _YourTripViewState createState() => _YourTripViewState();
}

class _YourTripViewState extends State<YourTripView> {

  Completer<GoogleMapController> _controller = Completer();
  Map<PolylineId, Polyline> polylines = <PolylineId, Polyline>{};
  int _polylineIdCounter = 1;
  static final CameraPosition _cameraPosition = CameraPosition(
    target: LatLng(-8.913455, 13.203063),
    zoom: 17.18,
  );

  @override
  void initState() {
    super.initState();
    _addtripPoly();
  }

  void _addtripPoly() {
    final String polylineIdVal = 'polyline_id_$_polylineIdCounter';
    _polylineIdCounter++;
    final PolylineId polylineId = PolylineId(polylineIdVal);

    final Polyline polyline = Polyline(
      polylineId: polylineId,
      consumeTapEvents: true,
      color: Colors.black,
      width: 5,
      points: _createTripPoints(),
      onTap: () {

      },
    );

    setState(() {
      polylines[polylineId] = polyline;
    });
  }

  LatLng _createLatLng(double lat, double lng) {
    return LatLng(lat, lng);
  }

  List<LatLng> _createTripPoints() {
    final List<LatLng> points = <LatLng>[];
    points.add(_createLatLng(-8.913012, 13.202450));
    points.add(_createLatLng(-8.913297, 13.202253));
    points.add(_createLatLng(-8.913752, 13.202803));
    points.add(_createLatLng(-8.913455, 13.203063));
    return points;
  }

  DateTime selectedDate = DateTime.now();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.black,
          title: Text("Your Trips"),

        ),
        body: Column(
          children: <Widget>[
            Container(
              height: 150,
              width: double.infinity,
              child: GoogleMap(
                polylines: Set<Polyline>.of(polylines.values),
                mapType: MapType.normal,
                initialCameraPosition: _cameraPosition,
                onMapCreated: (GoogleMapController controller) {
                  _controller.complete(controller);
                },
                onTap: (LatLng location) {
                  Navigator.pushNamed(context, "/select_issue");
                },
              ),
            ),
            SizedBox(height: 20,),
            Container(
              padding: EdgeInsets.symmetric(horizontal: 20),
              child: Column(
                children: <Widget>[
                  Row(
                    children: <Widget>[
                      Text("Today at 1:05 AM", style: TextStyle(fontWeight: FontWeight.bold,)),
                      Spacer(),
                      Text("\$7.42", style: TextStyle(fontWeight: FontWeight.bold,)),
                    ],
                  ),
                  SizedBox(height: 5,),
                  Row(
                    children: <Widget>[
                      Text("Infinity G Coupe"),
                      SizedBox(width: 10,),
                      Text("ABC123", style: TextStyle(fontWeight: FontWeight.bold,))
                    ],
                  ),
                ],
              ),
            )
          ],
        )
    );
  }
}
```
Tela para visualizar as viagens feitas

## Main

`main.dart`
```
import 'package:flutter/material.dart';
import 'package:taxidriver/src/blocs/auth_bloc.dart';
import 'package:taxidriver/src/ui/pages/add_payment_method.dart';
import 'package:taxidriver/src/ui/pages/free_rides.dart';
import 'package:taxidriver/src/ui/pages/help.dart';
import 'package:taxidriver/src/ui/pages/home.dart';
import 'package:taxidriver/src/ui/pages/login.dart';
import 'package:taxidriver/src/ui//pages/add_card.dart';
import 'package:taxidriver/src/ui/pages/payment.dart';
import 'package:taxidriver/src/ui/pages/select_issue.dart';
import 'package:taxidriver/src/ui/pages/settings.dart';
import 'package:taxidriver/src/ui/pages/your_trips.dart';

void main() => runApp(MyApp(
    AuthBloc(),
    MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Uber Clone',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      initialRoute: './',
      routes: {
        '/home': (context) => MyHomePage(title: 'Taxi'),
        '/': (context) => LoginPage(),
        '/payment': (context) => PaymentPage(),
        '/add_payment': (context) => AddPaymentMethodPage(),
        '/add_card': (context) => AddCardPage(),
        '/your_trip': (context) => YourTripPage(),
        '/select_issue': (context) => SelectIssuePage(),
        '/free_rides': (context) => FreeRidesPage(),
        '/help': (context) => HelpPage(),
        '/settings': (context) => SettingsPage(),
      },
    )));

class MyApp extends InheritedWidget {
  final AuthBloc authBloc;
  final Widget child;
  MyApp(this.authBloc, this.child) : super(child: child);

  @override
  bool updateShouldNotify(InheritedWidget oldWidget) {
    return false;
  }

  static MyApp of(BuildContext context) {
    return context.inheritFromWidgetOfExactType(MyApp);
  }
}
```
Algoritmo principal que dá inicio ao app:)







