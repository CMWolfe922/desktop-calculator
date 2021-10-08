`#!/usr/bin/pyqtenv python3`

# PyQt5: Notes and Examples of How to Use PyQt5


```sh
"""Creating a simple Hellp World example using PyQt5"""

import sys
```

```sh
# TODO: 1. Import `QApplication` and all the required widgets

from PyQt5.QtWidgets import QApplication as qapp
from PyQt5.QtWidgets import QLabel
from PyQt5.QtWidgets import QWidget
```


- First you import sys , which will allow you to hndle the exit status of the applicationn. Then, you import QApplication, QWidget, and QLabel from QtWidgets, which is part of the package called PyQt5


```sh
# TODO: 2. Create an instance of QApplication
app = qapp(sys.argv)
```


- The reason you create app (QApplication) instance before everything else is because app Object does A LOT of initialization. This is why creating it before creating any other object related to the GUI is best. Also, app object deals with command line arguments, so you also have to pass sys.argv as an argument when creating app

>NOTE: sys.argv contains the list of command-line arguments passed into a Python script. If Im not going to be using any command line args then I can pass in an empty list instead. EXAMPLE: app([])


```sh
# TODO: 3. Create an instance of the application's GUI
"""In step 3 I will create the apps gui. The GUI will be based on the QWidget
which is the base class of all user interface objects in PyQt"""

window = QWidget()
window.setWindowTitle('PyQt5 App')
window.setGeometry(100, 100, 280, 80)
window.move(60, 15)
helloMsg = QLabel('<h1>Hello World!</h1>', parent=window)
helloMsg.move(60, 15)
```
- `Window` is an instance of `QWidget`. Provides all features to create app window or form
- `setWindowTitle` gives app window a name/title
- `.setGeometry` defines window size, where to place on screen. It takes four args. First two: (x and y coordinates for on screen placement) Next two args (width and height of app window) Example: (200, 200, 200, 80)
- Like all GUI's they need widgets. Here we use QLabel object for (helloMsg) This shows Hello, World!. QLabel objects can accept HTML elements like `'<h1>Hello, World!</h1>'` to format textas an h1 header.
- Lastly, use `move()` to place helloMsg at the coordinates 60, 15 on the apps window


>__NOTE:__ Note: In PyQt5, you can use any widget (a subclass of `QWidget`) as a top-level window, or even a button or a label. The only condition is that you pass no parent to it. When you use a widget like this, PyQt5 automatically gives it a title bar and turns it into a normal window.

### The parent-child relationship is used for two complementary purposes:
    > 1. A widget that doesn’t have a parent is a main window or a top-level window.

    > 2. A widget that has a parent (which is always another widget) is contained (or shown) within its parent.

- This relationship __also__ __defines__ ownership, with __parents owning their children.__ The _PyQt5 ownership model_ __ensures__ that _if you delete a parent_ (for example, __a top-level window__), then __all of its children (widgets) are automatically deleted__ as well.
    - To avoid memory leaks, you should __always__ make sure that any `QWidget` object has a parent, with the _sole exception of top-level windows_.

- Last two steps of the example Hello, World! app
```sh
# TODO: 4. Show my Application's GUI
window.show()

# TODO: 5. Run My application's event loop (or main loop)
sys.exit(app.exec())
```

- Here I called `.show()` on window. The `show()` call schedules a paint event which is a new event to the apps event queue.

### NOTE: A paint event is a request for painting the widgets that compose a GUI

- Last but not least, I started the application by calling the event loop.
    - `app.exec()` The call to `.exec()` is __wrapped__ in `sys.exit()`, which allows you to cleanly exit Python and release memory resources when the app terminates.

![Image of what the example Hello, World! app looks like](https://files.realpython.com/media/hello.066635a13824.png)
