# TradeMateAI iOS App

Native iOS wrapper for the TradeMateAI web app using Capacitor. Loads the live web app (https://f058ce2575a5daf11ba9a52037f5f76c.ctonew.app) inside a native WebView, ready for App Store submission.

## Prerequisites (on your Mac)

1. **Xcode** — Install from the Mac App Store (requires macOS Ventura or later).
2. **Node.js** — Install via [nodejs.org](https://nodejs.org) (v18+), or use Homebrew: `brew install node`
3. **Apple Developer Account** — Enrolled at $79/year. Sign up at [developer.apple.com](https://developer.apple.com).
4. **App Store Connect** — Make sure you can sign in at [appstoreconnect.apple.com](https://appstoreconnect.apple.com).

## Quick Start

```bash
# 1. Install dependencies
cd ios-app
npm install

# 2. Sync web assets to the iOS project
npm run sync

# 3. Open in Xcode
npm run open
```

## Step-by-Step: First Build

### 1. Install Node dependencies
```bash
cd ios-app
npm install
```

### 2. Sync web assets to iOS
```bash
npm run sync
```
This copies the `www/` directory into the iOS project and updates Capacitor plugins.

### 3. Open in Xcode
```bash
npm run open
```
This opens `ios/App/App.xcworkspace` in Xcode.

### 4. Configure Signing in Xcode
- In Xcode, select the **App** target in the project navigator.
- Go to the **Signing & Capabilities** tab.
- Check **"Automatically manage signing"**.
- Select your **Apple Developer team** from the dropdown.
- Xcode will handle provisioning profiles automatically.

### 5. Choose a simulator or device
Select a target from the scheme dropdown in the Xcode toolbar:
- **iPhone 16 Pro Simulator** (for testing)
- **Any iOS device** (for archive/release)

### 6. Build & Run
Press **Cmd+R** to build and run on the simulator.
Press **Cmd+B** to build only (useful for checking for errors).

## Project Structure

```
ios-app/
├── capacitor.config.json    # Capacitor config (app name, bundle ID, server URL)
├── package.json             # Node scripts (sync, open, build:sync)
├── www/                     # Minimal web assets (placeholder; app loads from server.url)
├── ios/
│   └── App/
│       ├── App.xcworkspace          # Open this in Xcode
│       └── App/
│           ├── AppDelegate.swift    # Native app delegate
│           ├── Info.plist           # iOS permissions (camera, photo library)
│           ├── Assets.xcassets/     # App icon and splash screen
│           └── Base.lproj/          # Launch screen and main storyboard
└── README.md
```

## How It Works

This Capacitor app uses `server.url` to load the live web app. The WebView loads `https://f058ce2575a5daf11ba9a52037f5f76c.ctonew.app` on launch. Any updates to the web app are instantly available in the iOS app — no App Store resubmission required for web changes.

## App Store Submission

### 1. Prepare Your App Icon
Replace the placeholder icon with your 1024×1024px PNG:
```
ios/App/App/Assets.xcassets/AppIcon.appiconset/AppIcon-512@2x.png
```
**Requirements:** 1024×1024px, PNG, no transparency, no rounded corners (Apple applies the mask).

See `ICON-NOTES.md` for detailed icon guidelines.

### 2. Set Version & Build Number
In Xcode, under the **App** target → **General**:
- **Version** (e.g., `1.0.0`) — shown on the App Store
- **Build** (e.g., `1`) — incremented for each submission

### 3. Create an App Record in App Store Connect
1. Go to [appstoreconnect.apple.com](https://appstoreconnect.apple.com)
2. Click **My Apps** → **+** → **New App**
3. Fill in:
   - **Platform:** iOS
   - **Name:** TradeMateAI
   - **Primary Language:** English
   - **Bundle ID:** `ai.trademate.app`
   - **SKU:** `ai.trademate.app` (or any unique string)
   - **User Access:** Full Access

### 4. Complete App Store Listing
In App Store Connect, fill out:
- **App Description:** "AI-powered admin assistant for tradespeople — create quotes by describing the job. Take photos, generate professional PDF quotes, and manage your trade business from your phone."
- **Keywords:** tradesman, builder, quote, invoice, ai, assistant, plumber, electrician, construction
- **Support URL:** Your website URL
- **Privacy Policy URL:** Link to your privacy policy
- **Category:** Business (primary), Productivity (secondary)
- **Rating:** Select 4+ (no objectionable content)

### 5. Screenshots (Required)
Submit screenshots for each required device size:
- **6.7"** (iPhone 16 Pro Max): 1290×2796px
- **6.1"** (iPhone 16 Pro): 1179×2556px  
- **5.5"** (iPhone 8 Plus): 1242×2208px

You can use the simulator's screenshot feature (Cmd+S) or the screenshot tool in Xcode → **Window → Devices and Simulators**.

### 6. Archive & Upload
1. In Xcode, set the scheme to **"Any iOS Device (arm64)"**
2. Select **Product → Archive** from the menu
3. In the Organizer window, select the archive and click **"Distribute App"**
4. Choose **"App Store Connect"** → **"Upload"**
5. Follow the prompts to upload the binary

### 7. Submit for Review
1. In App Store Connect, open your app
2. Select the uploaded build under **"iOS App"** → **"Build"**
3. Complete the **"App Review Information"** section:
   - **Sign-in required?** No (unless you add auth later)
   - **Contact info:** Your name, phone, email
4. Click **"Submit for Review"**

### App Review Tips
- Apple typically reviews within 24–48 hours.
- Ensure all links in the app work (web app must be live and functional).
- Make sure the app doesn't crash on launch.
- Your privacy policy must be accessible at the URL you provide.
- Camera/photo permissions must have clear, descriptive strings (already configured in Info.plist).

## Updating the Web App

Since this Capacitor app loads the live URL, you only need to resubmit to the App Store when you:
- Change the app version or build number
- Add/remove native permissions
- Change the bundle ID or app name
- Update the app icon

**To push web-only changes:** Just deploy the website as usual — no App Store review needed.

## Common Issues

### "Signing requires a development team"
You need an Apple Developer account. Sign in to Xcode with your Apple ID in **Xcode → Settings → Accounts**, and ensure you've enrolled in the developer program.

### "No provisioning profile found"
Make sure **Automatically manage signing** is checked in the Signing & Capabilities tab.

### "Invalid Bundle ID"
The bundle ID `ai.trademate.app` must be registered in your Apple Developer account. If it's taken, change it in `capacitor.config.json`, run `npm run sync`, and create a matching App ID in App Store Connect.

### Simulator can't load the web app
Ensure the URL in `capacitor.config.json` (`server.url`) is accessible from the simulator. Test by opening Safari in the simulator and navigating to the URL.

## Scripts Reference

| Command | Description |
|---------|-------------|
| `npm run sync` | Copy web assets and sync Capacitor plugins to iOS |
| `npm run open` | Open the Xcode project |
| `npm run sync:open` | Sync, then open Xcode |
| `npm run build:sync` | Build the web app, then sync to iOS |
