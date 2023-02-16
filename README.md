
```swift


extension View {
    
    // read current view's x offset relative to UIScreen from the scroll view
    func onScrollViewYOffsetChanged(action: @escaping(_ offset: CGFloat) -> Void) -> some View {
        self
            .background(
                GeometryReader { geo in
                    // Get the exact offset of title view
                    Color
                        .clear
                        .preference(key: ScrollViewOffsetPrefenrenceKey.self, value: geo.frame(in: .global).minY)
                }
            )
            .onPreferenceChange(ScrollViewOffsetPrefenrenceKey.self) { value in
                action(value)
            }
    }
    
    // read current view's y offset relative to UIScreen from the scroll view
    func onScrollViewXOffsetChanged(action: @escaping(_ offset: CGFloat) -> Void) -> some View {
        self
            .background(
                GeometryReader { geo in
                    // Get the exact offset of title view
                    Color
                        .clear
                        .preference(key: ScrollViewOffsetPrefenrenceKey.self, value: geo.frame(in: .global).minX)
                }
            )
            .onPreferenceChange(ScrollViewOffsetPrefenrenceKey.self) { value in
                action(value)
            }
    }
    
}

```


```swift
struct ScrollViewOffsetPreferenceKeyBootcamp: View {
    
    let title: String = "New Title Here!!!"
    @State private var scrollViewOffset: CGFloat = 0
    
    var body: some View {
    
        ScrollView {
            VStack {
                self.titleLayer
                    // Fade Effect
                    .opacity(Double(self.scrollViewOffset) / 63.0)
                    .onScrollViewYOffsetChanged { offset in
                        self.scrollViewOffset = offset
                    }
                
                self.contentLayer
            }
            .padding()
        }
        .overlay(
            Text("\(self.scrollViewOffset)")
        )
        .overlay(
            self.navBarLayer
                .opacity(self.scrollViewOffset < 40 ? 1.0 : 0.0)
            ,alignment: .top
        )
        
    }
}
```
