<details>
<summary> Assignment 7 </summary>

# Assignment 7
## Muhammad Obin Mandalika - 2206046771

## What are the main differences between stateless and stateful widget in Flutter?

Stateless widgets are immutable, meaning their properties (also known as "widget parameters") are set when the widget is created and cannot be changed during the widget's lifetime.Stateless widgets do not have internal mutable state. They rely solely on the data provided as input and, when the input data changes, they rebuild their UI accordingly.

Stateful widgets, as the name suggests, can maintain mutable internal state. They have a mutable State object associated with them that can change over time. Stateful widgets consist of two classes: the StatefulWidget class, which is immutable, and the State class, which is mutable. The State class is responsible for managing the widget's mutable state.

## Widgets used

MyHomePage class:

- This class represents the main page of the app.
- Scaffold widget is used as the main structure for the page. It provides an app bar and body content.
- AppBar widget is used to display the app bar at the top of the screen with a title.
- SingleChildScrollView is a scrollable wrapper for the body content.
- Column is used to arrange child widgets vertically.
Padding widget:

- Padding is used to add padding around its child widget.
- It wraps the Column to create spacing around its content.
GridView.count widget:

- This widget creates a grid of cards for the shop items. It uses a grid layout with three columns.
ShopItem objects are mapped to ShopCard widgets and displayed within the grid.
ShopItem class:

This class defines a data structure for shop items with a name and an associated icon.
ShopCard class:

- This class represents a card widget for a shop item. It's a custom widget that displays an icon and a name.
- Material is used as a background material design element with an indigo color.
- InkWell is used to provide a responsive touch area for the card and trigger actions when tapped.
- Icon widget displays the item's associated icon.
- Text widget displays the item's name.

## Step-by-step tutorial

- Create a file `menu.dart` in the kollektiv/lib directory. And import the following package : 

```
import 'package:flutter/material.dart';
import 'package:shopping_list/menu.dart';
```

- in `menu.dart`, convert the menu page to a stateless widget.

- Add text and cards, to do that you can start defining the type :

```
class ShopItem {
  final String name;
  final IconData icon;

  ShopItem(this.name, this.icon);
}
```

- Add the items for sale :

```
final List<ShopItem> items = [
    ShopItem("View Products, Icons.checklist),
    ShopItem("Add Product", Icons.add_shopping_cart),
    ShopItem("Logout", Icons.logout),
];
```

- Add the Scaffold widget inside the `Widget build` method :

```
return Scaffold(
  appBar: AppBar(
    title: const Text(
      'Shopping List',
    ),
  ),
  body: SingleChildScrollView(
    // Scrolling wrapper widget
    child: Padding(
      padding: const EdgeInsets.all(10.0), // Set padding for the page
      child: Column(
        // Widget to display children vertically
        children: <Widget>[
          const Padding(
            padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
            // Text widget to display text with center alignment and appropriate style
            child: Text(
              'PBP Shop', // Text indicating the shop name
              textAlign: TextAlign.center,
              style: TextStyle(
                fontSize: 30,
                fontWeight: FontWeight.bold,
              ),
            ),
          ),
          // Grid layout
          GridView.count(
            // Container for our cards.
            primary: true,
            padding: const EdgeInsets.all(20),
            crossAxisSpacing: 10,
            mainAxisSpacing: 10,
            crossAxisCount: 3,
            shrinkWrap: true,
            children: items.map((ShopItem item) {
              // Iteration for each item
              return ShopCard(item);
            }).toList(),
          ),
        ],
      ),
    ),
  ),
);
```

- Create a new stateless widget to display the card

```
class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {Key? key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: Colors.indigo,
      child: InkWell(
        // Responsive touch area
        onTap: () {
          // Show a SnackBar when clicked
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("You pressed the ${item.name} button!")));
        },
        child: Container(
          // Container to hold Icon and Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

## BONUS

- To change the color of each button, we would need to define a new type:

```
class ShopItem {
  final String name;
  final IconData icon;
  final Color color;

  ShopItem(this.name, this.icon, this.color);
}
```

- Change the color under the material to `item.color`

```
...
override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
...
```

- Add your prefered color for the button

```
final List<ShopItem> items = [
    ShopItem("View Items", Icons.checklist, Colors.blue),
    ShopItem("Add Item", Icons.add_shopping_cart, Colors.black),
    ShopItem("Logout", Icons.logout, Colors.yellow),
    ];
