
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

