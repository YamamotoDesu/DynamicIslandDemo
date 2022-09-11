# DynamicIslandDemo

<img width="520" alt="スクリーンショット 2022-09-12 7 06 54" src="https://user-images.githubusercontent.com/47273077/189550852-0ac5951e-505b-4f86-a9ae-766f5764dc3f.gif">

```swift
//
//  ContentView.swift
//  DynamicIslandDemo
//
//  Created by 山本響 on 2022/09/11.
//

import SwiftUI

enum ImageFrame: CGFloat {
    case collapse = 30
    case expanded = 80
}

struct DynamicIslandView: View {
    
    @Binding var expanded: Bool
    
    var body: some View {
        VStack {
            
            HStack {
                Image("batman")
                    .resizable()
                    .frame(width: expanded ? ImageFrame.expanded.rawValue: ImageFrame.collapse.rawValue, height: expanded ? ImageFrame.expanded.rawValue: ImageFrame.collapse.rawValue)
                    .clipShape(Circle())
                    .padding(10)
                
                if expanded {
                    VStack(alignment: .leading) {
                        Text("Batman")
                            .font(.title)
                        Text("Under the red hood")
                            .opacity(0.5)
                    }.foregroundColor(.white)
                }
                
                Spacer()
                Image(systemName: "chart.bar.fill")
                    .foregroundColor(.white)
                    .padding(10)
            }
            
            if expanded {
                HStack {
                    Image(systemName: "backward.fill")
                    Image(systemName: "play.fill")
                    Image(systemName: "forward.fill")
                }.foregroundColor(.white)
                    .font(.title)
            }
        }.frame(maxWidth: .infinity, maxHeight: expanded ? 200: 80)
            .contentShape(Rectangle())
            .onTapGesture {
                withAnimation(.spring(response: 0.6, dampingFraction: 0.6, blendDuration: 1.0)) {
                    expanded.toggle()
                }
            }
            .background {
                Color.black
            }
            .clipShape(RoundedRectangle(cornerRadius: 40.0, style: .continuous))
            .padding()
    }
}

struct ContentView: View {
    
    @State private var expanded: Bool = false
    
    var body: some View {
        VStack {
            DynamicIslandView(expanded: $expanded)
            Spacer()
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```
