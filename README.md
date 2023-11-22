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

ListView:

This widget houses children displayed in a list layout, facilitating scrolling through the list of children while allowing definition of the extent of all its children for consistency. The children are presented consecutively, following their order in the list, in the direction specified by the list's scrolling (defaulting to up-to-down). It proves useful for navigating a lengthy drawer or scrolling through options like buttons.

Alignment:

This widget, featuring a singular child, can be positioned within the Alignment widget either through the use of a coordinate system with an offset or by employing predetermined alignments such as Alignment.bottomCenter. It is versatile for fitting logos or appropriately placing buttons within a specific section of a page.

GridView:

This widget organizes children in a grid layout, enabling the definition of the number of children on a row, spacing between children, padding of the grid from the edge of the GridView, and the margin around each child.

Container:

True to its name, this widget can contain other widgets, offering enhanced control over positioning and space utilization through attributes like padding, margin, and alignment. It serves well as a child of a larger widget, allowing for the encapsulation of multiple smaller children, such as a button incorporating both icon and text.

Padding:

This widget accommodates a single child while providing the ability to set EdgeInsets, determining the space between the edges of the parent class and the edges of the child class, providing control over layout.

Row:

This widget enables the grouping of children in an array, positioning each child to the right of the one preceding it. It is suitable for organizing a moderate number of similar buttons or widgets.

Column:

A widget designed for containing children in an array where each child is positioned below the one preceding it. The Column widget expands vertically as more items are added, ensuring a snug fit for every child.

Center:

A widget that centers its child, simplifying the alignment of inner widgets to the middle. This is beneficial when aiming to place an image or icon at the center of a widget or when dealing with significant blank space containing a button.


## List the form input elements you used in this assignment and explain why you used these input elements!

### Widgets Used

- Form: The form widget allows us to bunch multiple TextFormFields into one form. from here we can display, validate, save and reset the form as needed.
- TextFormField: A text field that allows users to input their responses into the form. here we can validate the response and save it as a string.

### ELEMENTS

- Name: Our store of course, needs to have items, so we will need to add the name of the item to our list.
- Price: The price also needs to be recorded in our shopping store.
- Description: so that users know what theu are getting, they need to know what the description of our object is.

## How is clean architecture implemented in a Flutter application?

Clean Architecture in Flutter involves organizing code into layers: presentation, domain, and data. The presentation layer deals with UI components and delegates most logic to the domain layer, which houses business logic independently of the framework. Data management is handled by the data layer, interacting with external sources via repositories and data sources. Following the dependency rule, dependencies flow from outer to inner layers, maintaining a clear separation of concerns. Dependency injection is used for providing dependencies, promoting flexibility and testability. By defining interfaces and abstract classes, you establish contracts between layers, enhancing maintainability and scalability. This approach supports independent testing of each layer and facilitates adaptation to evolving application requirements.

In a practical scenario, a Flutter widget (presentation layer) utilizes a use case (domain layer) for executing business logic. This use case relies on a repository (data layer) to fetch data, with the repository implementation managing the specifics of data retrieval. This modular structure ensures a maintainable and scalable Flutter application, emphasizing testability and adaptability over time.

## Explain how you implemented the checklist above step-by-step! (not just following the tutorial)

### Adding the form

To begin, I created a Dart file called 'inventory_form' to define a new page. Similar to our previous Flutter files, it imports from the "flutter/material.dart" package. In this file, I introduced a Stateful widget named "ShopFormPage," equipped with a constructor containing only "super.key", that is inherited from its parent class, and a private instance of "ShopFormPageState" as its state.

Subsequently, I outlined the state for "ShopFormPage," incorporating a private attribute named "formKey" to handle the form state along with previously listed input elements (name, category, code, and description as Strings, and amount and price as integers). Following this, I proceeded to override the "build" method within the state, incorporating specific features and contents.

Within the Form structure, there exists a Column incorporating a TextFormField for each previously mentioned input element. These TextFormFields are appropriately labeled based on the corresponding attribute. They feature an onChange method that assigns the current content of the TextFormField to the relevant attribute (e.g., the TextFormField labeled "Card Name" modifies the "name" attribute of the "ShopFormPageState"). Additionally, the TextFormFields are equipped with validators that return errors if the field is empty or if the attribute is expected to be an integer, but the TextFormField content is non-numeric.

