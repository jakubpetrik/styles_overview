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