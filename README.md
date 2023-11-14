
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

