# reorderableitemsview

[![pub package](https://img.shields.io/pub/v/reorderableitemsview.svg)](https://pub.dartlang.org/packages/reorderableitemsview)

A Flutter package for staggered grid view or ListView with ordering support

## Info

This plugin uses most for its code from ReorderableListView

This Plugin combines the [ReorderableListView](https://api.flutter.dev/flutter/material/ReorderableListView-class.html) and [flutter_staggered_grid_view](https://pub.dev/packages/flutter_staggered_grid_view) to provide Draggable behaviour for Staggered GridView

## Usage
To use this plugin, add `reorderableitemsview` as a [dependency in your pubspec.yaml file](https://flutter.dev/platform-plugins/).

### Example Staggered GridView

```dart
import 'package:flutter/material.dart';
import 'package:reorderableitemsview/reorderableitemsview.dart';

class GridPageView extends StatefulWidget {
  @override
  _GridPageViewState createState() => _GridPageViewState();
}

class _GridPageViewState extends State<GridPageView> {

  List<StaggeredTileExtended> _listStaggeredTileExtended = <StaggeredTileExtended>[
    StaggeredTileExtended.count(2, 2),
    StaggeredTileExtended.count(2, 1),
    StaggeredTileExtended.count(1, 2),
    StaggeredTileExtended.count(1, 1),
    StaggeredTileExtended.count(2, 2),
    StaggeredTileExtended.count(1, 2),
    StaggeredTileExtended.count(1, 1),
    StaggeredTileExtended.count(3, 1),
    StaggeredTileExtended.count(1, 1),
    StaggeredTileExtended.count(4, 1),
  ];

  List<Widget> _tiles = <Widget>[
    _Example01Tile(Key("a"),Colors.green, Icons.widgets),
    _Example01Tile(Key("b"),Colors.lightBlue, Icons.wifi),
    _Example01Tile(Key("c"),Colors.amber, Icons.panorama_wide_angle),
    _Example01Tile(Key("d"),Colors.brown, Icons.map),
    _Example01Tile(Key("e"),Colors.deepOrange, Icons.send),
    _Example01Tile(Key("f"),Colors.indigo, Icons.airline_seat_flat),
    _Example01Tile(Key("g"),Colors.red, Icons.bluetooth),
    _Example01Tile(Key("h"),Colors.pink, Icons.battery_alert),
    _Example01Tile(Key("i"),Colors.purple, Icons.desktop_windows),
    _Example01Tile(Key("j"),Colors.blue, Icons.radio),
  ];


  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("List Demo"),
      ),
      body: ReorderableItemsView(
        onReorder: (int oldIndex, int newIndex) {
          setState(() {
            _tiles.insert(newIndex, _tiles.removeAt(oldIndex));
          });
        },
        children: _tiles,
        crossAxisCount: 4,
        isGrid: true,
        staggeredTiles: _listStaggeredTileExtended,
        longPressToDrag: false,
      ),
    );
  }
}

class _Example01Tile extends StatelessWidget {
  _Example01Tile(Key key, this.backgroundColor, this.iconData): super(key: key);

  final Color backgroundColor;
  final IconData iconData;

  @override
  Widget build(BuildContext context) {
    return new Card(
      color: backgroundColor,
      child: new InkWell(
        onTap: () {},
        child: new Center(
          child: new Padding(
            padding: EdgeInsets.all(4.0),
            child: new Icon(
              iconData,
              color: Colors.white,
            ),
          ),
        ),
      ),
    );
  }
}
```

### Example ListView

```dart
import 'package:flutter/material.dart';
import 'package:reorderableitemsview/reorderableitemsview.dart';

class ListPageView extends StatefulWidget {
  @override
  _ListPageViewState createState() => _ListPageViewState();
}

class _ListPageViewState extends State<ListPageView> {

  List<Widget> _tiles = <Widget>[
    _Example01Tile(Key("a"),Colors.green, Icons.widgets),
    _Example01Tile(Key("b"),Colors.lightBlue, Icons.wifi),
    _Example01Tile(Key("c"),Colors.amber, Icons.panorama_wide_angle),
    _Example01Tile(Key("d"),Colors.brown, Icons.map),
    _Example01Tile(Key("e"),Colors.deepOrange, Icons.send),
    _Example01Tile(Key("f"),Colors.indigo, Icons.airline_seat_flat),
    _Example01Tile(Key("g"),Colors.red, Icons.bluetooth),
    _Example01Tile(Key("h"),Colors.pink, Icons.battery_alert),
    _Example01Tile(Key("i"),Colors.purple, Icons.desktop_windows),
    _Example01Tile(Key("j"),Colors.blue, Icons.radio),
  ];


  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("List Demo"),
      ),
      body: ReorderableItemsView(
        onReorder: (int oldIndex, int newIndex) {
          setState(() {
            _tiles.insert(newIndex, _tiles.removeAt(oldIndex));
          });
        },
        feedBackWidgetBuilder: (context, index, child) {
          return Container(
            child: child,
          );
        },
        children: _tiles,
        longPressToDrag: false,
      ),
    );
  }
}

class _Example01Tile extends StatelessWidget {
  _Example01Tile(Key key, this.backgroundColor, this.iconData): super(key: key);

  final Color backgroundColor;
  final IconData iconData;

  @override
  Widget build(BuildContext context) {
    return new Card(
      color: backgroundColor,
      child: new InkWell(
        onTap: () {},
        child: new Center(
          child: new Padding(
            padding: EdgeInsets.all(4.0),
            child: new Icon(
              iconData,
              color: Colors.white,
            ),
          ),
        ),
      ),
    );
  }
}
```

### Options

```dart
@required this.children, // List<Widget>
@required this.onReorder, // Callback onReorder(int oldIndex, int newIndex)
this.scrollController, // ScrollController
this.scrollDirection = Axis.vertical, // Axis Ignored in GridView
this.padding, 
this.staggeredTiles, // Only used in GridView, check gridview example above
this.crossAxisCount = 3, // Only used in GridView
this.isGrid = false, // if true renders as gridview
this.reverse = false,
this.longPressToDrag = true,
this.mainAxisSpacing = 0.0, // Only used in GridView
this.crossAxisSpacing = 0.0, // Only used in GridView
this.feedBackWidgetBuilder,
```

## Demo

<img src="https://github.com/PonnamKarthik/reorderableitemsview/raw/master/demo/demo.gif" width="320px" />