In the column nested within the Form, serving as the body of the Scaffold constructed when building this Widget, there is an ElevatedButton. This button is encapsulated by an Align widget, strategically positioning it at the bottom center. The button is labeled 'Save,' providing a clear and actionable indication of its purpose within the form.

### Adding the drawer

to start, I made a new file called left_drawer.dart wherein I imported the necessary flutter/materials packages as well as HomePage and ShopFormPage. In this file, I made a new STATELESS WIDGET called LeftDrawer. The widget's constructor exclusively includes "super.key" without introducing any specific attributes. The overridden "build" method of this widget is designed to return a Drawer when built. Within the Drawer, a ListView is positioned as its child.

I made sure that the drawer has the necessary features needed like the add item button, homepage and an indigo drawer header. for both buttons, i used Navigation.PushReplacement() to make sure that the page is how we need it to be.

## Assignment 9

### Can we retrieve JSON data without creating a model first? If yes, is it better than creating a model before retrieving JSON data?

While it is technically possible to retrieve JSON data in Flutter without creating a specific model first, doing so comes with trade-offs. Without a predefined model, the code lacks the benefits of static typing, making it susceptible to runtime errors if the JSON structure changes unexpectedly. This approach might be suitable for quick prototyping or scenarios where the JSON data is simple and doesn't require a formal structure. However, for more complex applications, creating a dedicated model class offers advantages in terms of type safety, code readability, and maintainability.

Creating a model class allows you to define a structured representation of the JSON data, providing a clear contract between your Dart code and the expected data format. This enhances code organization and readability, making it easier for developers to understand and work with the data. Additionally, tools like `json_serializable` automate the serialization/deserialization process, reducing boilerplate code and ensuring that the Dart model aligns seamlessly with the JSON structure. Overall, while fetching JSON data without a model may be feasible in certain scenarios, employing models is generally considered a best practice for robust and maintainable Flutter applications.

### Explain the function of CookieRequest and explain why a CookieRequest instance needs to be shared with all components in a Flutter application.


The `CookieRequest` class, part of the `pbp_django_auth` package, serves as a tool for managing authentication-related tasks in our Flutter application, specifically handling `login`, `logout`, and `HTTP` requests involving cookies. This class is responsible for managing the necessary cookies or tokens required for authentication with the Django backend server. To ensure a unified authentication state across the application, a `CookieRequest` instance should be shared with all components using a Provider in Flutter. This sharing mechanism guarantees that changes in login status, user data, and cookies are consistently reflected throughout the application. By centralizing authentication through a shared `CookieRequest` instance, the approach enhances code efficiency, reduces redundancy, and streamlines the user experience by facilitating easy tracking of cookies/tokens in a centralized manner.

### Explain the mechanism of fetching data from JSON until it can be displayed on Flutter.

In the Flutter application, after fetching and parsing the JSON data, you can use Flutter widgets to display the information. If you have a list of items, you might use a `ListView.builder` to efficiently build a scrolling list. For example, if your JSON data represents a list of user profiles, you could iterate through the list and create a widget for each user, displaying their name, age, or any other relevant information. If you are dealing with a single object, you can directly access its properties and use them to populate Text or other widgets. For instance, you might display a user's name and age in a simple `Column` or `Row widget.

Furthermore, you can incorporate state management solutions like `Provider` or `Bloc` to efficiently update the UI when the data changes. These patterns help in separating the UI from the data and managing the app's state in a more organized manner. By following these steps, you ensure that the JSON data is seamlessly integrated into your Flutter application, providing a dynamic and responsive user interface.

### Explain the authentication mechanism from entering account data on Flutter to Django authentication completion and the display of menus on Flutter.

The `authentication` process between Flutter and Django involves a sequence of steps for secure user account data management and authentication, leading to the display of menus within the Flutter application. When users enter their account details in the Flutter app, the application communicates with the Django backend through a POST request, transmitting the credentials for user authentication.

In the Django backend, authentication includes verifying the provided username and password against stored user data, employing features like password hashing and salting for security. Upon successful authentication, the Django server generates an authentication token or establishes a session to track the user's authenticated status. The server then sends a response back to the Flutter app, conveying the outcome of the authentication attempt, including additional user data or an authentication token if successful, or an error message if authentication fails.

