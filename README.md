# shoppinglist

A new Flutter project.

# Assignment 7

## What are the main differences between stateless and stateful widgets in Flutter?

Stateless widgets in Flutter are immutable, meaning their properties cannot change once they are created. They do not have any internal state that can be modified. Stateless widgets are typically used for displaying static content that doesn't change based on user interactions or other factors. Because they are immutable, they are considered lightweight and can be more efficient in terms of performance. Examples of stateless widgets include Container, Text, and Icon. When you need to display information that doesn't change, using a stateless widget is a good choice. 

On the other hand, stateful widgets are mutable and can change their properties and appearance over time in response to user interactions or other factors. They have an associated State object that can be modified, and the widget can rebuild itself in response to changes in its state. Stateful widgets are used for dynamic content that can change based on user input, network requests, and other events. Examples of stateful widgets include ListView, Form, and TextField. They are essential for creating interactive and dynamic user interfaces in Flutter applications.

## Explain all widgets that you used in this assignment.

### menu.dart:

`MyHomePage` functions as the primary widget that encompasses all other widgets within the Flutter application in the `menu.dart` file. Notably, `MyHomePage` extends the `StatelessWidget` class, allowing it to describe a portion of the user interface by assembling a collection of other widgets that more precisely depict the user interface. This is particularly useful when the section of the user interface being described does not rely on anything beyond the configuration information within the object itself and the BuildContext in which the widget is inflated. Extending `StatelessWidget` also indicates that MyHomePage does not possess a state and is modified by external events or parent events in the widget tree.

The `Scaffold` widget implements the fundamental material design and visual layout structure of the Flutter application. In this application, the `Scaffold consists` of a body (housing the primary content) and an `appBar` (a fixed app bar displayed at the top). However, the `Scaffold` can also include additional elements like a drawer, `primary`, `bottomNavigationBar`, `backgroundColor`, `floatingActionButtonLocation`, and `floatingActionButton`.

The `AppBar` widget is a material design app bar typically utilized in the `Scaffold.appBar` property. This widget positions the app bar as a fixed-height component at the top of the screen. In this Flutter application, the AppBar features a title specified by the 'title' property.

The `Text` widget is placed within the 'AppBar.title' property to present the application's title, which is "Flutter Inventory" in this instance.

`SingleChildScrollView` wraps the content, enabling it to be scrollable if it surpasses the available screen space. It ensures that the content can be scrolled if it exceeds the viewport.

`Padding` is used to apply padding around its child widget, establishing space around the content.

`Column` arranges its children vertically, making it suitable for displaying a list of items in a column.

`GridView.count` generates a grid of items with a specified number of columns. It's employed to display a grid of shop items. The items list is mapped to a list of ShopCard widgets and exhibited in the grid.

`ShopItem` is a custom class that defines the properties of a shop item, including name, icon, and color.

`ShopCard` is a custom widget used to present each shop item as a card. It extends StatelessWidget and accepts a ShopItem as a parameter. The card showcases an icon, name, and responds to taps by displaying a SnackBar.

`Material` furnishes a Material Design background color and elevation to the card, as it is responsible for the shape and border. It's important to note that any alterations made to the Material widget will impact the entire child.

`InkWell` enables the card to respond to taps. When tapped, it displays a SnackBar containing the message.

### main.dart:

The `MaterialApp` widget serves as the main widget for the entire application. It encompasses all the necessary widgets and establishes the fundamental structure of the Flutter application. Additionally, note that `MaterialApp` implicitly generates a `Scaffold` as its child widget. A `Scaffold` provides a basic framework for a Flutter app, incorporating elements such as the app bar, body, and other common UI components.

`MyHomePage` is the subsequent widget encapsulating the MaterialApp widget. It is designated as the home of the MaterialApp via the 'home' property but is defined in the 'menu.dart' file of the Flutter application.

The `Title` widget employs the 'title' property to specify the title of the Flutter application. This title appears as text in the application's app bar or in the task switcher.

`ThemeData` is a widget that utilizes the 'theme' property of the MaterialApp to establish the overall theme of the application, including visual attributes, colors, and typography. Within this widget, properties like 'colorScheme' can be employed to define the app's color scheme, while 'useMaterial3' indicates the utilization of Material 3 design principles in the Flutter application.


## Explain how you implemented the checklist above step-by-step (not just following the tutorial).

- First, we designate a new folder or directory we want to initiate git in to become our github repository

- Next, after we run `git init`, we run `flutter create <APP_NAME>`. We then write `cd <APP_NAME>` then `flutter run` to come up with the barebones skeleton of our application.

- Moving on, we then modify our `main.dart` and `menu.dart` to better reflect what is needed as the specification for our PBP assignment.

- We then repeat the steps for the tutorial. We first modified the  `menu.dart` file to include the `shopcard` `MyHomePage` and `snackBar` all of which extends `StatelessWidgets`. We copy the following code.

```
class MyHomePage extends StatelessWidget {
  MyHomePage({Key? key}) : super(key: key);
  final List<ShopItem> items = [
    ShopItem("View Products", Icons.checklist, Colors.blue),
    ShopItem("Add Product", Icons.add_shopping_cart, Colors.red),
    ShopItem("Logout", Icons.logout, Colors.green),
  ];
  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  @override
    Widget build(BuildContext context) {
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
}
}
class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {Key? key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
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

- Moving on, for the `main.dart` we first `package:flutter/material.dart` and `package:shoppinglist/menu.dart`. We then import all the required libraries for the `main.dart` and run it.

- Finally, we can start our app by typing `flutter run` in terminal then pressing `2` for google chrome platform. 

# Assignment 8

## Explain the difference between Navigator.push() and Navigator.pushReplacement(), accompanied by examples of the correct usage of both methods!

In Flutter, both the `Navigator.push()` and `Navigator.pushReplacement()` methods are used to navigate between different screens (routes) in a mobile application. The primary difference lies in how they manage the navigation stack. `Navigator.push()` pushes a new screen on top of the old screen. This is beneficial since the mew screen can be seen as well as the old screen technically still being able to be seen and navigated to using a back button. This is suitable for scenarios where you want to maintain a history of screens, such as when moving from a list view to a detailed view. Here is an example:
```
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondScreen()),
);
```
On the opposite side, `Navigator.pushReplacement()` is used to replace the old screen with a new one. This would mean that the user is not able to navigate to it anymore. This is suitable for authentication screen like after logging out. The user will not be able to come back to a page they don't have acces to once they log out. Here is an example:
```
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => HomeScreen()),
);
```

## Explain each layout widget in Flutter and their respective usage contexts!
## List the form input elements you used in this assignment and explain why you used these input elements!
## How is clean architecture implemented in a Flutter application?
## Explain how you implemented the checklist above step-by-step! (not just following the tutorial)
