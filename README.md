# ThinkVantage Dashboard: A system tool for ThinkPads.

ThinkVantage Dashboard works best with acpi_call, akmod-tp_smapi, akmod-acpi_call
and tp_smapi installed.

![Image of System Overview](http://i.imgur.com/QBbEaVz.png)
![Image of Memory](http://i.imgur.com/xHA5CHk.png)

If the ThinkVantage button is usele... err, unused, it will automatically use it
as a hotkey.

ThinkVantage Dashboard can be extended via plugins which are pythonic classes.

```python
class MyPlugin():
    def __init__(self):
        # Perform basic initialization
        self.autoupdate = -1 # Reloads data via getListboxRows every self.autoupdate seconds

    def getHeader(self):
        # Return a title as shown in the sidebar
        return 'My Plugin'

    def shouldDisplay(self):
        # Perform checks whether this plugin is available on this ThinkPad
        return True

    def getListboxRows(self):
        # Return a list of GtkWidgets for the main area
        rows = []
        # Displays a title ('Nothing') on the left, a the content of the
        # file ('/dev/null') on the right
        rows.append(addToListbox('Nothing', '/dev/null'))

        # Adds a title on the left, and a progressbar with subtitle
        # on the right
        rows.append(addPercentageToListbox('How full is the glass?',
                50.0,
                "volume of liquid"
        ))

        # Custom row with a GtkBox
        box = Gtk.Box()
        box.add(Gtk.Label("Hello"))
        box.add(Gtk.Label("World"))
        rows.append(box)

        return rows

# Add an instance of the plugin for auto-discovery with priority 99
PLUGINS.append((99, MyPlugin()))
```
