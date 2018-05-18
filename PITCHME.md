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

### TextStyle.Properties

```swift
class TextStyle {
  enum Properties {
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
### TextStyle.Properties.font

```swift
case font(UIFont)
```

```swift
let h1 = TextStyle(
  .font(.preferredFont(forTextStyle: .largeTitle))
)
```
---

### TextStyle.Properties.foregroundColor
```swift
case foregroundColor(UIColor)
```
```swift
let red = TextStyle(
  .foregroundColor(.red)
)
```
---
### TextStyle.Properties.backgroundColor
```swift
case backgroundColor(UIColor)
```
```swift
let highlight = TextStyle(
  .backgroundColor(.yellow)
)
```
---
### TextStyle.Properties.paragraphStyle
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