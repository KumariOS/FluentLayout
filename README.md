# FluentLayout

![Swift 3.0.1](https://img.shields.io/badge/Swift-3.0.1-green.svg)
[![CocoaPods compatible](https://img.shields.io/cocoapods/v/FluentLayout.svg)](#cocoapods)
[![License](http://img.shields.io/:license-mit-blue.svg)](http://doge.mit-license.org)

## Overview

FluentLayout's primary goal is to provide a simple, readable way to write UI code in Swift. Not using storyboards and doing all UI work all in code can be very daunting and get very complex very quickly.

A `Layout` is just a UIStackView under the covers with some nicer syntax and helpers on top.

In FluentLayout there is the concept of a section in the UI. All a section is, is just a simple way of breaking up a section to the UI of related items into it's own part with a different background color.

## Usage

For example if we were creating a new social media app and at the top of the want the following profile header:

<img src="https://github.com/wickwirew/FluentLayout/blob/master/Examples/ProfileHeader.png" width="375">

First we would create the layout and controls. Then add the layout to the view and add constraints for its top, left, and right edges.
Note: the controls are not added to the layout yet.

```swift
let layout = Layout()
view.addSubview(layout)
layout.pinToSuperview(top: 12, left: 12, right: 12)

let profilePicture = UIImageView()
profilePicture = UIImage(named: "ProfilePicture")

let name = UILabel()
name.text = "Wes Wickwire"
name.font = UIFont.systemFont(ofSize: 15)

let title = UILabel()
title.text = "Last online 8 hrs ago"
title.textColor = .lightGray
title.font = UIFont.systemFont(ofSize: 13, weight: UIFontWeightLight)
```

On the layout we can call `layout.addSection` then in a closure layout the section. 

```swift
layout.addSection {
    $0.addStack(axis: .horizontal, alignment: .top, spacing: 8) {

        $0.add(view: profilePicture).pin(size: CGSize(width: 50, height: 50))

        $0.addStack(axis: .vertical, spacing: 0) {
            $0.add(view: name)
            $0.add(view: title)
        }
    }
}
```

All default colors, spacings, and insets can be changed from the `LayoutDefaults` class.

For customizing the default controls (e.g. using methods like `layout.addLabel(text:)`) create a new class that conforms to the protocol `LayoutDefaultControls` and set `LayoutDefaults.defaultControls` to an instance of your new class. It will then use that to create all controls. Use of this class is not needed at all, provided as a ease of use to quickly add UI elements.

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

In the exmaple project, the following view is created.

<img src="https://github.com/wickwirew/FluentLayout/blob/master/Examples/ExampleScreenShot.png" width="300">

The code below creates the view above.

```swift
layout.create(spacing: 12) {

    // Top Title
    $0.addSection(title: "Lorem Ipsum")

    // Main Image, keep ratio of image
    $0.addImage(named: "snow.png").pinImageAspectRatio()

    // This section holds post information
    $0.addSection {

        // Group to contain the title, time stamp and heart
        $0.addStack(alignment: .center, spacing: 0) {

            // Title and time stamp should be on top of each other
            $0.addStack(axis: .vertical, spacing: 0) {
                $0.addTitleLabel(text: "Neque Porro Quisquam")

                // Add custom label
                $0.add(view: createdTime)
            }

            // Add heart button but pin width to 44
            $0.add(view: heartButton).pin(width: 44)
        }

        // add post body
        $0.addLabel(text: loremIpsum)
    }
}
```

## Requirements
* Xcode 8.0
* Swift 3.0+

## Installation

FluentLayout is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'FluentLayout'
```
## Contributions

Contributions are welcome and encouraged!

## Author

Wesley Wickwire, wickwirew@gmail.com

## License

FluentLayout is available under the MIT license. See the LICENSE file for more info.