```
</details>

<details>
<summary> Assignment 8 </summary>

# Assignment 8

## Explain the difference between `Navigator.push()` and `Navigator.pushReplacement()`, accompanied by examples of the correct usage of both methods!

`Navigator.push()` is used to push a new route onto the navigator's stack, adding it on top of the existing routes. `Navigator.pushReplacement()` is used to push a new route onto the navigator's stack while replacing the current route with the new one.

## Explain each layout widget in Flutter and their respective usage contexts!

- `Align`
A widget that aligns its child within itself and optionally sizes itself based on the child's size.

- `AspectRatio`
A widget that attempts to size the child to a specific aspect ratio.

- `Baseline`
Container that positions its child according to the child's baseline.

- `Center`
Alignment block that centers its child within itself.

- `ConstrainedBox`
A widget that imposes additional constraints on its child.

- `Container`
A convenience widget that combines common painting, positioning, and sizing widgets.

- `CustomSingleChildLayout`
A widget that defers the layout of its single child to a delegate.

- `Expanded`
A widget that expands a child of a Row, Column, or Flex.

- `FittedBox`
Scales and positions its child within itself according to fit.
FractionallySizedBox
A widget that sizes its child to a fraction of the total available space. For more details about the layout algorithm, see RenderFractionallySizedOverflowBox.

- `IntrinsicHeight`
A widget that sizes its child to the child's intrinsic height.

- `IntrinsicWidth`
A widget that sizes its child to the child's intrinsic width.

- `LimitedBox`
A box that limits its size only when it's unconstrained.

- `Offstage`
A widget that lays the child out as if it was in the tree, but without painting anything, without making the child available for hit...

- `OverflowBox`
A widget that imposes different constraints on its child than it gets from its parent, possibly allowing the child to overflow the parent.

- `Padding`
A widget that insets its child by the given padding.

- `SizedBox`
A box with a specified size. If given a child, this widget forces its child to have a specific width and/or height 

- `SizedOverflowBox`
A widget that is a specific size but passes its original constraints through to its child, which will probably overflow.

- `Transform`
A widget that applies a transformation before painting its child.

- `Column`
Layout a list of child widgets in the vertical direction.

- `CustomMultiChildLayout`
A widget that uses a delegate to size and position multiple children.

- `Flow`
A widget that implements the flow layout algorithm.

- `GridView`
A grid list consists of a repeated pattern of cells arrayed in a vertical and horizontal layout. The GridView widget implements this component.

- `IndexedStack`
A Stack that shows a single child from a list of children.

- `LayoutBuilder`
Builds a widget tree that can depend on the parent widget's size.

- `ListBody`
A widget that arranges its children sequentially along a given axis, forcing them to the dimension of the parent in the other axis.

- `ListView`
A scrollable, linear list of widgets. ListView is the most commonly used scrolling widget. It displays its children one after another in the scroll direction....

- `Row`
Layout a list of child widgets in the horizontal direction.

- `Stack`
This class is useful if you want to overlap several children in a simple way, for example having some text and an image, overlaid with...

- `Table`
Displays child widgets in rows and columns.

- `Wrap`
A widget that displays its children in multiple horizontal or vertical runs.


## List the form input elements you used in this assignment and explain why you used these input elements!

`TextFormField` is a Flutter widget that combines the functionalities of a `TextField` with a Form field. It's part of the Flutter framework's material library, and it's commonly used for collecting text-based input from the user. `TextFormField`simplifies the process of managing and validating user input, especially within a Form widget.

## How is clean architecture implemented in a Flutter application?

Clean Architecture is a software design philosophy that promotes separation of concerns and independence of frameworks. It is not tied to any specific programming language or framework, but its principles can be applied to Flutter as well. Implementing Clean Architecture in a Flutter application involves organizing your codebase into distinct layers with well-defined responsibilities.

## Step by step explanation

1. Create a page for adding a new item

Create a new file called `item_form.dart` in the `lib` directory and add the `Scaffold` widget replacing the `Placeholder` widget. Create a new variable named `_formKey` and add it to the `key` attribute of the `Form` widget. Create a `TextFormField` widget wrapped in `Padding` as one of the children of the `Column`. Then, add the `crossAxisAlignment` attribute to control the alignment of the Column's children. Create a button as the next child of the `Column`. Wrap the button with Padding and Align.

2. Create a drawer

Create a new file called `left_drawer.dart`. Using the `Drawer` widget, create a drawer `ListView` that has `ListTile` for routing to `MyHomePage()` and `ShopFormPage()`.

3. Edit the home page

Create a new file called `item_card.dart`. For each card, we add a special condition if `item.name == Add Item` it will redirect the user to the add item page. in `menu.dart` add `LeftDrawer` widget in the scaffold widget.

</details>

<details>

<summary> Assignment 9 </summary>

# Assignment 9

## Can we retrieve JSON data without creating a model first? If yes, is it better than creating a model before retrieving JSON data?

For basic JSON data retrieval and manipulation tasks, you don't necessarily need to create a model. Using programming language features or libraries for working with JSON may be sufficient. 


## Explain the function of CookieRequest and explain why a CookieRequest instance needs to be shared with all components in a Flutter application.

CookieRequest is a class that represents a request for a cookie. It is used to retrieve a cookie from the server. A CookieRequest instance needs to be shared with all components in a Flutter application because it is used to retrieve a cookie from the server.

##  Explain the mechanism of fetching data from JSON until it can be displayed on Flutter.

To fetch and display JSON data in a Flutter application, start by making an HTTP request using the http package to a server. Parse the received JSON data with the dart:convert library, and model the data using Dart classes that represent the JSON structure. Deserialize the JSON into Dart objects, then utilize Flutter widgets to present the data in the user interface. Manage the widget's state to handle loading and error states, employing tools like FutureBuilder for asynchronous operations. This process ensures a structured flow from data retrieval to UI rendering, allowing for efficient integration of JSON data into a Flutter app.



## Explain the authentication mechanism from entering account data on Flutter to Django authentication completion and the display of menus on Flutter.

## Widgets used in this assignment and explain their respective functions.

- FutureBuilder widget is used to build a widget based on the state of a Future. It takes a future parameter which is of type Future. It has a builder parameter which is of type AsyncWidgetBuilder. It is used to build a widget based on the state of a Future.

- ListView widget is used to display its children in a scrollable list layout. It takes a children parameter which is of type List. It has multiple children which are displayed in a scrollable list layout. It is used to display its children in a scrollable list layout.

- GestureDetector widget is used to detect gestures on its child widget. It takes a child parameter which is of type Widget. It has a single child which is used to detect gestures. It is used to detect gestures on its child widget.

- TextFormField widget is used to create a text field. It takes a controller parameter which is of type TextEditingController. It is used to create a text field.

- ElevatedButton widget is used to create a button. It takes a child parameter which is of type Widget. It is used to create a button.

- Container widget is used to contain a child widget with some specific styling properties. It takes a child parameter which is of type Widget. It has a single child which is contained within the container. It is used to contain a child widget with some specific styling properties.

## Step by step explanation

Update the Django project by putting `django-cors-headers` into `requirements.txt`. Add corsheaders to INSTALLED_APPS and `corsheaders.middleware.CorsMiddleware` to MIDDLEWARE in `settings.py`. We also add

```
CORS_ALLOW_ALL_ORIGINS = True
CORS_ALLOW_CREDENTIALS = True
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SAMESITE = 'None'
SESSION_COOKIE_SAMESITE = 'None'
```

In `settings.py`, we add `provider` and `pbp_django_auth` packages in order to create a login page. In the django app, we create a new app called `authentication` and create the routing for that app. In `views.py` in `authentication`, we add :

```
@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Successful login status.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login successful!"
                # Add other data if you want to send data to Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login failed, account disabled."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login failed, check email or password again."
        }, status=401)
