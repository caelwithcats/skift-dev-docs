# Introduction to creating GUI applications with libwidget

There is two ways of creating applications with a user interface in libwidget:

1. fully with code
2. with markup language (XML)

This tutorial will cover both ways and show you how to make the hello world application.

## Creating a GUI - method 1

**main.cpp**
```c++
#include <libwidget/Application.h>
#include <libwidget/Widgets.h>

int main(int argc, char **argv)
{
    application_initialize(argc, argv);

    // This is the main window
    Window *window = window_create(WINDOW_RESIZABLE);

    window_set_icon(window, Icon::get("application"));
    window_set_title(window, "Hello World!");
    window_set_size(window, Vec2i(500, 400));

    // Create widgets
    new Label(window_root(window), "Hello World!", Position::CENTER);
    auto button = new Button(window_root(window), BUTTON_TEXT, "Click Me!");
    
    button->on(Event::ACTION, [](auto) {
         dialog_message(Icon::get("close"), "Hi", "You clicked me", DIALOG_BUTTON_OK);
    });
    return 0;
}
```
**.build.mk**
```
APPS += HELLO_WORLD

HELLO_WORLD_NAME = hello-world
HELLO_WORLD_LIBS = widget graphic json
HELLO_WORLD_ICONS = application
```
## Creating a GUI - method 2
unfinished
