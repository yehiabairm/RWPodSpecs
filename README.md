# Speakol iOS SDK

This repository contains the Speakol iOS SDK source.

This guide is intended for publishers who want to use Speakol to monetize an iOS app that's built natively.

## Features

- [x] Insert speakol ads in UITableView
- [x] Insert speakol ads in UICollectionView
- [x] Support Image/Video Ads

## Requirements

- iOS 11.0

#### Background

See
[the Podfile Syntax Reference](https://guides.cocoapods.org/syntax/podfile.html#pod)
for instructions and options about overriding pod source locations.


## Installation

### Cocoapods

Install [Cocoapods](https://cocoapods.org/#install) if need be.

```bash
$ gem install cocoapods
```

Add `Speakol-SDK` in your `Podfile`.

```ruby
use_frameworks!

pod 'Speakol-SDK' # not published yet
```
Then, run the following command.

```bash
$ pod install
```

## Supported Views

| View |
|---|
|1. UITableView | 
|2. UICollectionView |

## Example

- for achieving view like this

<img src="https://github.com/yehiabairm/RWPodSpecs/raw/master/IMG_1272.PNG" width="250">

## Usage

Firstly, import `Speakol`.

```swift
import Speakol
```
Then, add initalizers to `AppDelegate` inside `didFinishLaunchingWithOptions` method to be like this

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  SpeakolManager.shared.speakolToken = "token_from_speakol_portal"
  SpeakolManager.shared.widgetId = "widget_id"
  SpeakolManager.shared.initializeSpeakolWithToken()
  return true
}
```

### Initialization for UITableView

- By storyboard, changing class of any `UITableView` to `SpeakolTableView`.

_**Note:** Set Module to `Speakol`._

### Configure SpeakolTableView

- First you need to implement `SpeakolTableViewDelegate`, and `SpeakolTableViewDataSource` like this:

```swift
class ViewController: UIViewController, SpeakolTableViewDelegate, SpeakolTableViewDataSource
```

- then you need to set `speakolDelegate`, and `speakolDataSource`

```swift
speakolTableView.speakolDelegate = self
speakolTableView.speakolDataSource = self
```
- then implement this method like native tableView

```swift
func speakolTableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  return number_of_your_items_want_to_be_displayed // not the speakol items will be inserted in another section this section is used for the publisher items only
}
func speakolTableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
  // here you will return the any tableview cell you want to dispaly
  let cell = speakolTableView.dequeueReusableCell(withIdentifier: "Cell", for: indexPath) as UITableViewCell
  return cell
}
```
also if you want to add speakol ads to the top of your `SpeakolTableView` set `SpeakolTableView.isTop = true`

### And for the publishers who have already existing UICollectionView you can update it to:

- By storyboard, changing class of any `UICollectionView` to `SpeakolCollectionView`.

_**Note:** Set Module to `Speakol`._

### Configure SpeakolCollectionView

- First you need to implement `SpeakolCollectionViewDelegate`, `SpeakolCollectionViewDataSource`, and `SpeakolCollectionViewDelegateFlowLayout` like this:

```swift
class ViewController: UIViewController, SpeakolCollectionViewDelegate, SpeakolCollectionViewDataSource, SpeakolCollectionViewDelegateFlowLayout
```

- then you need to set `speakolDelegate`, `speakolDataSource`, and `speakolDelegateFlowLayout`

```swift
collectionView.speakolDelegate = self
collectionView.speakolDataSource = self
collectionView.speakolDelegateFlowLayout = self
```
- then implement this method like native collectionView

```swift
func speakolCollectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return number_of_your_items_want_to_be_displayed // not the speakol items will be inserted in another section this section is used for the publisher items only
}
    
    func speakolCollectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "VideoCollectionViewCell", for: indexPath) as! UICollectionViewCell
        return cell
}
    
    func speakolCollectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        let collectionCellSize = collectionView.frame.size.width
        return CGSize(width: collectionCellSize/2, height: 100)
}
```

