# Driver Documentation Contribution Guide

This guide explains how to add new driver documentation, including details on file structure, image placement, and how custom CSS ensures consistent styling. This project aims to provide a comprehensive and easily navigable resource for various drivers.

## 1. Adding New Drivers

Each driver entry consists of two files: a Markdown (`.md`) file for the main content and a YAML (`.yaml`) file for metadata.

### File Structure

All driver documentation resides within `src/content/docs/`, organized by category, manufacturer, and driver. Each driver has its own directory containing all documentation and images:

```
src/content/docs/
├── mounts/                           # Category (lowercase slug)
│   └── sky-watcher/                  # Manufacturer (lowercase slug)
│       └── eqmod/                    # Driver (lowercase slug)
│           ├── eqmod.yaml           # Driver metadata
│           ├── eqmod.md             # Driver documentation
│           ├── eqmod.webp           # Thumbnail image
│           └── images/              # Additional screenshots (optional)
│               ├── connection.webp
│               └── features.webp
├── dustcaps/
│   └── deep-sky-dad/
│       └── deep-sky-dad-fp1/
│           ├── deep-sky-dad-fp1.yaml
│           ├── deep-sky-dad-fp1.md
│           ├── deep-sky-dad-fp1.webp
│           └── images/              # All additional images
│               └── operation.webp
└── ...
```

**Directory Naming Convention:**
- Use **lowercase** with **hyphens** for directory names (e.g., `sky-watcher`, `deep-sky-dad`, `ikarus-technologies`)
- Category directories: `mounts`, `cameras`, `dustcaps`, `lightboxes`, etc.
- Manufacturer directories: `sky-watcher`, `deep-sky-dad`, `zwo`, `qhyccd`, etc.
- Driver directories: `eqmod`, `deep-sky-dad-fp1`, etc.
- Driver filenames must match directory: `eqmod/eqmod.md`, `deep-sky-dad-fp1/deep-sky-dad-fp1.md`, etc.

**Supported INDI Driver Categories:**
- `adaptive-optics` - Adaptive Optics systems
- `auxiliaries` - Auxiliary devices
- `cameras` - CCD/CMOS cameras
- `domes` - Observatory domes
- `dustcaps` - Dust cap controllers
- `filter-wheels` - Filter wheel controllers
- `focusers` - Focuser controllers
- `lightboxes` - Flat panel/light box devices
- `mounts` - Telescope mounts
- `power-controllers` - Power distribution and control
- `rotators` - Camera rotators
- `weather-stations` - Weather monitoring stations

### YAML Metadata File

The YAML file contains driver metadata with both human-friendly display names and additional information:

```yaml
# Display Names (Human-Friendly - Required)
driver_name: EQMod Mount
manufacturer_name: Sky Watcher

# Categories (Required - can be multiple)
categories:
  - mounts

# Additional Metadata (Optional)
website: www.indlib.org
executable: indi_eqmod_telescope
platforms: Linux, BSD, OSX
author: Jean-Luc Levaire
version: 1.0
```

**Key Fields:**
- `driver_name`: Human-friendly driver name (displayed on the website)
- `manufacturer_name`: Human-friendly manufacturer name (e.g., "Sky Watcher", "Ikarus Technologies")
- `categories`: Array of category slugs the driver belongs to (e.g., `["mounts"]`, `["dustcaps", "lightboxes"]`)
- Additional fields: You can add any custom metadata that will be displayed in the driver information sidebar

**Multi-Category Support:**
Drivers can belong to multiple categories by specifying multiple category slugs in the `categories` array. For example, a device that functions as both a dust cap and a light box:

```yaml
driver_name: Deep Sky Dad FP1
manufacturer_name: Deep Sky Dad
categories:
  - dustcaps
  - lightboxes
```

This driver will appear in both the "Dust Caps" and "Light Boxes" categories in the sidebar navigation, with both entries linking to the same driver page.

**Important:** The human-friendly names will be automatically looked up from the central category configuration, while the directory structure and category slugs use SEO-friendly formats for URLs.

### Markdown Documentation File

The Markdown file contains the main driver documentation:

