# Template Modifications for Thesis Title Pages

## Summary

This is a customized version of the Eisvogel pandoc LaTeX template with enhanced support for academic thesis title pages (PhD, Master's, Honours). The modifications maintain full backward compatibility with the original template.

## Changes Made

### 1. Modified Files

#### `template-multi-file/eisvogel-title-page.latex`
Complete rewrite of the title page layout to support thesis-specific requirements:

**Key Changes:**
- **Logo positioning**: Moved from bottom to top of page, centered
- **New metadata sections**: Added support for department, assignment/thesis type, and supervisors
- **Improved spacing**: Replaced arbitrary negative spacing with semantic LaTeX commands (`\vspace`, `\vfill`)
- **Enhanced labels**: Added "Candidate:", "Primary Supervisor:", and "Co-Supervisors:" labels
- **Flexible layout**: Uses `\vfill` for responsive vertical spacing

**Layout Structure (top to bottom):**
1. Colored horizontal rule (existing)
2. University logo (centered, repositioned from bottom)
3. Department/Program name (e.g., "Infection, Inflammation and Immunity PhD:")
4. Thesis type (e.g., "Final Thesis")
5. Flexible space (`\vfill`)
6. Title (large, bold)
7. Subtitle (if present)
8. Fixed spacing
9. Candidate: [Author name]
10. Primary Supervisor: [Name]
11. Co-Supervisors: [Names] (if present)
12. Date
13. Background graphic (optional, covers full page)

#### `tools/release.sh`
Added cleanup step to remove sed backup files created on macOS:
- Removes `eisvogel.latex''` and `eisvogel.beamer''` artifact files
- Prevents cluttering the dist directory with temporary files

#### `README.md`
Added comprehensive documentation for new template variables:

**New Variables Documented:**
- `department` - Department or program name
- `assignment` - Thesis type (PhD Thesis, Final Thesis, etc.)
- `supervisor` - Primary supervisor name
- `cosupervisor` - List of co-supervisor names

**New Example Section:**
- Added "Thesis Title Page" example showing complete YAML metadata setup
- Includes detailed explanation of layout and features

### 2. New Template Variables

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| `department` | String | Not shown | Department/program name displayed below logo |
| `assignment` | String | Not shown | Thesis type (e.g., "Final Thesis", "PhD Thesis") |
| `supervisor` | String | Not shown | Primary supervisor name with "Primary Supervisor:" label |
| `cosupervisor` | List | Not shown | Co-supervisor names with "Co-Supervisors:" label |

All new variables are **optional** and wrapped in conditional blocks to maintain backward compatibility.

### 3. Backward Compatibility

The template maintains **100% backward compatibility** with existing documents:
- All new variables are optional
- Documents without thesis variables render identically to original template
- Existing `titlepage`, `titlepage-logo`, `logo-width`, and other variables work unchanged
- No breaking changes to existing functionality

### 4. Testing

Created test documents to verify:
- ✅ Thesis document with all new fields compiles correctly
- ✅ Standard document (no thesis fields) compiles identically to original
- ✅ Logo positioning moved to top
- ✅ Multiple co-supervisors format correctly
- ✅ All new labels display properly
- ✅ Spacing follows reference image proportions

Test files created in `test-thesis/`:
- `test-simple.md` - Full thesis example with all new fields
- `test-backward-compat.md` - Standard document for compatibility testing

## Usage Example

### Thesis Title Page

```yaml
---
title: "Your Thesis Title Here"
author: "Your Name"
date: "Month Year"
titlepage: true
titlepage-logo: "university-logo.png"
logo-width: 60mm
titlepage-background: "background.pdf"
titlepage-rule-color: "006699"
titlepage-rule-height: 4
titlepage-text-color: "5F5F5F"
department: "Department or Program Name:"
assignment: "Final Thesis"
supervisor: "Prof. Supervisor Name"
cosupervisor:
  - "Dr. First Co-supervisor"
  - "Dr. Second Co-supervisor"
lang: "en"
---

# Chapter One

Your content begins here...
```

### Compile Command

```bash
pandoc document.md -o document.pdf --from markdown --template eisvogel --syntax-highlighting idiomatic
```

## Building the Template

To rebuild the single-file template from the multi-file source:

```bash
./tools/release.sh version-name
```

This creates:
- `dist/eisvogel.latex` - Compiled single-file template
- `dist/eisvogel.beamer` - Beamer presentation template
- Distribution archives in `dist/`

## Files Modified

1. `template-multi-file/eisvogel-title-page.latex` - Title page layout
2. `README.md` - Documentation for new variables and examples
3. `tools/release.sh` - Added cleanup step for sed artifacts on macOS

## Files Added

1. `MODIFICATIONS.md` - This file
2. `test-thesis/` - Test documents directory
   - `test-simple.md` - Thesis example
   - `test-backward-compat.md` - Compatibility test
   - Compiled PDFs

## Design Decisions

1. **All left-aligned**: Following the reference design, all text is left-aligned
2. **Logo centered**: University logo is centered at the top for prominence
3. **Semantic spacing**: Uses `\vspace{Xem}` and `\vfill` instead of arbitrary values
4. **List format for co-supervisors**: Comma-separated list rather than individual rows to save space
5. **Optional everything**: All thesis fields are optional to maintain flexibility

## Reference Implementation

Based on University of Southampton thesis title page requirements with:
- Top-positioned institutional branding
- Clear hierarchical information display
- Support for multiple supervisors
- Professional academic formatting
- Optional background graphics support

## Version Information

- **Base Template**: Eisvogel (pandoc LaTeX template)
- **Original Repository**: https://github.com/Wandmalfarbe/pandoc-latex-template
- **Customization**: airj-thesis-template
- **Date**: February 2025

## License

Maintains the original BSD 3-Clause License from the Eisvogel template.
