# GENERIC_IMPLEMENTATION.md - Business Detail Replacement Template

This implementation plan directs an AI development agent on how to replace generic placeholders in `index.html` with business-specific details.

To customize `index.html` for a new business, you must load a structured configuration JSON file containing the business information (following the schema of `business_info.json`) and apply the replacements specified below.

---

## Configuration Schema Reference

The business details must be provided in a JSON file structured as follows:

```json
{
  "businessName": "The full name of the construction/roofing business",
  "establishedYear": "Year the business was established (e.g., 2011)",
  "phone": {
    "formatted": "Formatted phone number: (XXX) XXX-XXXX",
    "raw": "10-digit raw number for tel links: XXXXXXXXXX"
  },
  "location": {
    "cityState": "Primary city and state: City, ST"
  },
  "recentWorkCities": [
    "City name for Recent Work caption 1",
    "City name for Recent Work caption 2",
    "City name for Recent Work caption 3"
  ],
  "reviewCities": [
    "City name for Review 1 (Mike T.)",
    "City name for Review 2 (Sarah M.)"
  ]
}
```

---

## City Selection Guidelines

When setting up a new business profile, you must research and identify target service cities to populate `recentWorkCities` and `reviewCities`. Use the following criteria:

1. **City 1 (Primary City)**: This is the city specified in `location.cityState`.
2. **City 2 (Second Target City)**: Research and identify a prime neighboring city for roofing sales (e.g., a larger local economic center or a high-demand suburb).
3. **City 3 (Third Target City)**: Research and identify a third prime neighboring city (e.g., an affluent residential community or active development area).

Ensure these mapped values are populated into:
- `recentWorkCities` (contains City 1, City 2, and City 3)
- `reviewCities` (contains City 1 and City 2)

---

## Replacement Checklist & Step-by-Step Instructions

Perform the following find-and-replace tasks in `index.html`.

### 1. Document Title
*   **Location**: `<title>` tag in `<head>`
*   **Target Pattern**: `<title>[Business Name] | Professional Roofing</title>`
*   **Replacement**: Replace `[Business Name]` with the value of `businessName`.
    *   *Example*: `<title>Lapp Brothers Construction | Professional Roofing</title>`

### 2. Navigation Logo
*   **Location**: `nav-logo` class span (inside `<nav>`)
*   **Target Pattern**: `<span class="nav-logo">[Business Name]</span>`
*   **Replacement**: Replace `[Business Name]` with the value of `businessName`.

### 3. Navigation Phone Link
*   **Location**: `nav-phone` class anchor (inside `<nav>`)
*   **Target Pattern**: `<a href="tel:+10000000000" class="nav-phone">(000) 000-0000</a>`
*   **Replacement**: 
    *   Replace `+10000000000` with `+1` followed by `phone.raw`.
    *   Replace `(000) 000-0000` with `phone.formatted`.

### 4. Hero Eyebrow
*   **Location**: `hero-eyebrow` class div (inside Hero section)
*   **Target Pattern**: `<div class="hero-eyebrow">Serving [City, State] Since [Year]</div>`
*   **Replacement**:
    *   Replace `[City, State]` with `location.cityState`.
    *   Replace `[Year]` with `establishedYear`.

### 5. Hero Name (Heading)
*   **Location**: `hero-name` class h1 heading
*   **Target Pattern**:
    ```html
    <h1 class="hero-name">
      [Business<br>
      <em>Name]</em>
    </h1>
    ```
*   **Replacement & Formatting Rule**: 
    Split `businessName` across the `<br>` tag to match the design style. The main brand words should appear on the first line, and the industry/action word (italicized in `<em>`) should go on the second line.
    *   *Example (Lapp Brothers Construction)*:
        ```html
        <h1 class="hero-name">
          Lapp Brothers<br>
          <em>Construction</em>
        </h1>
        ```
    *   *Example (Summit Roofing)*:
        ```html
        <h1 class="hero-name">
          Summit<br>
          <em>Roofing</em>
        </h1>
        ```

### 6. Recent Work Image Captions
*   **Location**: `.work-caption` class divs inside the Recent Work strip
*   **Target Patterns**:
    1.  `Active Roof Installation & Framing — [City]`
    2.  `Detailed Shingle & Pipe Boot Repair — [City]`
    3.  `Complete Residential Shingle Roofing — [City]`
*   **Replacement**: Replace the `[City]` placeholder in captions 1, 2, and 3 sequentially with the respective values in the `recentWorkCities` array.
    *   *Example*: Caption 1 -> `Winchester`, Caption 2 -> `Decherd`, Caption 3 -> `Estill Springs`.

### 7. Review 1 Text and Author
*   **Location**: First review card (Mike T.)
*   **Target Patterns**:
    *   `"Best roofer in [City]. Fast, professional..."`
    *   `<div class="reviewer">— Mike T., [City]</div>`
*   **Replacement**: Replace `[City]` in both elements with the first element of the `reviewCities` array (`reviewCities[0]`).

### 8. Review 2 Text and Author
*   **Location**: Second review card (Sarah M.)
*   **Target Patterns**:
    *   `"[Business Name] was the only one..."`
    *   `<div class="reviewer">— Sarah M., [City]</div>`
*   **Replacement**:
    *   Replace `[Business Name]` with the value of `businessName`.
    *   Replace `[City]` with the second element of the `reviewCities` array (`reviewCities[1]`).

### 9. Call-To-Action (CTA) Button Phone Link
*   **Location**: Call button in CTA section
*   **Target Pattern**: `<a href="tel:+10000000000" class="btn-white">Call (000) 000-0000</a>`
*   **Replacement**:
    *   Replace `+10000000000` with `+1` followed by `phone.raw`.
    *   Replace `Call (000) 000-0000` with `Call ` followed by `phone.formatted`.

### 10. Footer Name & Note
*   **Location**: Footer tags
*   **Target Patterns**:
    *   `<span class="footer-name">[Business Name] Roofing</span>`
    *   `<span class="footer-note">Licensed & Insured &nbsp;·&nbsp; [City, State]</span>`
*   **Replacement**:
    *   Replace `[Business Name]` in the footer name with `businessName`.
    *   Replace `[City, State]` in the footer note with `location.cityState`.

---

## Verification Plan

Once replacements are complete, the AI agent must verify the following:

1.  **Strict String Validation**:
    *   Search `index.html` for any leftover `[` or `]` characters to ensure no placeholder token remains.
    *   Search `index.html` for `(000) 000-0000` or `+10000000000` to verify phone number replacements.
2.  **HTML Well-Formedness**:
    *   Verify all tag structures are closed correctly and no HTML tags (e.g., `<br>`, `<em>`) are broken during the Hero Name split.
3.  **Local Visual Inspection**:
    *   Load the page and confirm the layout renders correctly with the custom text.
