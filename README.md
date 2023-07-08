# Sinx-RealityKit-SwiftUI-
A simple sine function image that can move
# The first part
![IMG_0265](https://github.com/S-way520/Sinx-RealityKit-SwiftUI-/assets/95877651/2aabe3ac-49d8-4ebe-ad3e-9a95c901ff70)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
import RealityKit
struct ContentView: View {
    var body: some View {
        ARViewContainer()
            .edgesIgnoringSafeArea(.all)
    }
}
struct ARViewContainer: UIViewRepresentable {
    func makeUIView(context: Context) -> ARView {
        let arView = ARView(frame: .zero)
        let anchorEntity = AnchorEntity(plane: .horizontal)
        for siny in 0..<15 {
            let sphereEntity = ModelEntity(mesh: MeshResource.generateSphere(radius: 0.2 / 10), materials: [SimpleMaterial(color: .red, isMetallic: false)])
            let x = Float(siny) * 0.05
            sphereEntity.position.x = x
            anchorEntity.addChild(sphereEntity)
            arView.scene.addAnchor(anchorEntity)
            Timer.scheduledTimer(withTimeInterval: 0.02, repeats: true) { _ in
                let date = Date().timeIntervalSince1970
                let sinValue = 0.1 * sin(3 * date - Double(siny) / 2)
                sphereEntity.position.y = Float(sinValue)
            }
        }
        return arView
    }
    func updateUIView(_ uiView: ARView, context: Context) {}
}
```
