---
title: Red Text for Completed Items
version: 1.0
date_created: 2025-11-13
last_updated: 2025-11-13
---
# Implementation Plan: Red Text for Completed Items

**Brief description**: Modify the visual styling of completed todo items to display red text instead of the current grey (#999), providing a more prominent visual distinction between active and completed tasks.

## Architecture and design

### Overview
This is a **CSS-only change** that modifies existing styling without affecting the application's data model, rendering logic, or event handling patterns.

**Files affected**: 
- `todo-list-typescript-main/src/css/style.css` (single line modification)

**Architecture alignment**:
- ✅ Pure CSS solution (no JavaScript changes)
- ✅ Maintains singleton pattern (no model/template modifications)
- ✅ Follows existing BEM-like naming conventions
- ✅ Preserves accessibility features
- ✅ Consistent with project's styling domain patterns

### Design Considerations

1. **Existing Implementation**:
   - Current selector: `.item>input[type="checkbox"]:checked+label`
   - Current properties: `text-decoration: line-through; color: #999;`
   - Located at: `src/css/style.css` line 131-133

2. **Color Change Rationale**:
   - **From**: Grey `#999` (medium grey, subtle completed state)
   - **To**: Red color (more prominent, attention-grabbing)
   - **Consideration**: Need to choose appropriate red shade that maintains accessibility

3. **Red Color Options**:
   - `#ff0000` - Pure red (very bright, may be too aggressive)
   - `#dc143c` - Crimson (vibrant but more refined)
   - `#c41e3a` - Dark red (softer, better contrast)
   - `#cc0000` - Medium red (balanced visibility)
   - **Recommendation**: Use `#ff6b6b` (coral red) for better readability on dark background

4. **Accessibility Considerations**:
   - Background color: `#333` (dark grey)
   - Must maintain WCAG AA contrast ratio (minimum 4.5:1 for normal text)
   - Current `#999` provides 5.9:1 contrast
   - Proposed `#ff6b6b` provides ~6.2:1 contrast (exceeds WCAG AA)
   - Alternative `#ff4757` provides ~5.8:1 contrast

5. **Consistency with Project Patterns**:
   - Follows existing checked state selector pattern
   - Uses adjacent sibling combinator (already established)
   - Maintains single global stylesheet approach
   - No architectural changes required
   - Aligns with styling domain conventions documented in `.results/4-domains/styling.md`

### Browser Compatibility
- Standard CSS `color` property - universal support
- No vendor prefixes needed
- Works with existing `:checked` pseudo-class
- No polyfills required

## Tasks

### Task 1: Determine optimal red color value
- [ ] Test color contrast ratios using WebAIM contrast checker
- [ ] Verify proposed colors on dark background (`#333`)
- [ ] Choose between:
  - `#ff6b6b` (coral red - 6.2:1 contrast) ✅ Recommended
  - `#ff4757` (bright red - 5.8:1 contrast)
  - `#dc143c` (crimson - may need testing)
- [ ] Document chosen color with contrast ratio justification
- **Acceptance criteria**: Selected color meets WCAG AA (4.5:1 minimum)

### Task 2: Modify CSS file
- [ ] Open `todo-list-typescript-main/src/css/style.css`
- [ ] Locate `.item>input[type="checkbox"]:checked+label` selector (line ~131-133)
- [ ] Change `color: #999;` to `color: #ff6b6b;` (or chosen red)
- [ ] Maintain existing formatting and indentation
- [ ] Preserve `text-decoration: line-through;` property
- **Acceptance criteria**: CSS file modified with single color value change

### Task 3: Visual verification in development
- [ ] Run `npm run dev` in `todo-list-typescript-main` directory
- [ ] Navigate to `http://localhost:5173/` in browser
- [ ] Create multiple test todo items
- [ ] Check various items to mark as complete
- [ ] Verify completed items display:
  - Line-through decoration (existing)
  - Red text color (new)
- [ ] Verify unchecked items remain white/whitesmoke
- **Acceptance criteria**: Visual appearance matches design intent

### Task 4: Accessibility testing
- [ ] Verify contrast ratio in browser DevTools or contrast checker
- [ ] Test with browser zoom at 200% (ensure readability)
- [ ] Test with Windows High Contrast mode (if available)
- [ ] Verify screen reader still announces checked state correctly
- [ ] Check both hover and focus states on checkbox remain functional
- **Acceptance criteria**: WCAG AA compliance maintained, no accessibility regressions

### Task 5: Cross-browser compatibility testing
- [ ] Test in Chrome/Edge (primary browsers)
- [ ] Test in Firefox
- [ ] Test in Safari (if macOS available)
- [ ] Verify consistent red color rendering across browsers
- [ ] Check mobile viewport rendering (responsive design)
- **Acceptance criteria**: Consistent appearance across modern browsers

### Task 6: Update documentation (optional)
- [ ] Consider updating `.github/copilot-instructions.md` example if it references grey color
- [ ] Update `grey-text-completed-items.md` status to "SUPERSEDED" if desired
- [ ] Document the color change rationale in commit message
- **Acceptance criteria**: Relevant documentation reflects new color choice

## Open questions

### 1. What shade of red should be used?
**Context**: Multiple red options available, each with different visual impact and accessibility implications.

**Options**:
- **Option A**: `#ff6b6b` (Coral red)
  - Pros: Softer, warm tone; excellent contrast (6.2:1); easy on eyes
  - Cons: Less "dramatic" than pure red
- **Option B**: `#ff4757` (Bright red)
  - Pros: More vibrant; good contrast (5.8:1); attention-grabbing
  - Cons: May feel aggressive for completed tasks
- **Option C**: `#dc143c` (Crimson)
  - Pros: Classic red; professional appearance
  - Cons: Needs contrast verification
- **Option D**: Custom color based on design system
  - Pros: Could match broader brand colors
  - Cons: No existing design system in this project

**Recommendation**: **Option A (`#ff6b6b`)** - Best balance of visibility, accessibility, and visual comfort for completed tasks.

**Decision needed**: Confirm preferred red shade before implementation.

---

### 2. Should red color semantics be considered?
**Context**: Red typically signifies error, danger, or warning in UI design. Using red for "completed" tasks may conflict with conventional color semantics.

**Considerations**:
- **Traditional semantics**: Red = error/danger, Green = success, Grey = disabled/inactive
- **Current implementation**: Grey indicates completion (neutral/inactive state)
- **Proposed change**: Red for completion (unconventional)

**Potential issues**:
- Users may perceive red items as errors needing attention
- Conflicts with standard UI patterns (e.g., form validation)
- May cause confusion about what action is needed

**Alternative approaches**:
- Use green for completed items (aligns with success semantics)
- Use blue for completed items (informational, neutral)
- Keep grey but make it darker/lighter for variation
- Add icon or badge instead of color change

**Question**: Is there a specific reason red is preferred over semantically conventional colors like green?

**Recommendation**: Consider green (`#6bcf7f` - 6.4:1 contrast) or blue (`#4a90e2`) as alternatives that align with standard UI patterns.

---

### 3. Should there be a transition/animation effect?
**Context**: The current implementation has instant state changes with no CSS transitions.

**Considerations**:
- No transitions currently exist in the codebase
- Adding `transition: color 0.3s ease;` would animate the color change
- Would be a new pattern not established in the styling domain

**Options**:
- **Option A**: No transition (maintain consistency with existing instant changes)
- **Option B**: Add subtle transition (150-300ms) for smoother visual feedback
- **Option C**: Add transition only for color, not other properties

**Architectural impact**:
- Option A: No impact, maintains current patterns
- Option B/C: Introduces new CSS pattern, sets precedent for future animations

**Question**: Should we maintain the current instant state change pattern, or introduce animations?

**Recommendation**: **Option A** - Maintain consistency with existing codebase patterns unless animations are being added project-wide.

---

**Estimated effort**: 10 minutes (CSS modification + testing)  
**Risk level**: Very low (isolated CSS change, easily reversible)  
**Testing required**: Visual verification, accessibility testing, cross-browser compatibility check  
**Rollback plan**: Revert single line change from red back to `#999` grey