Upon receiving the authentication response, the Flutter app adjusts its local state accordingly. Successful authentication leads to a transition to a menu display page through Flutter's navigation system, presenting various menus or features accessible to the authenticated user. Throughout this process, the implementation of secure communication practices, such as `HTTPS`, is crucial for data transmission security. Effective error handling and user feedback mechanisms ensure a seamless user experience, with error messages displayed when authentication encounters issues. The authentication mechanism orchestrates a coordinated data exchange between Flutter and Django, prioritizing the security and integrity of user account information.

### List all the widgets you used in this assignment and explain their respective functions.

-Provider

This widget is the one that is available in the `provider` package that is useful for knowing what the current state is. This is used to keep data to be used by `child` widgets. It allows for inheriting properties down to `child` widgets.

- CookieRequest

This is provided by the TAs in the `PBP` package. It allows us to store certain cookies that would be used to integrate with the Django assignment. 

- FutureBuilder

A wisget that enables the handling of asynchronous functions, such as data retrieval, by designating the function for the  future. It captures snapshots of the latest interaction with the function and utilizes them to construct or reconstruct the webpage. In this scenario, the snapshots encompass all items extracted from the response to the fetch request made to the Django project.

- Gridview.Builder

Similar to `GridView.count`, but this has a dynamic number of children that is able to change count of.

- detail.dart

This is the page that shows in depth details of objects in the `shoplist.dart`. It has all the fields associated with the Django assignment, namely, `name`, `price`, and `description`.
  
### Explain how you implement the checklist above step by step! (not just following the tutorial).

**Ensure the deployment of the Django assignment is running smoothly.**

Currently it is not running smoothly, however I have expressed all my concerns to the TA and together, we are currently looking for a solution to fix it. There was a problem with a git folder with a white arrow howeverm I fixed it by running some scripts then pushing again.

**Creating the login page in FLutter and integrating it with Django Assignment**

First off, within my Django Project, I incorporated an app named `corsheaders`. I configured the `settings.py` file to recognize it as an installed app by adding it into `INSTALLED_APPS`, I then included its associated middleware in the `Middleware` list in settings.py, and added all the necessary constants for `corsheaders` to function according to the requirements in `settings.py`. Subsequently, I established an `authentication` app using the command `python manage.py startapp authentication`. In this app, I defined `login` and `logout` functions that operate similarly to those in the previous assignments, with the distinction that they interpret the request differently now, they interpret requests as `request.POST['data']`. Instead of returning an `HttpResponseRedirect`, they now return a `JSONResponse` containing all the information required by our Flutter app, such as the success status, message, and the username of the user in the case of a successful login. Tehn, in the `authentication` application, I created a `urls.py` file, set up routing paths in   `urls.py` to the functions in the views.py of the authentication app, and added a path that includes the authentication   `urls.py` in the project directory.

Moving on to a new file named `login.dart`, I crafted a stateful widget called `LoginApp`, with an instance of `_LoginPageState` as its state. The `_LoginPageState` widget includes final (unchanging) variables of type TextEditingController to track the contents of the TextFields where users input their data, namely _usernameController and _passwordController. Additionally, within the build function, there is a request variable of the CookieRequest class, which tracks cookies and enables sending HTTP requests to our Django project.

In the `_LoginPageState` widget, We override the Build method. On build, it creates a `Scaffold` with an `Appbar`, and its body, which is the main body visible on the webpage, is a Container (used for padding) with a child of the Column class (used for positioning and storing a list of children widgets displayed below one another). The Column class includes the following children:

- `TextField` with `_usernameController` as its controller and InputDecoration indicating that this field is for "Username."
- A `TextField` with `_passwordController` as its controller and InputDecoration stating that this field is for "Password."
- An `ElevatedButton` with the text "Login" that, when clicked, fetches the contents of the text fields by accessing the text attribute of the controllers. It then awaits a request to the Django project using the request CookieRequest, routed to the login function in the `authentication` app, which attempts to log in to the application. If successful, some session data is stored in the request `CookieRequest`, and the user is navigated to the HomePage of the app.

Essentially what the login does is after integrating with django, the process of logging in occurs in the Django app within `authentication`. The flutter app acts as a frontend and to display to the user responses gotten from the Django app.

**Create a custom model according to your Django application project.**

