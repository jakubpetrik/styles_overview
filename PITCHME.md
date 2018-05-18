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
* Demo
* Zeplin Extension 🤯
* 🍻
---
### What the Styles?!
<p>
- __declarative__: You describe the style, framework will do the rest
- __type-safe__: Type system will help you describe your style
- __plays nice with UIAppearance__: In fact its designed for it.
- __usable as settable property__:  Not only works as UIAppearance proxy, but also as settable property
- __supports UIControl states and UITextField editing__: You're gonna ❤︎ it.
- __saves you from the `NSAttributedString`<sup><sup>[1](#soso)</sup></sup>__: Just work with `String`s.
- __text, color and layer properties__: Custom line height, letter spacing, corners? Me gusta.
- __supports Styles updating__: Design base style for you app and update it on the fly as needed.
- __Zeplin extension__: Just copy styles over to your project. Super easy. 

<sub><sub><a name="soso">1</a>: In most cases.</sub></sub>
</p>

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