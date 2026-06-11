# Test Documents

This directory contains test documents to verify the thesis title page template modifications.

## Test Files

### test-simple.md
A complete thesis document demonstrating all new template variables:
- `department` - Program/department name
- `assignment` - Thesis type
- `supervisor` - Primary supervisor
- `cosupervisor` - List of co-supervisors
- `titlepage-logo` - University logo at top

**Purpose**: Verify all new thesis-specific features work correctly.

### test-backward-compat.md
A standard document using only original Eisvogel variables without any thesis-specific fields.

**Purpose**: Ensure backward compatibility - documents without thesis variables should render identically to the original template.

## Compilation

To compile a test document:

```bash
cd test-thesis
pandoc "test-simple.md" -o "test-simple.pdf" --from markdown --template "../dist/eisvogel.latex" --syntax-highlighting idiomatic
```

## Expected Results

### test-simple.pdf
Should display:
- University logo centered at top
- "Infection, Inflammation and Immunity PhD:" below logo
- "Final Thesis" below that
- Large title after vertical space
- "Candidate: Alexander I.R. Jackson"
- "Primary Supervisor: Prof M.P.W. Grocott"
- "Co-Supervisors: Dr. First Co-supervisor, Dr. Second Co-supervisor"
- "February 2025" at bottom

### test-backward-compat.pdf
Should display:
- Colored rule at top
- Title and subtitle
- Author name
- Date
- No thesis-specific labels or fields
- Layout identical to original Eisvogel template

## Verification Checklist

- [x] Thesis document compiles without errors
- [x] Standard document compiles without errors
- [x] Logo appears at top (not bottom)
- [x] All new labels display correctly
- [x] Multiple co-supervisors format as comma-separated list
- [x] Spacing matches reference design
- [x] Backward compatibility maintained