```

Create a new file called `login.dart` inside `screens` and add :

```
import 'package:kollektiv/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

void main() {
    runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
const LoginApp({super.key});

@override
Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Login',
        theme: ThemeData(
            primarySwatch: Colors.blue,
    ),
    home: const LoginPage(),
    );
    }
}

class LoginPage extends StatefulWidget {
    const LoginPage({super.key});

    @override
    _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
    final TextEditingController _usernameController = TextEditingController();
    final TextEditingController _passwordController = TextEditingController();

    @override
    Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
            appBar: AppBar(
                title: const Text('Login'),
            ),
            body: Container(
                padding: const EdgeInsets.all(16.0),
                child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                        TextField(
                            controller: _usernameController,
                            decoration: const InputDecoration(
                                labelText: 'Username',
                            ),
                        ),
                        const SizedBox(height: 12.0),
                        TextField(
                            controller: _passwordController,
                            decoration: const InputDecoration(
                                labelText: 'Password',
                            ),
                            obscureText: true,
                        ),
                        const SizedBox(height: 24.0),
                        ElevatedButton(
                            onPressed: () async {
                                String username = _usernameController.text;
                                String password = _passwordController.text;

                                // Check credentials
                                // TODO: Change the URL and don't forget to add a trailing slash (/) at the end of the URL!
                                // To connect the Android emulator to Django on localhost,
                                // use the URL http://10.0.2.2/
                                final response = await request.login("http://127.0.0.1:8000/auth/login/", {
                                'username': username,
                                'password': password,
                                });

                                if (request.loggedIn) {
                                    String message = response['message'];
                                    String uname = response['username'];
                                    Navigator.pushReplacement(
                                        context,
                                        MaterialPageRoute(builder: (context) => MyHomePage()),
                                    );
                                    ScaffoldMessenger.of(context)
                                        ..hideCurrentSnackBar()
                                        ..showSnackBar(
                                            SnackBar(content: Text("$message Welcome, $uname.")));
                                    } else {
                                    showDialog(
                                        context: context,
                                        builder: (context) => AlertDialog(
                                            title: const Text('Login Failed'),
                                            content:
                                                Text(response['message']),
                                            actions: [
                                                TextButton(
                                                    child: const Text('OK'),
                                                    onPressed: () {
                                                        Navigator.pop(context);
                                                    },
                                                ),
                                            ],
                                        ),
                                    );
                                }
                            },
                            child: const Text('Login'),
                        ),
                    ],
                ),
            ),
        );
    }
}
```

Modify the `MyApp` class in `main.dart` in order to integrate the auth system with the flutter project.

```
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Provider(
      create: (_) {
        CookieRequest request = CookieRequest();
        return request;
      },
      child: MaterialApp(
          title: 'Flutter App',
          theme: ThemeData(
            colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
            useMaterial3: true,
          ),
          home: LoginPage()),
    );
  }
}
```

Create a new file called `product.dart` inside `models` and add :

```
// To parse this JSON data, do
//
//     final product = productFromJson(jsonString);

