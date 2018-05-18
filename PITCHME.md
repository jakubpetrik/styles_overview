# Styles
```
github "inloop/Styles"
```
---
## `TextStyle`


* `UILabel`, `UITextField`, `UITextView`
* Replacement for `NSAttributedString`

---

### `TextStyle.Property`
#### `.font`

```swift
let h1 = TextStyle(
  .font(.prefferedFont(forTextStyle: .largeTitle))
)
```
----

### `TextStyle.Property`
#### `.foregroundColor`

```swift
let red = TextStyle(
  .foregroundColor(.red)
)
```

---

### `TextStyle.Property`
#### `.backgroundColor`

```swift
let highlight = TextStyle(
  .backgroundColor(.yellow)
)
```

---

### `TextStyle.Property`
#### `.paragraphStyle`

---
