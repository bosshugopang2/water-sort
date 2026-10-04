# Flutter Web Conversion Guide for Water Sort

This guide will help you convert the Water Sort Flutter mobile app to a web app.

## Prerequisites

You need:
- Flutter SDK 3.12.2 or later
- A terminal/command line
- Git

## Quick Start Commands

Run these commands in order:

```bash
# Enable web support in Flutter
flutter config --enable-web

# Create web platform files
flutter create --platforms=web .

# Install dependencies
flutter pub get

# Run locally (choose one)
flutter run -d chrome
# OR
flutter run -d web-server

# Build for production
flutter build web --release
```

## What Gets Created

After `flutter create --platforms=web .`, a new `web/` folder appears with:
- `index.html` - Main HTML entry point
- `manifest.json` - Web app manifest
- `styles.css` - Base styling

## Run Locally

To test the app locally before building:

```bash
flutter run -d chrome
```

This opens the app in Chrome at `localhost:52682` (or similar port).

To use a different port:
```bash
flutter run -d web-server --web-port 8080
```

Then open `http://localhost:8080` in any browser.

## Build for Production

```bash
flutter build web --release
```

This creates optimized production files in `build/web/` ready for deployment.

## Deployment Options

### Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

### Netlify
```bash
npm install -g netlify-cli
netlify deploy --prod --dir=build/web
```

### GitHub Pages
1. Build the app
2. Copy `build/web` contents to `docs/` folder
3. Enable GitHub Pages in repo settings

### Vercel
```bash
npm install -g vercel
vercel --prod
```

## Known Issues & Fixes

### Image Picker Not Available on Web
The `image_picker` package only works on mobile. If the app uses custom background images:

In `lib/ui/features/home/views/customization_view.dart`, wrap image picker code:

```dart
import 'package:flutter/foundation.dart';

if (!kIsWeb) {
  // image_picker code here
}
```

### Hive Storage on Web
Hive stores data in browser localStorage automatically. No changes needed, but note:
- Data persists across browser sessions
- Clearing browser cache clears game progress
- Each browser/device has separate storage

### Audio Issues
Flame audio should work on web. If issues occur:
- Ensure `assets/audio/` is in `pubspec.yaml`
- Test with simple WAV/MP3 files first
- Check browser console for audio errors

## Troubleshooting

### "Web not enabled"
```bash
flutter config --enable-web
flutter config  # verify enable-web: true appears
```

### "Chrome not found"
```bash
flutter run -d web-server
# Then open http://localhost:8080
```

### "Assets not loading"
```bash
flutter clean
flutter pub get
flutter run -d chrome
```

### "Hive box errors"
```bash
flutter run -d chrome --web-unsafe
# This disables some web security for testing
```

### "Slow performance"
Always test with `--release`:
```bash
flutter run -d chrome --release
```

Debug mode is slow. Release mode is production-ready.

## Testing

Test in multiple browsers:
- Chrome
- Firefox
- Safari
- Edge

Test on mobile browsers:
- Open your deployed URL on phone
- Verify touch interactions work
- Check performance

## Next Steps

1. Run `flutter create --platforms=web .`
2. Run `flutter pub get`
3. Run `flutter run -d chrome` to test locally
4. Fix any errors (see Troubleshooting)
5. Run `flutter build web --release`
6. Deploy using one of the options above

## Support

- Flutter Web Docs: https://flutter.dev/docs/get-started/web
- Flame Docs: https://flame-engine.org
- Riverpod Docs: https://riverpod.dev
