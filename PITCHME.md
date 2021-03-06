@title[Styles]
# Styles
https://github.com/inloop/Styles
---
## Agenda
@ul
* What the Styles?!
* TextStyle
  * Properies
  * Effects
* ViewStyle
  * Properties
* Combining
* Demo
* 🍻
@ulend
---
### What the Styles?!
@ul
- easy styling
- type-safe
- declarative
- easy to reason about
- has Zeplin extension
@ulend
---
### What makes Styles?!
@ul
- TextStyle
- ViewStyle
- SwitchStyle
- more (soon)
@ulend
---

## TextStyle
@ul
* Replacement for `NSAttributedString`
* `UILabel`, `UITextField`, `UITextView` or plain
* Properties
* TextEffects
@ulend

---

### TextStyle.Property

```swift
class TextStyle {
  enum Property {
    case font(UIFont)
    case foregroundColor(UIColor)
    case backgroundColor(UIColor)
    case paragraphStyle([ParagraphStyle])
    case letterSpacing(CGFloat)
    case strikethrought(TextDecoration)
    case underline(TextDecoration)
    case obliqueness(Double)
    case shadow(Shadow)
    case writingDirectionOverrides([WritingDirectionOverride])
    case baselineOffset(Double)
  }
}
```
---
@title[Font]
### TextStyle.Property.font

```swift
case font(UIFont)
```

```swift
let h1 = TextStyle(
  .font(.preferredFont(forTextStyle: .largeTitle))
)
```
---
@title[Foreground Color]
### TextStyle.Property.foregroundColor
```swift
case foregroundColor(UIColor)
```
```swift
let red = TextStyle(
  .foregroundColor(.red)
)
```
---
@title[Background Color]
### TextStyle.Property.backgroundColor
```swift
case backgroundColor(UIColor)
```
```swift
let highlight = TextStyle(
  .backgroundColor(.yellow)
)
```
---
@title[ParagraphStyle]
### TextStyle.Property.paragraphStyle

```swift
case paragraphStyle([ParagraphStyle])

enum ParagraphStyle { 
  // .left, .right, .center, .justified, .natural
  case alignment(NSTextAlignment)
  // lineSpacing != lineHeight in Zepline
  case lineSpacing(CGFloat)
}

let centered = TextStyle(
  .paragraphStyle([
    .alignment(.center),
    .lineSpacing(1.5)
  ])
)
```
@[1]
@[3-9]
@[10-17]

---
@title[LetterSpacing]
### TextStyle.Property.letterSpacing
```swift
case letterSpacing(CGFloat)
```
```swift
let wide = TextStyle(
  .letterSpacing(10.4)
)
```
---
@title[TextDecoration]
### TextStyle.Property.strikethrought
```swift
case strikethrought(TextDecoration)
```
```swift
struct TextDecoration {
  enum Pattern {
    case dot, dash, dashDot, dashDotDot
  }

  enum Style {
    case single, thick, double
  }

  init(
    style: Style, pattern: Pattern, 
    byWord: Bool = false, color: UIColor? = nil
  ) { ... }
}
```
---
@title[Strikethrough]
### TextStyle.Property.strikethrought
```swift
let deprecated = TextStyle(
  .strikethrought(TextDecoration(
    style: .thick,
    pattern: .dash
  ))
)
```
---
@title[Underline]
### TextStyle.Property.underline
```swift
case underline(TextDecoration)
```

```swift
let important = TextStyle(
  .underline(TextDecoration(
    style: .single,
    pattern: .dashDotDot,
    byWord: true,
    color: .red
  ))
)
```
---
@title[Obliqueness]
### TextStyle.Property.obliqueness
```swift
case obliqueness(Double)
```