```markdown
---
title: EQMod Mount
categories: ["mounts"]
description: The EQMod driver for Sky Watcher mounts.
thumbnail: ./eqmod.webp
---

# EQMod Driver

This is the documentation for the EQMod driver...

## Features

![Features](./images/features.webp)

* Feature 1
* Feature 2

## Installation

Installation instructions...
```

**Frontmatter Fields:**
- `title`: The driver name (should match `driver_name` in YAML)
- `categories`: Array of category slugs matching those in the YAML file (e.g., `["mounts"]` or `["dustcaps", "lightboxes"]`)
- `description`: Brief description for SEO and previews
- `thumbnail`: (Optional) Relative path to the driver's thumbnail image (e.g., `./eqmod.webp`)

**Multi-Category Example:**
```markdown
---
title: Deep Sky Dad FP1
categories: ["dustcaps", "lightboxes"]
description: A flat panel for both dust cap and light box functionality.
thumbnail: ./deep-sky-dad-fp1.webp
---
```

**Image References:**
- Use **relative paths** for all images: `./image.webp` or `./images/image.webp`
- Never use absolute paths like `/images/...`

## 2. Image Guidelines

All driver images are co-located with their documentation in the driver's directory. This makes it easy for contributors to submit everything in one place.

### Driver Images Structure

**Path Structure:**
```
src/content/docs/<category>/<manufacturer>/<driver>/
├── <driver>.webp              # Thumbnail (required)
└── images/                    # All additional images (optional)
    ├── feature1.webp
    ├── screenshot1.webp
    └── diagram1.webp
```

**Example:**
```
src/content/docs/mounts/sky-watcher/eqmod/
├── eqmod.webp                 # Thumbnail
└── images/                    # All screenshots and diagrams
    ├── connection.webp
    ├── features.webp
    └── options.webp
```

**Requirements:**
- **Format**: Must be `.webp`
- **Thumbnail**: Named same as driver (e.g., `eqmod.webp`) at root of driver directory
- **Additional Images**: All other images must be in the `images/` subdirectory
- **Recommended Size**: 200x200 pixels for thumbnails, larger for screenshots
- **References**: Use relative paths in markdown:
  - Thumbnail: `./eqmod.webp`
  - Other images: `./images/features.webp`

### Shared Assets (Manufacturer Logos & Category Icons)

These are stored in `public/images/` as they are shared across multiple drivers:

**Manufacturer Logos:**
```
public/images/manufacturers/<manufacturer-slug>.webp
```

**Examples:**
```
public/images/manufacturers/sky-watcher.webp
public/images/manufacturers/deep-sky-dad.webp
```

**Category Icons:**
```
public/images/categories/<category-slug>.webp
```

**Examples:**
```
public/images/categories/mounts.webp
public/images/categories/cameras.webp
```

**Requirements:**
- **Format**: Must be `.webp`
- **Recommended Size**: 200x200 pixels

## 3. URL Structure

The site automatically generates clean, SEO-friendly URLs based on the directory structure:

**Directory Structure:**
```
src/content/docs/mounts/sky-watcher/eqmod/eqmod.md
```

**Generated URL:**
```
https://drivers.indilib.org/mounts/sky-watcher/eqmod
```

**Display Names:**
The website will show "Mounts" > "Sky Watcher" > "EQMod Mount" using the human-friendly names from your YAML file, while the URL remains clean and SEO-friendly.

## 4. Markdown Features

This project supports GitHub-flavored Markdown, including special callout blocks for highlighting important information.

### Callout Blocks

You can use various types of callout blocks to emphasize different kinds of information:

```markdown
> [!NOTE]
> This is a note with general information.

> [!TIP]
> This is a helpful tip.

> [!IMPORTANT]
> This is important information.

> [!WARNING]
> This is a warning about potential issues.

> [!CAUTION]
> This is a critical caution or serious warning.
```

These callouts are rendered with custom styling to draw attention to specific content.

## 5. Step-by-Step Contribution Process

### Adding a New Driver

1. **Create the driver directory:**
   ```bash
   mkdir -p src/content/docs/<category>/<manufacturer>/<driver>/images
   ```
   Example:
   ```bash
   mkdir -p src/content/docs/mounts/sky-watcher/eqmod/images
   ```

