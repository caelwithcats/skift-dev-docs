# Introduction to creating GUI applications with libwidget

There are two ways of creating graphical user interfaces (GUI) applications in libwidget:

1. only with C++ code
2. with markup language (XML)

This tutorial will cover both ways and show you how to make the hello world application.

## Creating a GUI - method 1

**main.cpp**
```c++
#include <libwidget/Application.h>
#include <libwidget/Widgets.h>
#include <libwidget/dialog/Dialog.h>

int main(int argc, char **argv)
{
    application_initialize(argc, argv);

    // This is the main window
    Window *window = new Window(WINDOW_RESIZABLE);

    // The insets are the padding
    window->root()->insets(Insets(8));
    window->root()->layout(VFLOW(0));
    window->icon(Icon::get("application"));
    window->title("Hello World!");
    window->size(Vec2i(500, 400));

    // Create widgets
    new Label(window_root(window), "Hello World!", Position::CENTER);
    auto button = new Button(window_root(window), BUTTON_FILLED, "Click Me!");

    button->on(Event::ACTION, [](auto) {
         dialog_message(Icon::get("close"), "Hi", "You clicked me", DIALOG_BUTTON_OK);
    });
    window->show();

    return application_run();
}
```
**.build.mk**
```js
APPS += HELLO_WORLD

HELLO_WORLD_NAME = hello-world
HELLO_WORLD_LIBS = widget graphic json
HELLO_WORLD_ICONS = application
```
## Creating a GUI - method 2

This method involves using a markup file. This is the fastest way to build libwidget applications

**hello-world.markup**
```xml
<Window
    title="Hello World!"
    icon="application"
    width="500"
    height="400"
    layout="vflow(0)"
    padding="insets(8)"
    >
    <Label text="Hello World!" position="center"/>
    <Button id="button" text="Click Me!" filled/>
</Window>
```
**main.cpp**
```c++
#include <libwidget/Application.h>
#include <libwidget/Widgets.h>
#include <libwidget/Markup.h>
#include <libwidget/dialog/Dialog.h>

int main(int argc, char **argv)
{
    application_initialize(argc, argv);

    // Converts our markup file to a window
    Window *window = window_create_from_file("/Applications/hello-world/hello-world.markup");;
    
    // Get a pointer to the button
    Button* button = nullptr;
    if ((button = (Button*)window_get_widget_by_id(window, "button")))
    {
        button->on(Event::ACTION, [](auto) {
            dialog_message(Icon::get("close"), "Hi", "You clicked me", DIALOG_BUTTON_OK);
        });
    }
    window->show();

    return application_run();
}
```
**.build.mk**
```js
APPS += HELLO_WORLD

HELLO_WORLD_NAME = hello-world
HELLO_WORLD_LIBS = widget markup json graphic
HELLO_WORLD_ICONS = application
```
