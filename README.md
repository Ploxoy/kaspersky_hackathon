### Winning solution for Hackathon on Data Analysis from "Kaspersky lab"
https://events.kaspersky.com/hackathon/

### Team DMIA [Data Mining In Action]:
https://github.com/aguschin, https://github.com/canorbal, https://github.com/ohld

check out our elective course on Data Mining in MIPT - https://github.com/vkantor/MIPT_Data_Mining_In_Action_2016

### Task
Multivariate time series classification ("normal" TS vs TS with anomalies) based on Tennessee Eastman Problem http://users.abo.fi/khaggblo/RS/McAvoy.pdf

Detailed task description can be found in README.pdf

Data can be downloaded from https://yadi.sk/d/LzWCsMmo3GvWrt

### Brief solution description:

0) Train LSTM to predict timeseries on 10 ticks ahead using "normal" TS as training data. lstm_baseline_nextstep.ipynb
1) Use LSTM to predict all TS from Train and Test and calculate new features based on error amount statistics.
2) Train Xgboost in xgboost_baseline.ipynb (producing xgb_best_4_knn.csv).
3) Train ExtraTrees in extratrees_baseline-window-lstm.ipynb (producing et_window_250_lstm.csv)
4) Train KNN in KNN_baseline.ipynb (producing knn_best.csv and final mixed submission  knn_xgb_et_RANKS_FINAL_002.csv)

Basically, all three models share the same features - different statistics based upon different columns and their derivatives which belong to the same file and thus have the same label (either 1 for anomalies or 0 for "normal" TS). Extratrees also have "error features" provided by LSTM predictions.


# Regex

> Swifty [regular expressions](https://en.wikipedia.org/wiki/Regular_expression)

This is a wrapper for [`NSRegularExpression`](https://developer.apple.com/documentation/foundation/nsregularexpression) that makes it more convenient and type-safe to use regular expressions in Swift.

## Install

Add the following to `Package.swift`:

```swift
.package(url: "https://github.com/sindresorhus/Regex", from: "0.1.0")
```

[Or add the package in Xcode.](https://developer.apple.com/documentation/xcode/adding_package_dependencies_to_your_app)

## Usage

First, import the package:

```swift
import Regex
```

[Supported regex syntax.](https://developer.apple.com/documentation/foundation/nsregularexpression#1661061)

### Examples

Check if it matches:

```swift
Regex(#"\d+"#).isMatched(by: "123")
//=> true
```

Get first match:

```swift
Regex(#"\d+"#).firstMatch(in: "123-456")?.value
//=> "123"
```

Get all matches:

```swift
Regex(#"\d+"#).allMatches(in: "123-456").map(\.value)
//=> ["123", "456"]
```

Replacing first match:

```swift
"123🦄456".replacingFirstMatch(of: #"\d+"#, with: "")
//=> "🦄456"
```

Replacing all matches:

```swift
"123🦄456".replacingAllMatches(of: #"\d+"#, with: "")
//=> "🦄"
```

Named capture groups:

```swift
let regex = Regex(#"\d+(?<word>[a-z]+)\d+"#)

regex.firstMatch(in: "123unicorn456")?.group(named: "word")?.value
//=> "unicorn"
```

[Pattern matching:](https://docs.swift.org/swift-book/ReferenceManual/Patterns.html)

```swift
switch "foo123" {
case Regex(#"^foo\d+$"#):
	print("Match!")
default:
	break
}

switch Regex(#"^foo\d+$"#) {
case "foo123":
	print("Match!")
default:
	break
}
```

Multiline and comments:

```swift
let regex = Regex(
	#"""
	^
	[a-z]+  # Match the word
	\d+     # Match the number
	$
	"""#,
	options: .allowCommentsAndWhitespace
)

regex.isMatched(by: "foo123")
//=> true
```

## API

[See the API docs.](https://sindresorhus.com/Regex/Structs/Regex.html)

## FAQ

### Why are pattern strings wrapped in `#`?

Those are [raw strings](https://www.hackingwithswift.com/articles/162/how-to-use-raw-strings-in-swift) and they make it possible to, for example, use `\d` without having to escape the backslash.

## Related

- [Defaults](https://github.com/sindresorhus/Defaults) - Swifty and modern UserDefaults
- [KeyboardShortcuts](https://github.com/sindresorhus/KeyboardShortcuts) - Add user-customizable global keyboard shortcuts to your macOS app
- [LaunchAtLogin](https://github.com/sindresorhus/LaunchAtLogin) - Add “Launch at Login” functionality to your macOS app
- [More…](https://github.com/search?q=user%3Asindresorhus+language%3Aswift)

## Sponsors

- [Paypal](https://www.paypal.com/donate?business=RBHMVN4AQGQE2&currency_code=BRL)


