@title[Styles]
# Styles
```
github "inloop/Styles"
```
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
  init(style: Style, pattern: Pattern, byWord: Bool = false, color: UIColor? = nil) { ... }
}