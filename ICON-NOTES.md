# App Icon Requirements

The app icon placeholder lives at:
```
ios/App/App/Assets.xcassets/AppIcon.appiconset/AppIcon-512@2x.png
```

## What You Need

A single **1024×1024 pixel PNG** with these requirements:

| Requirement | Detail |
|-------------|--------|
| **Resolution** | 1024×1024px |
| **Format** | PNG (no JPEG, no alpha channel issues) |
| **Color Space** | sRGB |
| **Corners** | Square — Apple applies the corner mask automatically |
| **Transparency** | None — use a solid background |
| **File Size** | Under 4MB |

## Design Tips

- Keep the icon simple and recognizable at small sizes
- Avoid text — it becomes illegible at small sizes
- Use bold, contrasting colors
- Test at 40×40px (smallest Home Screen size) to make sure it's recognizable
- The icon should represent: AI + tools + trades — consider a wrench/spanner with an AI spark or a hard hat with a circuit pattern

## How to Generate All Required Sizes (Optional but Recommended)

Xcode can generate all required sizes from your 1024×1024 source. Just provide the single 1024×1024 image and check **"iOS — All Sizes"** in the AppIcon asset catalog.

If you want to generate them manually, use a tool like:
- [IconKitchen](https://icon.kitchen) (free, web-based)
- [App Icon Generator](https://appicon.co) (free, web-based)
- Photoshop/Figma with an iOS icon template

## Current State

The placeholder icon (`AppIcon-512@2x.png`) is a generic Capacitor default. **Replace it before submitting to the App Store** — Apple rejects apps with placeholder icons.
