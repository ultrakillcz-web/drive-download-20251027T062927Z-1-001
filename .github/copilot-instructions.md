# Copilot Instructions - Android APK Versions Repository

## Project Overview

This repository contains different versions of an Android application named "Documento de 👉👉Léo👈👈". These APKs represent various builds and updates of the same application, likely part of a larger development project with iterative releases for Android and potentially macOS platforms.

## Repository Structure

```
.
├── .git/                                          # Git repository metadata
├── Documento de 👉👉Léo👈👈.apk                   # Base APK (~4MB)
├── Documento de 👉👉Léo👈👈(1).apk               # Variant 1 (~4MB)
├── Documento de 👉👉Léo👈👈(2).apk               # Variant 2 (~3.6MB)
├── Documento de 👉👉Léo👈👈(3).apk               # Variant 3 (~4MB)
├── Documento de 👉👉Léo👈👈(4).apk               # Variant 4 (~3.6MB)
├── Documento de 👉👉Léo👈👈(5).apk               # Variant 5 (~3.6MB)
└── Documento de 👉👉Léo👈👈(6).apk               # Variant 6 (~4MB)
```

## Key Patterns and Conventions

### File Naming Convention
- Base format: `Documento de 👉👉Léo👈👈.apk`
- Variants: Numbered in parentheses `(1)`, `(2)`, etc.
- All files use Portuguese naming with emoji indicators

### APK Characteristics
- File sizes range from ~3.6MB to ~4MB
- Different versions represent iterative builds of the same application
- Size variations (~400KB difference) indicate feature additions or optimizations between versions
- All versions target Android platform with potential cross-platform compatibility

## Working with APK Files

### Analysis Commands
```powershell
# List all APKs with sizes
Get-ChildItem *.apk | Select-Object Name, Length | Format-Table

# Check APK metadata (requires Android SDK tools)
aapt dump badging "Documento de 👉👉Léo👈👈.apk"

# Extract APK contents for analysis
# Note: APK files are ZIP archives
Expand-Archive "Documento de 👉👉Léo👈👈.apk" -DestinationPath "./extracted/"
```

### Common Operations
- **Version Comparison**: Compare APK manifests to identify version differences and feature changes
- **Build Analysis**: Extract and examine AndroidManifest.xml, resources, and DEX files to understand evolution
- **Cross-Platform Testing**: Test functionality across different Android versions and potentially macOS if applicable
- **Integration Testing**: Ensure compatibility with other components in the larger project ecosystem

## Development Workflow

### Adding New APKs
1. Follow existing naming convention with sequential numbering (e.g., `(7)`, `(8)`)
2. Test APK functionality before committing new versions
3. Document version changes and new features in commit messages
4. Maintain compatibility with existing project components

### Repository Management
- Part of a larger development ecosystem - consider integration points
- APK versions may correspond to different feature branches or development phases
- Coordinate releases with related repositories in the project
- Track version history for rollback capabilities

## External Dependencies
- Android SDK tools (aapt, adb) for APK analysis
- APK analysis tools for security scanning or reverse engineering
- Android emulator/device for testing installations

## Security Considerations
- APK files should be scanned for malware before distribution
- Verify APK signatures and certificates
- Consider using APK signing tools for verification

## Integration with Larger Project
- This repository is part of a broader development project
- APK versions may be built from source code in related repositories
- Consider cross-repository dependencies and version synchronization
- May require coordination with other project components for full functionality

## Notes
- Repository focuses on versioned APK builds rather than source code
- Each APK represents a milestone or iteration in the application development
- Consider testing across Android and potential macOS compatibility layers