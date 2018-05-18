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
### What the Styles?!
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
### TextEffect
```swift
let blackBackground = TextStyle(
  .backgroundColor(.black)
)
let logo: UIImage = ...
let logoBeforeCompanyName = TextEffect(
  image: logo, 
  style: blackBackground, 
  matching: First(occurenceOf: "INLOOPX")
)
let title = TextStyle(
  .foregroundColor(.green),
  effects([
    logoBeforeCompanyName
  ])
)
```
---
### Match
```swift
protocol Match {
  func ranges(in base: String) -> [NSRange]
}
```