@title[Styles]
```
github "inloop/Styles"
```
---
## `TextStyle`


* `UILabel`, `UITextField`, `UITextView`
* Replacement for `NSAttributedString`

---

### `TextStyle`
### Properties

 - `.font(UIFont)`
case foregroundColor(UIColor)
        /// Specifies the text backgroundColor
        case backgroundColor(UIColor)
        /// Spcifies the text `ParagraphStyle`
        case paragraphStyle([ParagraphStyle])
        /// Specifies letter spacing
        case letterSpacing(CGFloat)
        /// Specifies the `TextDecoration` of strikethrought
        case strikethrought(TextDecoration)
        /// Specifies the `TextDecoration` of underline
        case underline(TextDecoration)
        /// Specifies the obliqueness of the text
        case obliqueness(Double)
        /// Specifies the text `Shadow`
        case shadow(Shadow)
        /// Specifies array of `WritingDirectionOverride`
        case writingDirectionOverrides([WritingDirectionOverride])
        /// Specifies baseline offset
        case baselineOffset(Double)