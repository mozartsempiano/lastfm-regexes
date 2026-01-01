# Last.fm Regex Edits

This file contains regular expression (regex) rules to automatically clean and standardize music metadata.

## Complete List of Changes

### 1. Album Cleanup

**Pattern**: `(.*) (?:- (Single|EP)|- EP|- Single|\[ ?Clean ?\](?: \[ ?Clean ?\])?|\[ ?[Ee]xplicit ?\])`
**Effect**: Removes suffixes like:

- `- Single`, `- EP`
- `[ Clean ]`, `[ Clean ][ Clean ]`
- `[ Explicit ]`, `[ explicit ]`

### 2. Artist Topic Cleanup

**Pattern**: `(.*) - Topic`
**Effect**: Removes `- Topic` suffix from artist names (common on YouTube channels)

### 3. Artist Collaboration Cleanup

**Pattern**: `^(.*) (?:e|&) (.+)$`
**Effect**: Removes collaborators indicated by `&` or `e` (keeps only the first artist)

### 4. Artist Comma Cleanup

**Pattern**: `^(.*), (?!the creator|the creator\b|the creator\.|the creator\s|the creator$)(.+)$`
**Effect**: Removes text after commas in artist names (except when it contains "the creator")

### 5. Track Cleanup (Comprehensive)

**Pattern**: Complex regex removing multiple suffixes
**Effect**: Removes:

- `- 2024 Vinyl LP` (year and format info)
- `(Unreleased)` (release status)
- `(2024 Remastered)`, `(Remastered 2024)` (remaster info)
- `(prod. Producer Name)` (producer credits)
- `(ft. Artist)`, `(feat. Artist)` (featuring credits)
- `(part. Info)` (part information)
- `(Official Video)`, `(Official Audio)`, `(Lyric Video)` (video types)
- `(Lyrics)` (lyrics indicator)
- `(Radio Edit)`, `- Radio Edit` (radio edits)
- `(Visualizer)` (visualizer videos)

### 6. Specific Artist Standardizations

#### Oliver Francis

**Patterns**: `Oliver`, `Oliver~`
**Standardized to**: `Oliver Francis`

#### Alex G

**Patterns**: `alex_g_offline`, `alexgoffline`, `alexgonline`, `(Sandy) Alex G`
**Standardized to**: `Alex G`

#### Lil Peep

**Patterns**: `☆LiL PEEP☆`, `lilpeep`
**Standardized to**: `Lil Peep`

#### Empire! Empire!

**Patterns**: `Empire! Empire!`, `empire empire`, `Empire Empire I was a Lonely Estate`, `Empire! Empire!(I Was A Lonely Estate)`
**Standardized to**: `Empire! Empire! (I Was a Lonely Estate)`

### 7. Specific Album Corrections

#### Lil Peep Album

**Patterns**: `LiL PEEP PART ONE`, `LiL PEEP, PART ONE`
**Standardized to**: `LiL PEEP; PART ONE`

#### Bladee Album Removal

**Effect**: Removes album `3STYLE` for artist `Bladee`

#### awakebutstillinbed Album

**Pattern**: `what people call low self‐esteem is really just seeing yourself the way that other people see you`
**Standardized to**: `what people call low self​-​esteem is really just seeing yourself the way that other people see you`
**Effect**: Fixes dash character encoding

### 8. Specific Track Corrections

#### Bladee Track

**Patterns**: `Fuck the world I'm still suicidal`, `Fuck the world I am still suicidal`
**Standardized to**: `Fuck the world im still suicidal`

#### Lil Peep Track

**Patterns**: `Benz Truck Pt. 2`, `Benz Truck Pt 2`, `Benz Truck 2`
**Standardized to**: `Benz Truck, Pt. 2`

## How It Works

Each rule contains:

- **search**: A regex pattern to find specific metadata
- **replace**: Replacement text, using capture groups (`$1`, `$2`, etc.)

Rules are applied sequentially to music metadata to automatically clean and standardize the information.