2. **Create the YAML metadata file:**
   ```bash
   touch src/content/docs/mounts/sky-watcher/eqmod/eqmod.yaml
   ```
   Add your metadata with human-friendly names and categories:
   ```yaml
   driver_name: EQMod Mount
   manufacturer_name: Sky Watcher
   categories:
     - mounts
   website: www.indilib.org
   executable: indi_eqmod_telescope
   # ... other fields
   ```

3. **Create the Markdown documentation file:**
   ```bash
   touch src/content/docs/mounts/sky-watcher/eqmod/eqmod.md
   ```
   Add your documentation with frontmatter (categories must match YAML):
   ```markdown
   ---
   title: EQMod Mount
   categories: ["mounts"]
   description: Driver description here
   thumbnail: ./eqmod.webp
   ---
   
   ## Features
   ![Features](./images/features.webp)
   
   Your documentation content...
   ```

4. **Add images to the driver directory:**
   - Thumbnail: `src/content/docs/mounts/sky-watcher/eqmod/eqmod.webp`
   - Screenshots: `src/content/docs/mounts/sky-watcher/eqmod/images/features.webp`
   - If manufacturer logo doesn't exist: `public/images/manufacturers/sky-watcher.webp`

5. **Convert images to WebP format:**
   ```bash
   # Using cwebp (recommended)
   cwebp -q 80 input.png -o output.webp
   
   # Using ImageMagick
   convert input.png -quality 80 output.webp
   ```

6. **Test locally:**
   ```bash
   npm run dev
   ```
   Visit `http://localhost:4321/mounts/sky-watcher/eqmod`

7. **Submit a pull request** with your changes.

### Adding a Multi-Category Driver

For drivers that belong to multiple categories (e.g., a device that functions as both a dust cap and light box):

1. **Create the driver directory in the PRIMARY category:**
   ```bash
   mkdir -p src/content/docs/dustcaps/deep-sky-dad/deep-sky-dad-fp1/images
   ```

2. **Create the YAML metadata file with multiple categories:**
   ```bash
   touch src/content/docs/dustcaps/deep-sky-dad/deep-sky-dad-fp1/deep-sky-dad-fp1.yaml
   ```
   ```yaml
   driver_name: Deep Sky Dad FP1
   manufacturer_name: Deep Sky Dad
   categories:
     - dustcaps
     - lightboxes
   website: www.deepskydad.com
   executable: indi_deepskydad_fp1
   # ... other fields
   ```

3. **Create the Markdown file with matching categories:**
   ```bash
   touch src/content/docs/dustcaps/deep-sky-dad/deep-sky-dad-fp1/deep-sky-dad-fp1.md
   ```
   ```markdown
   ---
   title: Deep Sky Dad FP1
   categories: ["dustcaps", "lightboxes"]
   description: A flat panel that functions as both dust cap and light box
   thumbnail: ./deep-sky-dad-fp1.webp
   ---
   
   # Deep Sky Dad FP1
   
   This device serves dual purposes...
   ```

4. **Add images:**
   - Thumbnail: `src/content/docs/dustcaps/deep-sky-dad/deep-sky-dad-fp1/deep-sky-dad-fp1.webp`
   - Screenshots: `src/content/docs/dustcaps/deep-sky-dad/deep-sky-dad-fp1/images/operation.webp`

5. **Result:**
   - The driver appears in both "Dust Caps" and "Light Boxes" sidebar categories
   - Both entries link to: `/dustcaps/deep-sky-dad/deep-sky-dad-fp1`
   - Metadata displays: "Categories: Dust Caps, Light Boxes"

## 6. Important Notes

- **Consistency**: Always use lowercase with hyphens for directory and file names
- **Human-Friendly Names**: Use proper capitalization and spacing in YAML metadata
- **Images**: Convert images to `.webp` format for optimal performance
- **Documentation**: Write clear, comprehensive documentation with examples
- **Testing**: Always test your contribution locally before submitting

## Contribution

We welcome contributions from the community! If you have new driver documentation to add or improvements to existing ones, please follow this guide. Your contributions help make this resource more valuable for everyone.

For questions or issues, please open an issue on the GitHub repository.