import 'dart:convert';

List<Product> productFromJson(String str) => List<Product>.from(json.decode(str).map((x) => Product.fromJson(x)));

String productToJson(List<Product> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class Product {
    String model;
    int pk;
    Fields fields;

    Product({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory Product.fromJson(Map<String, dynamic> json) => Product(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
    };
}

class Fields {
    int user;
    String name;
    int amount;
    DateTime dateAdded;
    int price;
    String description;

    Fields({
        required this.user,
        required this.name,
        required this.amount,
        required this.dateAdded,
        required this.price,
        required this.description,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        user: json["user"],
        name: json["name"],
        amount: json["amount"],
        dateAdded: DateTime.parse(json["date_added"]),
        price: json["price"],
        description: json["description"],
    );

    Map<String, dynamic> toJson() => {
        "user": user,
        "name": name,
        "amount": amount,
        "date_added": "${dateAdded.year.toString().padLeft(4, '0')}-${dateAdded.month.toString().padLeft(2, '0')}-${dateAdded.day.toString().padLeft(2, '0')}",
        "price": price,
        "description": description,
    };
}

```

Create a new file called `list_product.dart` in `screens` and add :

```
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'package:kollektiv/models/product.dart';
import 'package:kollektiv/widgets/left_drawer.dart';

class ProductPage extends StatefulWidget {
  const ProductPage({Key? key}) : super(key: key);

  @override
  _ProductPageState createState() => _ProductPageState();
}

class _ProductPageState extends State<ProductPage> {
  Future<List<Product>> fetchProduct() async {
    var url = Uri.parse('http://127.0.0.1:8000/json/');
    var response = await http.get(
      url,
      headers: {"Content-Type": "application/json"},
    );

    // decode the response to JSON
    var data = jsonDecode(utf8.decode(response.bodyBytes));

    // convert the JSON to Product object
    List<Product> list_product = [];
    for (var d in data) {
      if (d != null) {
        list_product.add(Product.fromJson(d));
      }
    }
    return list_product;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Text('Product'),
        ),
        drawer: const LeftDrawer(),
        body: FutureBuilder(
            future: fetchProduct(),
            builder: (context, AsyncSnapshot snapshot) {
              if (snapshot.data == null) {
                return const Center(child: CircularProgressIndicator());
              } else {
                if (!snapshot.hasData) {
                  return const Column(
                    children: [
                      Text(
                        "No product data available.",
                        style:
                            TextStyle(color: Color(0xff59A5D8), fontSize: 20),
                      ),
                      SizedBox(height: 8),
                    ],
                  );
                } else {
                  return ListView.builder(
                      itemCount: snapshot.data!.length,
                      itemBuilder: (_, index) => Container(
                            margin: const EdgeInsets.symmetric(
                                horizontal: 16, vertical: 12),
                            padding: const EdgeInsets.all(20.0),
                            child: Column(
                              mainAxisAlignment: MainAxisAlignment.start,
                              crossAxisAlignment: CrossAxisAlignment.start,
                              children: [
                                Text(
                                  "${snapshot.data![index].fields.name}",
                                  style: const TextStyle(
                                    fontSize: 18.0,
                                    fontWeight: FontWeight.bold,
                                  ),
                                ),
                                const SizedBox(height: 10),
                                Text("${snapshot.data![index].fields.price}"),
                                const SizedBox(height: 10),
                                Text(
                                    "${snapshot.data![index].fields.description}")
                              ],
                            ),
                          ));
                }
              }
            }));
  }
}

```




</details>