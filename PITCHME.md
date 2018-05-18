@title[Styles]
# Styles
https://github.com/inloop/Styles
---
## Agenda
* What the Styles?!
* TextStyle
  * Properies
  * Effects
* ViewStyle
  * Properties
* Bonus: SwitchStyle
* Demo
* 🍻
---
## TextStyle

* `UILabel`, `UITextField`, `UITextView`
* Replacement for `NSAttributedString`
* Properties and Effects

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
```
```swift
enum ParagraphStyle { 
  // NSTextAlignment: 
  // .left, .right, .center, .justified, .natural
  case alignment(NSTextAlignment)
  case lineSpacing(CGFloat)
}
```
```swift
let centered = TextStyle(
  .paragraphStyle([
    .alignment(.center),
    .lineSpacing(1.5)
  ])
)
```
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
```
```swift
struct Shadow {
  let color: UIColor
  let opacity: Float
  let offset: UIOffset
  let radius: CGFloat
  let shouldRasterizeLayer: Bool
  let rasterizationScale: CGFloat
}
```