I first ran `localhost:8000/json` that displays the serialised version of JSON that is in my `Django` project. I then went onto https://app.QuickType.io. i then copy pasted the JSON response I got into the site to get the necessary code to put in JSON. I then made a new folder in `lib` called `models` and there added a .dart file called `product.dart` I then copy pasted it into the models and did not change any fields since all the fields necessary are the same as my Django file.

**Create a page containing a list of all items available at the JSON endpoint in Django that you have deployed.**

In a new file called `list_product.dart`, I create a StatefulWidget named ItemPage, assigning an instance of `_ProductPageState` as its state. Subsequently, I define the `ProductPageState`, incorporating a Future List of Items that gets updated by the outcome of an asynchronous function named fetchData. This fetchData function utilizes the request CookieRequest to dispatch a request to the Django Project, intending it to be routed to the `show_json` function, and extracts the `JSON` from the response. For each item within the `JSON`, the function employs the serialization logic derived from the Item model to transform the JSON into an object of type Item. Subsequently, the item is added to a list. The fetchData function concludes by returning this list.

**Create a detail page for each item listed on the Item list page.**

I made a new file called `detail.dart`, there, I added the following code:

```
import 'package:flutter/material.dart';
import 'package:shoppinglist/models/product.dart';
import 'package:shoppinglist/widgets/left_drawer.dart';

class ProductDetailPage extends StatelessWidget {
  final Product product;

  const ProductDetailPage({Key? key, required this.product}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('product Details'),
        backgroundColor: Colors.indigo,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              product.fields.name,
              style: const TextStyle(
                fontSize: 24.0,
                fontWeight: FontWeight.bold,
              ),
            ),
            const SizedBox(height: 10),
            Text("Price: ${product.fields.price}"),
            const SizedBox(height: 10),
            Text("Description: ${product.fields.description}"),
            const SizedBox(height: 10),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(
                    context); // Navigate back to the product list page
              },
              child: const Text('Back to product List'),
            ),
          ],
        ),
      ),
    );
  }
}
```
There are some notable things to take note of.

```
children: [
            Text(
              product.fields.name,
              style: const TextStyle(
                fontSize: 24.0,
                fontWeight: FontWeight.bold,
              ),
            ),
            const SizedBox(height: 10),
            Text("Price: ${product.fields.price}"),
            const SizedBox(height: 10),
            Text("Description: ${product.fields.description}"),
            const SizedBox(height: 10),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(
                    context); // Navigate back to the product list page
              },
              child: const Text('Back to product List'),
            ),
```
This is basically the contents of the site where It displays the necessary fields `name`, `price` and `description` as well as an `ElevatedButton` to bring me back to the `list_product.dart` page.

In `list_product.dart`, we add the following code:

```
InkWell(
                          onTap: () {
                            Navigator.push(
                                context,
                                MaterialPageRoute(
                                    builder: (context) => ProductDetailPage(
                                        product: snapshot.data![index])));
                          },
```
Here, we add an `InkWell` that has an `onTap` function. For the function, we push the `ProductDetailPage` to be shown to the user.

***Bonus 1* Showing list only for that specific user**

To do this, the steps are simple.

In the Django app, we modify the `show_json` function in `main/views` as such:

```
def show_json(request):
    data = Product.objects.filter(user=request.user)
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
```
Here we send JSON files based on the id of the user so it is only their items that get sent.

Next in Flutter, we modify `shoplist_form.dart` as such:

```
Future<List<Product>> fetchProduct() async {
    final request = context.watch<CookieRequest>();
    // TODO: Change the URL to your Django app's URL. Don't forget to add the trailing slash (/) if needed.
    var url = Uri.parse('http://127.0.0.1:8000/json/');
    var response = await http.get(
      url,
      headers: {"Content-Type": "application/json"},
    );

    // decode the response to JSON
    // var data = jsonDecode(utf8.decode(response.bodyBytes));

    final data = await request.get('http://127.0.0.1:8000/json/');

    // convert the JSON to Product object
    List<Product> list_product = [];
    for (var d in data) {
      if (d != null) {
        list_product.add(Product.fromJson(d));
      }
    }
    return list_product;
  }
```

We create a `Future` that will differ based on the number of items a user has. It waits for response from the django's json represented by `data`. for each item, it will make a card. 

Don't forget to add the necessary imports at the top of the file.

```
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';
```

