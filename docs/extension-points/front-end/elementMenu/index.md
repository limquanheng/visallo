Element Menu Plugin
===================
* [Vertex Menu Javascript API `org.visallo.vertex.menu`](../../../javascript/org.visallo.vertex.menu.html)
* [Edge Menu Javascript API `org.visallo.edge.menu`](../../../javascript/org.visallo.edge.menu.html)

Plugin to add new items to vertex or edge context menu.

## Example

To register an item:

```js
require([
    'configuration/plugins/registry',
    'util/messages'
], function(registry, i18n) {

    //vertex menu item
    registry.registerExtension('org.visallo.vertex.menu', {
        label: i18n('com.myplugin.vertex.menu.label'),
        shortcut: 'alt+i',
        event: 'searchSimilar',
        selection: 2,
        options: {
            insertIntoMenuItems: function(item, items) {
                // Add item as fourth in list
                items.splice(3, 0, item);
            }
        }
    });

    //edge menu item
    registry.registerExtension('org.visallo.edge.menu', {
        label: i18n('com.myplugin.edge.menu.label'),
        shortcut: 'meta-e',
        event: 'selectConnected',
        options: {
            insertIntoMenuItems: function(item, items) {
                // Add item to the end of the list
                items.push(item);
            }
        }
    });
});
```

To create a `shouldDisable` handler the example shown is for a vertex menu item, but the handler has the same signature for either menu.

```js
shouldDisable: function(currentSelection, elementId, domElement, element) {
    // Disable this menu option if the vertex is not a certain type
    return element.conceptType !== 'http://mycompany.com/sub#mySpecialConcept';
}
```

To add a divider:

```js
registry.registerExtension('org.visallo.vertex.menu', 'DIVIDER');  // vertex menu
registry.registerExtension('org.visallo.edge.menu', 'DIVIDER');  //edge menu
```
