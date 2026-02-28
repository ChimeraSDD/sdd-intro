name: "Text-to-Alpine.js GUI: Document Info Record - Search Documents"
description: |

## Purpose
Generate a complete, self-contained Alpine.js HTML page from a structured text description file. The output is a faithful visual and functional representation of the described screen layout.

## Core Principles
1. **Context is King**: The full screen description is embedded below — read it carefully
2. **Validation Loops**: Open the output HTML in a browser and verify each component visually
3. **Alpine.js Conventions**: Follow the CLAUDE.md style guide exactly (attribute ordering, logic out of DOM, extracted JS functions)
4. **Progressive Success**: Build structure first, add interactivity, then validate

---

## Goal
Read `docs/gui_description.txt` and produce `output/document-info-record.html` — a pixel-faithful, fully interactive Alpine.js single-page application representing the "Document Info Record - Search Documents" screen.

## Why
- **Business value**: Proves the text-to-GUI pipeline works end-to-end for screen layout descriptions
- **Integration**: This is the first output of the ChimeraSDD text-to-Alpine.js workflow
- **Problems solved**: Eliminates manual hand-coding of UI from design specs

## What

A self-contained `output/document-info-record.html` file that renders:

1. **Top navigation bar** — white background, logo (black box) left, 6 nav links right, user avatar circle
2. **Red alert banner** — full-width, dark red (#8b1a1a), centered white text "You are in test system"
3. **Page title** — "Document Info Record" bold, below banner
4. **Collapsible search card** — white card with chevron toggle; contains:
   - Left column: "What do you want to work on?" dropdown + "Material" text input
   - Right section: "Relevant document types" label + 2 columns of checkboxes (11 total) + "Check All"
   - Bottom: "FIND DOCUMENTS" black button
5. **Footer** — centered "©Kemira" grey text

### Success Criteria
- [ ] All 32 components from `docs/gui_description.txt` are rendered
- [ ] Navigation active state is shown on "DOCUMENT INFO RECORD" link
- [ ] Alert banner spans full width and is clearly visible
- [ ] Search card collapses/expands when clicking the chevron icon
- [ ] "Check All" checkbox toggles all 11 document type checkboxes
- [ ] "FIND DOCUMENTS" button calls a `findDocuments()` method (logs to console)
- [ ] Page is responsive at desktop widescreen (16:9)
- [ ] No inline JavaScript expressions in HTML (all logic in JS functions)
- [ ] Alpine.js attribute ordering: `x-data` → `x-init` → bindings → events → conditionals → transitions
- [ ] File opens directly in browser with no build step

---

## All Needed Context

### Documentation & References
```yaml
- url: https://alpinejs.dev/start-here
  why: Alpine.js CDN script tag and basic x-data setup

- url: https://alpinejs.dev/directives/data
  why: How to define component state and methods

- url: https://alpinejs.dev/directives/show
  why: Used for collapsible card (x-show with transition)

- url: https://alpinejs.dev/directives/model
  why: Used for checkbox and input binding (x-model)

- url: https://alpinejs.dev/directives/on
  why: @click for button and chevron interactions

- url: https://alpinejs.dev/directives/bind
  why: :class for conditional nav active styling

- url: https://alpinejs.dev/directives/text
  why: x-text for dynamic text rendering

- url: https://alpinejs.dev/directives/transition
  why: Smooth collapse/expand animation on the search panel

- url: https://tailwindcss.com/docs/installation/play-cdn
  why: Tailwind CSS via CDN (no build step) for styling

- file: docs/gui_description.txt
  why: PRIMARY REFERENCE — complete component list with positions, colors, labels, and notes
```

### Screen Description (Embedded for Agent Context)
```
SCREEN TITLE: Document Info Record - Search Documents
SCREEN DIMENSIONS: Desktop widescreen (approx 16:9)
BACKGROUND: Light grey (#f5f5f5)

COMPONENTS:
comp_01  navbar           [Top Navigation Bar]           white bg, full-width
comp_02  label            [Logo/Brand]                   black rectangle, top-left
comp_03  label            VENDOR DOCUMENTS               dark grey, nav link
comp_04  label            MY REQUESTS                    dark grey, nav link
comp_05  label            SOURCING REQUESTS              dark grey, nav link
comp_06  label            ARCHIVE                        dark grey, nav link
comp_07  label            DOCUMENT INFO RECORD           dark, ACTIVE (underlined)
comp_08  label            CONFIGURATION                  dark grey, nav link + chevron
comp_09  icon             [User Avatar]                  grey circle
comp_10  divider          You are in test system         dark red (#8b1a1a), full-width, white text centered
comp_11  header           Document Info Record           bold black, page title
comp_12  card             Search Documents               white card, collapsible with chevron top-right
comp_13  label            Search Documents               card section title
comp_14  label            What do you want to work on?*  field label with required asterisk
comp_15  dropdown         Product documentation          with chevron, in left column
comp_16  label            Material *                     field label with required asterisk
comp_17  input            60172 : ISOTHIAZOLINE...       wide text input, left column
comp_18  label            Relevant document types *      right section header
comp_19  checkbox         Check All                      top of right column
comp_20  checkbox         Cert. of Conformity            right col 1
comp_21  checkbox         CoA for Finished Pr.           right col 1
comp_22  checkbox         Manufacturing Plan             right col 1
comp_23  checkbox         Product Info. Form             right col 1
comp_24  checkbox         Sales Specification            right col 1
comp_25  checkbox         Auth. Confirmation             far right col 2
comp_26  checkbox         Certification                  far right col 2
comp_27  checkbox         CoA for Traded Goods           far right col 2
comp_28  checkbox         Pr. Research Summary           far right col 2
comp_29  checkbox         Raw Material Quest.            far right col 2
comp_30  checkbox         Technical Data Sheet           far right col 2
comp_31  button           FIND DOCUMENTS                 black bg, white text, bottom-left of card
comp_32  footer           ©Kemira                        grey, centered, bottom of page
```

### Current Codebase Tree
```bash
.
├── .claude/
│   └── commands/
├── docs/
│   └── gui_description.txt      # PRIMARY INPUT - screen layout description
├── examples/
│   └── .gitkeep                 # Empty - no existing Alpine.js examples
├── PRPs/
│   ├── templates/
│   │   └── prp_base.md
│   └── text-to-alpinejs-gui.md  # This PRP
├── CLAUDE.md
├── INITIAL.md
└── README.md
```

### Desired Codebase Tree
```bash
.
├── docs/
│   └── gui_description.txt      # Unchanged input
├── output/
│   └── document-info-record.html  # NEW: The generated Alpine.js page
├── TASK.md                        # NEW: Task tracking
└── ... (unchanged)
```

### Known Gotchas & Alpine.js Quirks
```javascript
// CRITICAL: Alpine.js MUST be loaded with defer attribute, placed BEFORE the component markup
// <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>

// CRITICAL: x-data component function must be defined BEFORE Alpine.js initialises
// Define JS function in a <script> tag ABOVE the Alpine CDN <script defer> tag
// OR define it in a <script> tag in <head> that runs synchronously

// CRITICAL: CLAUDE.md requires logic OUT of the DOM — no inline expressions like @click="open = !open"
// Instead: @click="toggleSearchPanel()" — method defined in component function

// CRITICAL: CLAUDE.md attribute ordering in HTML elements:
// x-data → x-init → :bind attrs → @events → x-show/x-if → x-transition

// CRITICAL: x-show uses display:none, not DOM removal — use it for the collapsible panel
// x-transition adds smooth animation: x-transition:enter / x-transition:leave

// GOTCHA: Tailwind CDN (Play CDN) is for prototyping only — suitable here since this is a prototype
// <script src="https://cdn.tailwindcss.com"></script>

// GOTCHA: Alpine x-model on a checkbox uses true/false values by default — works for boolean state
// For "Check All", use a watcher or a dedicated toggleAll() method (not @change inline)

// GOTCHA: Custom Tailwind colours (#8b1a1a, #f5f5f5) need inline style="" or tailwind.config
// Use inline style attributes for the specific custom colours in this screen

// PATTERN: Self-contained HTML file — all CSS via CDN, all JS inline in <script> or x-data
// No external files, no build step, opens directly in browser
```

---

## Implementation Blueprint

### Data Models and Structure

```javascript
// The Alpine.js component function — define in <script> in <head>
// Component: documentSearchApp()
// State:
//   isSearchPanelOpen: boolean  — controls card collapse/expand
//   workOn: string              — value of the "What do you want to work on?" dropdown
//   material: string            — value of the Material text input
//   allChecked: boolean         — state of "Check All" checkbox
//   docTypes: object            — keyed boolean map of all 11 document type checkboxes

// Methods:
//   init()                — called by x-init, no side effects (empty or setup)
//   toggleSearchPanel()   — flips isSearchPanelOpen
//   toggleAll()           — sets all docTypes values to match allChecked
//   watchDocTypes()       — updates allChecked when individual boxes change (use $watch or recompute in toggleDocType)
//   toggleDocType(key)    — toggles individual checkbox and recalculates allChecked
//   findDocuments()       — collects form state, logs to console, could show alert

function documentSearchApp() {
  return {
    // State
    isSearchPanelOpen: true,
    workOn: 'Product documentation',
    material: '60172 : ISOTHIAZOLINE 1,5% DRUMTH 209KG PMRA',
    allChecked: false,
    docTypes: {
      certConformity:    false,
      coaFinished:       false,
      manufacturingPlan: false,
      productInfoForm:   false,
      salesSpec:         false,
      authConfirmation:  false,
      certification:     false,
      coaTraded:         false,
      prResearchSummary: false,
      rawMaterialQuest:  false,
      technicalDataSheet:false,
    },

    // Called by x-init — set up watchers here
    init() {
      this.$watch('docTypes', () => {
        const values = Object.values(this.docTypes);
        this.allChecked = values.every(v => v);
      }, { deep: true });
    },

    toggleSearchPanel() {
      this.isSearchPanelOpen = !this.isSearchPanelOpen;
    },

    toggleAll() {
      Object.keys(this.docTypes).forEach(key => {
        this.docTypes[key] = this.allChecked;
      });
    },

    findDocuments() {
      const selected = Object.entries(this.docTypes)
        .filter(([, v]) => v)
        .map(([k]) => k);
      console.log('Find Documents clicked', {
        workOn: this.workOn,
        material: this.material,
        selectedDocTypes: selected,
      });
    },
  };
}
```

### List of Tasks (in order)

```yaml
Task 1: Create output directory and skeleton HTML file
CREATE output/document-info-record.html:
  - Standard HTML5 boilerplate (<!DOCTYPE html>, <html lang="en">)
  - <head> with charset, viewport, title "Document Info Record - Search Documents"
  - Load Tailwind CSS CDN: <script src="https://cdn.tailwindcss.com"></script>
  - Define documentSearchApp() function in a <script> block in <head> (before Alpine loads)
  - Load Alpine.js CDN with defer: <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
  - <body> with x-data="documentSearchApp()" and x-init="init()" and style="background-color:#f5f5f5"
  - Verify file opens in browser with no errors

Task 2: Implement Navigation Bar (comp_01 to comp_09)
MODIFY output/document-info-record.html:
  - <nav> element: white bg, full-width, flex layout, shadow-sm
  - Left: logo — black filled rectangle div (logo placeholder per notes)
  - Right: flex row of nav links using <a> tags with x-text content
  - Active link (DOCUMENT INFO RECORD): darker colour, border-bottom-2 style
  - CONFIGURATION link: append a ▾ chevron character after text
  - User avatar: grey circle div, far right
  - Use Tailwind classes for layout, inline style only for #8b1a1a and custom colours

Task 3: Implement Alert Banner (comp_10)
MODIFY output/document-info-record.html:
  - Full-width <div> below <nav>
  - inline style="background-color:#8b1a1a"
  - White text, centered, padding, text content "You are in test system"
  - Use x-text to display the message (keeps logic out of DOM)

Task 4: Implement Page Title (comp_11)
MODIFY output/document-info-record.html:
  - <h1> tag below the banner
  - "Document Info Record" — bold, black, appropriate size
  - Left-aligned with consistent horizontal padding

Task 5: Implement Collapsible Search Card (comp_12, comp_13)
MODIFY output/document-info-record.html:
  - White card div with border, rounded, shadow-sm, margin
  - Card header: flex row, "Search Documents" label left, chevron button right
  - Chevron button: @click="toggleSearchPanel()" — uses ▾ / ▴ based on isSearchPanelOpen
  - Card body: x-show="isSearchPanelOpen" with x-transition for smooth animation

Task 6: Implement Left Column Form Fields (comp_14 to comp_17)
MODIFY output/document-info-record.html (inside card body):
  - 2-column flex layout inside card body
  - Left column:
    - Label: "What do you want to work on? *" (with red asterisk)
    - <select> dropdown: x-model="workOn", option "Product documentation"
    - Label: "Material *" (with red asterisk)
    - <input type="text"> x-model="material", full-width within column

Task 7: Implement Right Section — Document Type Checkboxes (comp_18 to comp_30)
MODIFY output/document-info-record.html (inside card body, right column):
  - Section label: "Relevant document types *" (with red asterisk)
  - "Check All" checkbox: x-model="allChecked" @change="toggleAll()"
  - Two sub-columns of checkboxes (5-6 each):
    Left sub-column (col 1): Cert. of Conformity, CoA for Finished Pr., Manufacturing Plan,
                              Product Info. Form, Sales Specification
    Right sub-column (col 2): Auth. Confirmation, Certification, CoA for Traded Goods,
                               Pr. Research Summary, Raw Material Quest., Technical Data Sheet
  - Each checkbox: x-model="docTypes.{key}" — no inline logic
  - Label text uses x-text or literal text (no dynamic data, so literal is fine)

Task 8: Implement FIND DOCUMENTS Button (comp_31)
MODIFY output/document-info-record.html (bottom of card body):
  - <button> element: black bg, white text, uppercase, px-4 py-2
  - @click="findDocuments()"
  - Positioned bottom-left of card, below the form grid

Task 9: Implement Footer (comp_32)
MODIFY output/document-info-record.html:
  - <footer> at bottom of page
  - Centered grey text "©Kemira"
  - Sufficient top margin to push to bottom on full-page content

Task 10: Create TASK.md
CREATE TASK.md:
  - Add task entry: "Generate Alpine.js page from gui_description.txt" with date 2026-02-28
  - Mark as completed after output/document-info-record.html is validated
```

### Per Task Pseudocode

```html
<!-- TASK 1: Skeleton structure -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document Info Record - Search Documents</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    // PATTERN (CLAUDE.md): Define component function BEFORE Alpine initialises
    // REASON: Alpine.js scans DOM on load; function must exist in global scope first
    function documentSearchApp() {
      return {
        isSearchPanelOpen: true,
        workOn: 'Product documentation',
        material: '60172 : ISOTHIAZOLINE 1,5% DRUMTH 209KG PMRA',
        allChecked: false,
        docTypes: {
          certConformity:     false,
          coaFinished:        false,
          manufacturingPlan:  false,
          productInfoForm:    false,
          salesSpec:          false,
          authConfirmation:   false,
          certification:      false,
          coaTraded:          false,
          prResearchSummary:  false,
          rawMaterialQuest:   false,
          technicalDataSheet: false,
        },

        init() {
          // PATTERN (CLAUDE.md): x-init only for side effects
          // Use $watch to keep allChecked in sync with individual checkboxes
          this.$watch('docTypes', () => {
            const vals = Object.values(this.docTypes);
            this.allChecked = vals.length > 0 && vals.every(Boolean);
          }, { deep: true });
        },

        toggleSearchPanel() {
          this.isSearchPanelOpen = !this.isSearchPanelOpen;
        },

        toggleAll() {
          // REASON: Called by "Check All" checkbox @change — syncs all docTypes
          Object.keys(this.docTypes).forEach(key => {
            this.docTypes[key] = this.allChecked;
          });
        },

        findDocuments() {
          const selected = Object.entries(this.docTypes)
            .filter(([, v]) => v)
            .map(([k]) => k);
          console.log('Find Documents:', { workOn: this.workOn, material: this.material, selected });
        },
      };
    }
  </script>
  <!-- CRITICAL: defer ensures Alpine initialises after DOM is parsed -->
  <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
</head>
<body
  x-data="documentSearchApp()"
  x-init="init()"
  style="background-color:#f5f5f5; min-height:100vh;"
  class="font-sans text-sm"
>

  <!-- TASK 2: Navigation Bar (comp_01 to comp_09) -->
  <nav class="bg-white shadow-sm px-4 py-2 flex items-center justify-between">
    <!-- Logo (comp_02): black rectangle placeholder -->
    <div class="bg-black w-24 h-7 rounded-sm"></div>

    <!-- Nav links (comp_03 to comp_09) -->
    <div class="flex items-center gap-6 text-xs font-medium text-gray-600 uppercase tracking-wide">
      <a href="#" class="hover:text-gray-900">Vendor Documents</a>
      <a href="#" class="hover:text-gray-900">My Requests</a>
      <a href="#" class="hover:text-gray-900">Sourcing Requests</a>
      <a href="#" class="hover:text-gray-900">Archive</a>
      <!-- comp_07: Active link — darker colour, underline -->
      <a href="#" class="text-gray-900 font-bold border-b-2 border-gray-900">Document Info Record</a>
      <!-- comp_08: Dropdown nav link -->
      <a href="#" class="hover:text-gray-900 flex items-center gap-1">Configuration <span>▾</span></a>
      <!-- comp_09: Avatar circle -->
      <div class="w-8 h-8 rounded-full bg-gray-400 flex items-center justify-center text-white text-xs">
        <!-- avatar icon placeholder -->
      </div>
    </div>
  </nav>

  <!-- TASK 3: Alert Banner (comp_10) -->
  <div
    class="w-full py-2 text-center text-white text-sm font-medium"
    style="background-color:#8b1a1a;"
  >
    <!-- PATTERN (CLAUDE.md): x-text keeps text out of DOM attributes -->
    <span x-text="'You are in test system'"></span>
  </div>

  <!-- Main content wrapper -->
  <main class="max-w-screen-xl mx-auto px-4 py-4">

    <!-- TASK 4: Page Title (comp_11) -->
    <h1 class="text-xl font-bold text-gray-900 mb-4">Document Info Record</h1>

    <!-- TASK 5: Collapsible Search Card (comp_12, comp_13) -->
    <div class="bg-white border border-gray-200 rounded shadow-sm">

      <!-- Card Header -->
      <div class="flex items-center justify-between px-4 py-3 border-b border-gray-100">
        <span class="font-semibold text-gray-800 text-sm">Search Documents</span>
        <button
          @click="toggleSearchPanel()"
          class="text-gray-500 hover:text-gray-800 text-base"
          :aria-label="isSearchPanelOpen ? 'Collapse search panel' : 'Expand search panel'"
        >
          <!-- PATTERN (:class object for conditional rendering) -->
          <span x-text="isSearchPanelOpen ? '▴' : '▾'"></span>
        </button>
      </div>

      <!-- TASK 6 & 7: Card Body — collapsible -->
      <div
        x-show="isSearchPanelOpen"
        x-transition:enter="transition ease-out duration-150"
        x-transition:enter-start="opacity-0 -translate-y-1"
        x-transition:enter-end="opacity-100 translate-y-0"
        x-transition:leave="transition ease-in duration-100"
        x-transition:leave-start="opacity-100 translate-y-0"
        x-transition:leave-end="opacity-0 -translate-y-1"
        class="px-4 py-4"
      >
        <!-- Two-column grid: left form fields + right checkboxes -->
        <div class="flex gap-8">

          <!-- Left Column: form fields -->
          <div class="flex flex-col gap-3 w-72">

            <!-- comp_14 + comp_15: Work on dropdown -->
            <div>
              <label class="block text-xs text-gray-600 mb-1">
                What do you want to work on? <span class="text-red-600">*</span>
              </label>
              <select
                x-model="workOn"
                class="w-full border border-gray-300 rounded px-2 py-1.5 text-sm bg-white"
              >
                <option>Product documentation</option>
                <option>Safety documentation</option>
                <option>Quality documentation</option>
              </select>
            </div>

            <!-- comp_16 + comp_17: Material input -->
            <div>
              <label class="block text-xs text-gray-600 mb-1">
                Material <span class="text-red-600">*</span>
              </label>
              <input
                type="text"
                x-model="material"
                class="w-full border border-gray-300 rounded px-2 py-1.5 text-sm"
              />
            </div>

          </div>

          <!-- Right Column: document type checkboxes -->
          <div class="flex flex-col gap-2 flex-1">

            <!-- comp_18: Section label -->
            <label class="text-xs text-gray-600">
              Relevant document types <span class="text-red-600">*</span>
            </label>

            <!-- comp_19: Check All -->
            <label class="flex items-center gap-2 text-xs font-medium text-gray-700 mb-1">
              <input
                type="checkbox"
                x-model="allChecked"
                @change="toggleAll()"
                class="rounded"
              />
              <span x-text="'Check All'"></span>
            </label>

            <!-- Two sub-columns of individual checkboxes -->
            <div class="flex gap-8">

              <!-- Left sub-column (comp_20 to comp_24) -->
              <div class="flex flex-col gap-1">
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.certConformity" class="rounded" />
                  <span x-text="'Cert. of Conformity'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.coaFinished" class="rounded" />
                  <span x-text="'CoA for Finished Pr.'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.manufacturingPlan" class="rounded" />
                  <span x-text="'Manufacturing Plan'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.productInfoForm" class="rounded" />
                  <span x-text="'Product Info. Form'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.salesSpec" class="rounded" />
                  <span x-text="'Sales Specification'"></span>
                </label>
              </div>

              <!-- Right sub-column (comp_25 to comp_30) -->
              <div class="flex flex-col gap-1">
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.authConfirmation" class="rounded" />
                  <span x-text="'Auth. Confirmation'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.certification" class="rounded" />
                  <span x-text="'Certification'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.coaTraded" class="rounded" />
                  <span x-text="'CoA for Traded Goods'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.prResearchSummary" class="rounded" />
                  <span x-text="'Pr. Research Summary'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.rawMaterialQuest" class="rounded" />
                  <span x-text="'Raw Material Quest.'"></span>
                </label>
                <label class="flex items-center gap-2 text-xs text-gray-700">
                  <input type="checkbox" x-model="docTypes.technicalDataSheet" class="rounded" />
                  <span x-text="'Technical Data Sheet'"></span>
                </label>
              </div>

            </div><!-- end two sub-columns -->

          </div><!-- end right column -->

        </div><!-- end two-column grid -->

        <!-- TASK 8: FIND DOCUMENTS Button (comp_31) -->
        <div class="mt-4">
          <button
            @click="findDocuments()"
            class="bg-black text-white text-xs font-bold uppercase px-5 py-2 rounded hover:bg-gray-800 active:bg-gray-900"
          >
            Find Documents
          </button>
        </div>

      </div><!-- end card body -->

    </div><!-- end search card -->

  </main>

  <!-- TASK 9: Footer (comp_32) -->
  <footer class="text-center text-gray-400 text-xs py-6 mt-8">
    <span x-text="'©Kemira'"></span>
  </footer>

</body>
</html>
```

### Integration Points
```yaml
FILES:
  - Create: output/document-info-record.html
  - Create: TASK.md
  - Read:   docs/gui_description.txt (input — do not modify)

CDN DEPENDENCIES:
  - Alpine.js v3: https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js
    (use the latest 3.x release, e.g. 3.14.1 — check https://alpinejs.dev/start-here)
  - Tailwind CSS Play CDN: https://cdn.tailwindcss.com

NO BUILD SYSTEM REQUIRED — file opens directly in a browser.
```

---

## Validation Loop

### Level 1: File Structure Check
```bash
# Verify output file was created
ls -la output/document-info-record.html

# Check file is non-empty and has expected markers
grep -c "x-data" output/document-info-record.html    # Should be >= 1
grep -c "x-show" output/document-info-record.html    # Should be >= 1
grep -c "x-model" output/document-info-record.html   # Should be >= 11 (one per checkbox)
grep -c "@click" output/document-info-record.html    # Should be >= 2
grep -c "alpinejs" output/document-info-record.html  # Should be 1 (CDN script)
grep -c "tailwindcss" output/document-info-record.html # Should be 1 (CDN script)

# Verify no inline JS expressions (logic should be in methods)
# This pattern should NOT appear: @click="open = !open" or x-show="flag == true"
grep -n "= !open\|== true\|== false" output/document-info-record.html  # Should be 0 matches
```

### Level 2: Component Coverage Check
```bash
# Verify all major components are present by checking for key text strings
grep -i "You are in test system" output/document-info-record.html   # comp_10
grep -i "Document Info Record" output/document-info-record.html     # comp_11
grep -i "Search Documents" output/document-info-record.html         # comp_12/13
grep -i "What do you want to work on" output/document-info-record.html # comp_14
grep -i "Material" output/document-info-record.html                 # comp_16
grep -i "Relevant document types" output/document-info-record.html  # comp_18
grep -i "Check All" output/document-info-record.html                # comp_19
grep -i "Cert. of Conformity" output/document-info-record.html      # comp_20
grep -i "Auth. Confirmation" output/document-info-record.html       # comp_25
grep -i "Technical Data Sheet" output/document-info-record.html     # comp_30
grep -i "Find Documents" output/document-info-record.html           # comp_31
grep -i "Kemira" output/document-info-record.html                   # comp_32
```

### Level 3: Alpine.js Conventions Check (CLAUDE.md compliance)
```bash
# Verify attribute ordering: x-data comes before x-init (check body tag)
grep -A2 "x-data" output/document-info-record.html

# Verify no x-html usage (CLAUDE.md: avoid x-html for untrusted content)
grep "x-html" output/document-info-record.html  # Should return NOTHING

# Verify logic is in methods (no fat-arrow inline state mutations)
# Pattern to AVOID: @click="someBoolean = !someBoolean"
# Pattern to HAVE:  @click="toggleSomething()"
grep "@click=" output/document-info-record.html  # All should call method names ending in ()
```

### Level 4: Manual Browser Validation
Open `output/document-info-record.html` in a browser and verify:

```
Visual Checks:
[ ] Page background is light grey (#f5f5f5)
[ ] Navigation bar is white with logo (black rectangle) on the left
[ ] Six nav links appear on the right, "Document Info Record" is visually distinct (bold/underlined)
[ ] User avatar circle appears far right in nav
[ ] Dark red alert banner spans full width with "You are in test system" centred in white text
[ ] "Document Info Record" h1 appears below the banner, bold
[ ] White search card renders below the page title
[ ] Card header shows "Search Documents" left and a chevron button right

Interaction Checks:
[ ] Click the chevron button → search card body collapses smoothly
[ ] Click again → search card body expands smoothly
[ ] "What do you want to work on?" shows a dropdown selector
[ ] "Material" text input is editable
[ ] "Check All" checkbox → checking it checks ALL 11 document type checkboxes
[ ] "Check All" checkbox → unchecking it unchecks ALL 11 document type checkboxes
[ ] Checking all 11 individually → "Check All" becomes checked automatically
[ ] "FIND DOCUMENTS" button → opens browser console, logs object with workOn, material, selected docTypes
[ ] Footer shows "©Kemira" centred at bottom

Accessibility:
[ ] The chevron button has aria-label that changes when open/closed
```

---

## Final Validation Checklist
- [ ] `output/document-info-record.html` exists and is < 500 lines (CLAUDE.md constraint)
- [ ] All 32 components from `docs/gui_description.txt` are represented
- [ ] Alpine.js CDN loaded with `defer`
- [ ] Component function defined before Alpine CDN script tag
- [ ] No `x-html` directives used (CLAUDE.md: avoid for untrusted content)
- [ ] Attribute ordering: `x-data` → `x-init` → bindings → events → conditionals (CLAUDE.md)
- [ ] All click handlers call named methods, no inline mutations
- [ ] `x-init` calls `init()` for logic (CLAUDE.md convention)
- [ ] `$watch` used in `init()` to sync `allChecked` with individual checkboxes
- [ ] Custom colours (#8b1a1a, #f5f5f5) applied via inline `style=""` attributes
- [ ] "Check All" correctly controls all 11 document type checkboxes bidirectionally
- [ ] `findDocuments()` method logs form state to console
- [ ] Page opens directly in browser with no build step
- [ ] `TASK.md` created and task marked as completed

---

## Anti-Patterns to Avoid
- ❌ Don't use `x-html` — use `x-text` for all dynamic text (CLAUDE.md: never inject untrusted HTML)
- ❌ Don't write inline mutations like `@click="isOpen = !isOpen"` — always call a named method
- ❌ Don't skip `defer` on the Alpine CDN script — it will throw "AlpineJS already started" errors
- ❌ Don't define the component function after the Alpine CDN script — race condition
- ❌ Don't use inline styles where Tailwind classes exist — prefer utility classes
- ❌ Don't add `x-init` logic that isn't a side effect — put business logic in named methods
- ❌ Don't create more than one HTML file — all 32 components belong in a single page
- ❌ Don't hardcode checked states in HTML — bind everything to Alpine state

---

## Confidence Score: 9/10

High confidence because:
- Complete, literal component inventory from `docs/gui_description.txt` is embedded in this PRP
- All Alpine.js directives needed are well-documented at alpinejs.dev
- Tailwind CSS CDN eliminates all styling complexity
- The component JS function pseudocode is provided in full above — agent can use it directly
- Validation gates are executable shell commands + clear manual browser checklist
- No backend, no build system, no external dependencies beyond 2 CDN scripts

Minor uncertainty on:
- Exact Alpine.js 3.x version number in CDN URL (agent should check alpinejs.dev for latest patch)
- Whether Tailwind's `rounded` class renders exactly as the native browser checkbox style — if not, use `accent-color: black` via inline style
