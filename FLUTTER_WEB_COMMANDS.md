# Flutter Web Conversion - Quick Reference

## Enable Web Support

```bash
flutter config --enable-web
```

## Create Web Platform

```bash
flutter create --platforms=web .
```

This creates the `web/` folder with:
- `index.html` - Entry point
- `manifest.json` - PWA configuration
- `styles.css` - Base styles

## Install Dependencies

```bash
flutter pub get
```

## Run Locally in Browser

### Chrome
```bash
flutter run -d chrome
```

### Any Browser (Web Server)
```bash
flutter run -d web-server
```

Then open `http://localhost:8080` in your browser.

### Custom Port
```bash
flutter run -d web-server --web-port 9000
```

## Build for Production

```bash
flutter build web --release
```

Output is in `build/web/` - ready to deploy.

## Deploy to Firebase Hosting

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
# Select project, use 'build/web' as public directory
firebase deploy
```

## Deploy to Netlify

```bash
netlify deploy --prod --dir=build/web
```

Or drag `build/web` folder to https://app.netlify.com/drop

## Deploy to GitHub Pages

1. Build: `flutter build web --release`
2. Copy `build/web` → `docs/`
3. Push to GitHub
4. Enable Pages in repo settings (use `docs/` folder)

## Deploy to Vercel

```bash
npm install -g vercel
vercel --prod
```

## Troubleshooting

### Clear cache
```bash
flutter clean
flutter pub get
```

### Check Flutter config
```bash
flutter config
```

Should show `enable-web: true`

### Debug mode (slow)
```bash
flutter run -d chrome
```

### Release mode (fast)
```bash
flutter run -d chrome --release
```

## Files Modified

- `web/index.html` - HTML entry point
- `web/manifest.json` - PWA config
- `web/styles.css` - CSS base
- `.gitignore` - Updated for web builds
- `WEB_SETUP.md` - Detailed guide
