# 🛋️ AR Furniture Placement App

A simple augmented reality app built using Unity and AR Foundation that allows users to place, move, scale, and rotate virtual furniture in real-world space using their mobile device.

## 📱 Platform

- **Engine**: Unity 2020.3.32f1 (LTS)
- **AR SDK**: AR Foundation 4.1.7
- **Tested Device**: Google Pixel 2 XL
- **Base Scene**: `SimpleAR` scene from AR Foundation Samples

---

## ✨ Features

- **Surface Detection**  
  Uses AR Foundation's surface detection with a custom **Placement Indicator** to guide the user without displaying AR planes.

- **Furniture Placement**  
  Spawn 3D furniture models at detected surfaces by tapping the screen. Uses `Vector3.Lerp` for scale animation to make spawning smooth and visually appealing.

- **Object Manipulation**  
  - **Select**: Tap to select an object (highlighted using Outline shader).
  - **Move**: Drag finger to move the selected object using world-space translation logic.
  - **Rotate**: Use two fingers to rotate the object based on gesture slope delta.
  - **Scale (optional)**: Can be implemented using pinch gesture.

- **Lighting & Shadows**  
  - Two directional lights (key + fill)
  - Furniture models have **blob shadows** for grounding effects.
  - PBR textures recommended (e.g., Evermotion assets, optimized for real-time rendering).

- **UI/UX**  
  - Scrollable menu with icons to spawn various furniture items.
  - Icons: Screenshots of 3D models on white backgrounds.
  - UI elements are raycast-blocked to prevent interaction conflict.

---

## 🧱 Architecture

- `Assets/Scenes/SimpleAR` – Base AR scene.
- `Scripts/` – All interaction logic including placement, selection, movement, rotation.
- `Prefabs/` – 3D furniture assets with correct pivot points and shadows.
- `UI/` – Canvas icons, scroll menu, placement toggle.

---

## 📜 Key Scripts

### Object Scale Animation
```csharp
IEnumerator LerpObjectScale(Vector3 a, Vector3 b, float time, GameObject lerpObject) {
    float i = 0.0f;
    float rate = (1.0f / time);
    while (i < 1.0f) {
        i += Time.deltaTime * rate;
        lerpObject.transform.localScale = Vector3.Lerp(a, b, i);
        yield return null;
    }
}