```swift
let bold = TextStyle(
  .obliqueness(10.4)
)
```
---
@title[Shadow]
### TextStyle.Property.shadow
```swift
case shadow(Shadow)

struct Shadow {
  let color: UIColor
  let opacity: Float
  let offset: UIOffset
  let radius: CGFloat
  let shouldRasterizeLayer: Bool
  let rasterizationScale: CGFloat
}
```
---
@title[Shadow Example]
### TextStyle.Property.shadow
```swift
let blackShadow = TextStyle(
  .shadow(Shadow(
    color: .black,
    offset: UIOffset(horizontal: 10, vertical: 4),
    radius: 1.04
  ))
)
```
---
@title[WritingDirectionOverride]
##### TextStyle.Property.writingDirectionOverrides
```swift
case writingDirectionOverrides([WritingDirectionOverride])
```
```swift
enum WritingDirectionOverride {
  case leftToRightEmbedding
  case rightToLeftEmbedding
  case leftToRightOverride
  case rightToLeftOverride
}

let rtl2 = TextStyle(
  .writingDirectionOverrides(
    .rightToLeftEmbedding,
    .rightToLeftOverride
  )
)
```
---
@title[BaselineOffset]
### TextStyle.Property.baselineOffset
```swift
case baselineOffset(Double)
```
```swift
let body = TextStyle(
  .baselineOffset(10.4)
)
```
---
@title[TextEffects Summary]
### TextEffects
@ul
- useful for strings with multiple styles
- style or image
- only for UILabel and UITextView
@ulend 
---

### TextEffect
```swift
enum TextEffect {
  case style(TextStyle, Match)
  case image(UIImage, TextStyle, Match)

  init(style: TextStyle, matching match: Match) { ... }
  init(
    image: UIImage, 
    style: TextStyle = .empty, 
    matching match: Match
  ) { ... }
}
```
---
@title[TextEffect Example]
### TextEffect
```swift
let logo: UIImage = ...

let logoBeforeCompanyName = TextEffect(
  image: logo, 
  matching: First(occurenceOf: "INLOOPX")
)

let title = TextStyle(
  .foregroundColor(.green),
  ...
  effects([
    logoBeforeCompanyName
  ])
)
```
---
@title[TextEffect Helpers]
### TextEffect
```swift
// appending effect
let h1: TextStyle = ...
let title = h1.appending(
  logoBeforeCompanyName
)

// removing effect
let justH1 = title.removing(
  logoBeforeCompanyName
)
```
---
### Match
```swift
protocol Match {
  func ranges(in base: String) -> [NSRange]
}
```
---
@title[Match Styles default]
### Match
@ul
- `First`
- `Regex` 
  - `.wordMatches`
  - `.wordStarts` 
  - `.wordEnds` 
  - `.lastWord`
  - `.firstWord`
- `Range`
- `Block`
@ulend

---
## Usage

```swift
let h1: TextStyle = ...

myLabel.textStyle = h1

MyLabel.appearance().textStyle = h1

let myAttributedString = h1.apply(to: "INLOOPX")
```
---
## ViewStyle

- same principle as `TextStyle`
- for all `UIView`s
- Properties

---
### ViewStyle.Property

```swift
class ViewStyle {
  enum Property {
    case backgroundColor(UIColor?)
    case tintColor(UIColor?)
    case borderColor(UIColor)
    case borderWidth(CGFloat)
    case cornerRadius(CGFloat)
    case opacity(Float)
    case shadow(Shadow)
  }
}
```
---
## Combining styles

```swift
let h1: TextStyle = 
let blackShadow: TextStyle =
let fancyTitle = h1 + blackShadow

...

let h1: ViewStyle =
let redBorder: ViewStyle = 
let redTitle = h1 + redBorder
```

---
## Updating styles
```swift
func updating(_ properties: Property...) -> TextStyle
func updating(_ properties: Property...) -> ViewStyle
```
```swift
let blueHeader = h1.updating(
  .foregroundColor(.blue)
)

let roundRed = round.updating(
  .tintColor(.red)
)
```
---
## Usage

```swift
let round = ViewStyle(
  .cornerRadius(10.4)
)

myView.viewStyle = round
// or
MyView.appearance().viewStyle = round
```

---
# DEMO
---
# Questions? 🤔
---
# 🖖
