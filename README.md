# TableViewManager

[![Version](https://img.shields.io/cocoapods/v/TableViewManager.svg?style=flat)](http://cocoapods.org/pods/TableViewManager)
[![License](https://img.shields.io/cocoapods/l/TableViewManager.svg?style=flat)](http://cocoapods.org/pods/TableViewManager)
[![Platform](https://img.shields.io/cocoapods/p/TableViewManager.svg?style=flat)](http://cocoapods.org/pods/TableViewManager)

## Description

Pod registers cells (Nibs and dynamic one) and allows you to handle all UITableViewCells with enum. Written in Swift.

## Installation

TableViewManager is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod "TableViewManager"
```

## Quick Start (in 3 steps!)

### Step 1

Remember about `import TableViewManager`. Make sure that `ViewController` is your UITableView's data source.

### Step 2

Implemment `tableView(_:cellForRowAtIndexPath:)` as below.

```swift
extension ViewController: UITableViewDataSource {
    func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
        return self.tableViewManager(tableView, cellForRowAtIndexPath: indexPath)
    }

    // (...)
}
```

### Step 3

Implemment `TableViewManager` protocol.

```swift
extension ViewController: TableViewManager, EnumTableViewManager {
    // Cell identifier should be the same as you set in .xib or storyboard file.
    enum TableViewCellsIdentifiers: String {
        case TextTableViewCell
        case ImageTableViewCell
    }

    // Return cell indentifier for provided indexPath
    func tableView(tableView: UITableView, cellIdentifierForIndexPath indexPath: NSIndexPath) -> TableViewCellsIdentifiers {
        return .TextTableViewCell
    }

    // Configure cell as before in tableView(_:cellForRowAtIndexPath:)
    func tableView(tableView: UITableView, configureCell cell: UITableViewCell, forIndexPath indexPath: NSIndexPath) {
        if let cell = cell as? TextTableViewCell {
            cell.myLabel.text = "Lorem Ipsum"
        }
    }

    // Implemment if you want to change default Nib name, which is the same as identifier
    //func tableView(tableView: UITableView, nibNameForCellIdentifier cellIdentifier: TableViewCellsIdentifiers) -> String? {
    //    return nil
    //}
}
```

That's all!

You can also use `TableViewManager` without enum. It could be useful when you creating external data source object.

## License

TableViewManager is available under the MIT license. See the LICENSE file for more info.
