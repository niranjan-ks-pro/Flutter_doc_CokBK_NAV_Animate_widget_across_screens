# Flutter_doc_CokBK_NAV_Animate_widget_across_screens
 https://euangoddard.github.io/clipboard2markdown/
Animate a widget across screens
===============================

1.  [Cookbook](https://docs.flutter.dev/cookbook)
2.  [Navigation](https://docs.flutter.dev/cookbook/navigation)
3.  [Animate a widget across screens](https://docs.flutter.dev/cookbook/navigation/hero-animations)

It's often helpful to guide users through an app as they navigate from screen to screen. A common technique to lead users through an app is to animate a widget from one screen to the next. This creates a visual anchor connecting the two screens.

Use the [`Hero`](https://api.flutter.dev/flutter/widgets/Hero-class.html) widget to animate a widget from one screen to the next. This recipe uses the following steps:

1.  Create two screens showing the same image.
2.  Add a `Hero` widget to the first screen.
3.  Add a `Hero` widget to the second screen.

[](https://docs.flutter.dev/cookbook/navigation/hero-animations#1-create-two-screens-showing-the-same-image)1\. Create two screens showing the same image
---------------------------------------------------------------------------------------------------------------------------------------------------------

In this example, display the same image on both screens. Animate the image from the first screen to the second screen when the user taps the image. For now, create the visual structure; handle animations in the next steps.

info Note: This example builds upon the [Navigate to a new screen and back](https://docs.flutter.dev/cookbook/navigation/navigation-basics) and [Handle taps](https://docs.flutter.dev/cookbook/gestures/handling-taps) recipes.

content_copy

```
import 'package:flutter/material.dart';

class MainScreen extends StatelessWidget {
  const MainScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Main Screen'),
      ),
      body: GestureDetector(
        onTap: () {
          Navigator.push(context, MaterialPageRoute(builder: (context) {
            return const DetailScreen();
          }));
        },
        child: Image.network(
          'https://picsum.photos/250?image=9',
        ),
      ),
    );
  }
}

class DetailScreen extends StatelessWidget {
  const DetailScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: GestureDetector(
        onTap: () {
          Navigator.pop(context);
        },
        child: Center(
          child: Image.network(
            'https://picsum.photos/250?image=9',
          ),
        ),
      ),
    );
  }
}
```

[](https://docs.flutter.dev/cookbook/navigation/hero-animations#2-add-a-hero-widget-to-the-first-screen)2\. Add a `Hero` widget to the first screen
---------------------------------------------------------------------------------------------------------------------------------------------------

To connect the two screens together with an animation, wrap the `Image` widget on both screens in a `Hero` widget. The `Hero` widget requires two arguments:

`tag`

An object that identifies the `Hero`. It must be the same on both screens.

`child`

The widget to animate across screens.

content_copy

```
Hero(
  tag: 'imageHero',
  child: Image.network(
    'https://picsum.photos/250?image=9',
  ),
)
```

[](https://docs.flutter.dev/cookbook/navigation/hero-animations#3-add-a-hero-widget-to-the-second-screen)3\. Add a `Hero` widget to the second screen
-----------------------------------------------------------------------------------------------------------------------------------------------------

To complete the connection with the first screen, wrap the `Image` on the second screen with a `Hero` widget that has the same `tag` as the `Hero` in the first screen.

After applying the `Hero` widget to the second screen, the animation between screens just works.

content_copy

```
Hero(
  tag: 'imageHero',
  child: Image.network(
    'https://picsum.photos/250?image=9',
  ),
)
```

info
