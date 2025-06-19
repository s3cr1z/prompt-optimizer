# Lingo.Dev AI Localization Setup

This project uses [Lingo.Dev](https://lingo.dev) AI-powered localization to automatically manage translations for multiple languages.

## 🚀 Features

- **Automated Translation**: AI-powered translations for multiple languages
- **Smart Context Awareness**: Understands your project context for better translations
- **Pull Request Integration**: Creates PRs for translation updates
- **Multi-Format Support**: Handles TypeScript i18n files, JSON locales, and Markdown docs

## 📁 Localized Files

The following files are automatically localized:

### UI Components
- `packages/ui/src/i18n/locales/*.ts` - Vue.js i18n translation files
- Currently supports: Chinese (zh-CN), English (en-US)

### Browser Extension
- `packages/extension/public/_locales/*/messages.json` - Chrome extension locales
- Currently supports: Chinese (zh_CN), English (en)

### Documentation
- `README*.md` - Project documentation
- `docs/**/*.md` - All documentation files

## ⚙️ Configuration

The localization behavior is configured in `lingo.config.json`:

```json
{
  "version": "1.0",
  "localization": {
    "source_language": "en-US",
    "target_languages": ["zh-CN", "ja-JP", "ko-KR", "es-ES", "fr-FR", "de-DE"],
    "file_patterns": [
      "packages/ui/src/i18n/locales/**/*.ts",
      "packages/extension/public/_locales/**/*.json",
      "README*.md",
      "docs/**/*.md"
    ]
  }
}
```

### Supported Target Languages

- �� **Chinese (zh-CN)** - Auto-generated
- 🇯🇵 **Japanese (ja-JP)** - Auto-generated
- 🇰🇷 **Korean (ko-KR)** - Auto-generated  
- 🇪🇸 **Spanish (es-ES)** - Auto-generated
- 🇫🇷 **French (fr-FR)** - Auto-generated
- 🇩🇪 **German (de-DE)** - Auto-generated

## 🔄 Workflow Triggers

The localization workflow runs automatically when:

1. **Push to main/master**: Changes to localization files or documentation
2. **Pull Requests**: For review of localization changes
3. **Manual Trigger**: Via GitHub Actions interface

### Trigger Paths
- `packages/ui/src/i18n/locales/**` - UI translation files
- `packages/extension/public/_locales/**` - Extension locales
- `**.md` - Markdown documentation
- `docs/**` - Documentation folder

## 📝 How It Works

1. **Source Detection**: Lingo.Dev scans configured file patterns
2. **Context Analysis**: AI analyzes your codebase for translation context
3. **Translation Generation**: Creates contextually appropriate translations
4. **Pull Request**: Submits changes via automated PR
5. **Review & Merge**: Review AI-generated translations before merging

## 🛠️ Customization

To customize the localization:

1. **Edit `lingo.config.json`** to modify:
   - Target languages
   - File patterns
   - Translation settings
   - Output preferences

2. **Update `.github/workflows/localization.yml`** to modify:
   - Trigger conditions
   - Workflow timing
   - Additional steps

## 📋 Best Practices

- **Review AI Translations**: Always review before merging
- **Maintain Context**: Keep translation keys descriptive
- **Test Locally**: Verify translations work in your application
- **Consistent Terminology**: Use project-specific terms consistently

## 🚫 Excluded Files

The following are automatically excluded:
- `node_modules/**`
- `dist/**`, `build/**`
- Test files (`*.test.ts`, `*.spec.ts`)

## 🔧 Manual Operation

To run localization manually:

1. Go to **Actions** tab in GitHub
2. Select **Lingo.Dev AI Localization** workflow  
3. Click **Run workflow**
4. Select branch and click **Run workflow**

## 📚 Resources

- [Lingo.Dev Documentation](https://lingo.dev/docs)
- [GitHub Action Repository](https://github.com/lingodotdev/lingo.dev)
- [Project i18n Guide](packages/ui/src/i18n/README.md)
