# ✨ DeckUI

[![](https://img.shields.io/endpoint?url=https%3A%2F%2Fswiftpackageindex.com%2Fapi%2Fpackages%2Fjoshdholtz%2FDeckUI%2Fbadge%3Ftype%3Dswift-versions)](https://swiftpackageindex.com/joshdholtz/DeckUI)
[![](https://img.shields.io/endpoint?url=https%3A%2F%2Fswiftpackageindex.com%2Fapi%2Fpackages%2Fjoshdholtz%2FDeckUI%2Fbadge%3Ftype%3Dplatforms)](https://swiftpackageindex.com/joshdholtz/DeckUI)
![](https://img.shields.io/github/license/joshdholtz/DeckUI)
[![](https://img.shields.io/badge/SPM-supported-DE5C43.svg?style=flat)](https://swift.org/package-manager/)
[![](https://img.shields.io/badge/twitter-@joshdholtz-blue.svg?style=flat)](<[https://twitter.com/joshdholtz](https://twitter.com/joshdholtz)>)

DeckUI is a Swift DSL (domain specific language) for writing slide decks in Xcode. It allows for quick creation of slides and content in a language and environment you are familiar with.

But _why_?

Well, I made this because:

- I was bored on an airplane
- Wanted to use this as a demo for future conference talk on Swift DSLs
- Need something more customizable than markdown for writing slide decks and more codey than Keynote

👉 Watch [Introducing DeckUI - Write slide decks in Swift](https://www.youtube.com/watch?v=FraeH6OeJPY) on my YouTube channel for more explanation and full demo

👉 Watch [Pushing to the App Store using Swift](https://www.youtube.com/watch?v=SxozYjWMhgU) (7 minutes), one of the first talks public to talks to embrace DeckUI! Also, checkout the [GitHub repo](https://github.com/FullQueueDeveloper/Deck-2022-09-13) for the talk!

## ✨ Features

- [x] Create slide decks in pure Swift code
- [x] Decks are presented in SwiftUI with `Presenter`
- [x] Build decks without knowing any SwiftUI
  - With `Deck`, `Slide`, `Title`, `Words`, `Bullets`, `Media`, `Columns`
- [x] Use `RawView` to drop any SwiftUI view
  - Fully interactive and great for demos
- [x] Display code with `Code`
  - Use up and down arrows to highlight lines of code as your talking about them
- [x] Support videos on `Media`

### 🐌 Future Features

- [ ] Support iOS and maybe tvOS
- [ ] Fix bug with `Media` remote image loading and slide transitions
- [ ] Animations within a slide
- [ ] More customization on `Words`
- [ ] Nesting of `Bullets`
- [ ] Syntax highlighting for `Code`
- [ ] Documentation
- [ ] More examples

## Simple Demo

```swift
import SwiftUI
import DeckUI

struct ContentView: View {
    var body: some View {
        Presenter(deck: self.deck)
    }
}

extension ContentView {
    var deck: Deck {
        Deck(title: "SomeConf 2023") {
            Slide(alignment: .center) {
                Title("Welcome to DeckUI")
            }

            Slide {
                Title("Quick Demo")
                Columns {
                    Column {
                        Bullets {
                            Words("Bullets")
                            Words("Words")
                            Words("Images")
                            Words("Columns")
                        }
                    }

                    Column {
                        Media(.remoteImage(URL(string: "https://www.fillmurray.com/g/200/300")!))
                    }
                }
            }
        }
    }
}
```

https://user-images.githubusercontent.com/401294/189043329-fe75161c-17c1-4471-8632-07fb79d26d1a.mov

## 💻 Installing

### Swift Package Manager

- File > Swift Packages > Add Package Dependency
- Add `https://github.com/joshdholtz/DeckUI.git`
- Select "Up to Next Major" with "1.0.0"

## 🚀 Getting Started

There are no official "Getting Started" docs yet 😅 But look at...

- [Demo app](https://github.com/joshdholtz/DeckUI/blob/main/Examples/Demo/Shared/ContentView.swift) for usage
- [Sources/DeckUI/DSL](https://github.com/joshdholtz/DeckUI/tree/main/Sources/DeckUI/DSL) for how the `Deck`, `Slide`, and all slide components are built
- [Sources/DeckUI/Views](https://github.com/joshdholtz/DeckUI/tree/main/Sources/DeckUI/Views) for how `Presenter` is built

## 📖 Documentation

100% not documented yet but I'll get there 🤷‍♂️

## 🏎 Performance

Probably bad and never production ready 😈 Please only use DeckUI for a single presentation and never at any scale.

## 👨‍💻 Contributing

Yes please! I'm happy to discuss issues and review/merge pull requests 🙂 I will do my best to get to the but I am a dad, work at [RevenueCat](https://www.revenuecat.com/), and the lead maintainer of [fastlane](https://github.com/fastlane/fastlane) so I might not respond right away.

## 📚 Examples

### Slide

`Slide` can be used without any parameters but can be given a custom `alignment`, `padding`, and `theme`.

```swift
Slide {
    // Content
}
```

```swift
Slide(alignment: .center, padding: 80, theme: .white) {
    // Content
}
```

### Title

`Title` can be used by itself or with an optional `subtitle`. It was real similar to `Words` but larger.

```swift
Slide(alignment: .center) {
    Title("Introducing...")
}
```

```swift
Slide {
    Title("Introduction", subtitle: "What is it?")
    // Content
}
```

### Words

`Words` are similar to what a textbox would be in Keynote, PowerPoint, or Google Slides. There will eventually be more style configurations for words.

```swift
Slide(alignment: .center) {
    Title("Center alignment")
    Words("Slides can be center aligned")
    Words("And more words")
}
```

### Bullets

`Bullets` turns `Words` into a list. It takes an optional `style` parameter where you can choose between `.bullets` and `.dash`. `Bullets` cannot be nested yet but soon™️.

```swift
Slide {
    Title("Introduction", subtitle: "What is it?")
    Bullets {
        Words("A custom Swift DSL to make slide decks")
        Words("Distributed as a Swift Package")
        Words("Develop your slide deck in Xcode with Swift")
    }
}
```

```swift
Slide {
    Title("Introduction", subtitle: "What is it?")
    Bullets(style: .dash) {
        Words("A custom Swift DSL to make slide decks")
        Words("Distributed as a Swift Package")
        Words("Develop your slide deck in Xcode with Swift")
    }
}
```

### Media

`Media` provides a few ways to display images from various source types. This will eventually support videos.

```swift
Slide {
    Media(.assetImage("some-asset-name"))
    Media(.bundleImage("some-file-name.jpg"))
    Media(.remoteImage(URL(string: "http://placekitten.com/g/200/300"))!)
}
```

### Columns

`Columns` allow you to use one to infinte `Column`s. Put other slide content in `Column`.

```swift
Slide {
    Title("Columns")
    Columns {
        Column {
            // Content
        }

        Column {
            // Content
        }
    }
}
```

```swift
Slide {
    Title("Columns")
    Columns {
        Column {
            // Content
        }

        Column {
            // Content
        }

        Column {
            // Content
        }

        Column {
            // Content
        }
    }
}
```

### Code

`Code` is a super specifi version `Words`. It will:

- Display text as monospace
- Scroll vertical if bigger than screen
- Highlight lines of code when up and down arrows are pressed

```swift
Slide {
    Code("""
    struct ContentView: View {
        var body: some View {
            Text("Hello slides")
        }
    }
    """)
}
```

```swift
Slide {
    Code("""
    struct ContentView: View {
        var body: some View {
            Text("Hello slides")
        }
    }
    """, , enableHighlight: false)
}
```

### RawView

Drop any SwiftUI view inside of `RawView`. Could be built-in SwiftUI views like `Text` or `Button` but can also be any custom SwiftUI view.

```swift
Slide {
    RawView {
        CounterView()
    }
}

struct CounterView: View {
    @State var count = 0

    var body: some View {
        Button {
            self.count += 1
        } label: {
            Text("Press me - \(self.count)")
                .font(.system(size: 60))
                .padding(.horizontal, 40)
                .padding(.vertical, 20)
                .foregroundColor(.white)
                .overlay(
                    RoundedRectangle(cornerRadius: 25)
                    .stroke(Color.white, lineWidth: 2)
                )
        }.buttonStyle(.plain)
    }
}
```

### Themes

A `Theme` can be set in `Presenter` or individually on `Slide`. There are three default themes (`.dark`, `.black`, `.white`) but feel free to use your own.

```swift
struct ContentView: View {
    var body: some View {
        Presenter(deck: self.deck, showCamera: true)
    }
}

extension Theme {
    public static let venonat: Theme = Theme(
        background: Color(hex: "#624a7b"),
        title: Foreground(
            color: Color(hex: "#ff5a5a"),
            font: Font.system(size: 80,
                              weight: .bold,
                              design: .default)
        ),
        subtitle: Foreground(
            color: Color(hex: "#a48bbd"),
            font: Font.system(size: 50,
                              weight: .light,
                              design: .default).italic()
        ),
        body: Foreground(
            color: Color(hex: "#FFFFFF"),
            font: Font.system(size: 50,
                              weight: .regular,
                              design: .default)
        ),
        code: Foreground(
            color: Color(hex: "#FFFFFF"),
            font: Font.system(size: 26,
                              weight: .regular,
                              design: .monospaced)
        ),
        codeHighlighted: (Color(hex: "#312952"), Foreground(
            color: Color(hex: "#FFFFFF"),
            font: Font.system(size: 26,
                              weight: .heavy,
                              design: .monospaced)
        ))
    )
}
```
