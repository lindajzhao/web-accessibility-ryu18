# WAI-ARIA Landmarks
- defines regions on a webpage

## 8 landmark roles
- [w3 reference](https://www.w3.org/TR/wai-aria-practices/examples/landmarks/index.html)
-  "all perceivable content should reside in a semantically meaningful landmark in order that content is not missed by the user"
- top level landmarks: banner, main, complementary, contentinfo (one per document/application)
- if a role will be reused, they should be differentiated using an `aria-label` or `aria-labelledby`

### Banner
- site-wide info (rather tan page-specific)
- usually contains logo, search
- top of page, spans full width

### Contentinfo
- Large region containing info about the parent document
- eg. copyright and links to privacy statements

### Navigation
- Usually links. For navigating the doc or related docs

### Main
- Central topic of the doc
- Alternative to "skip to main content" links

### Complementary
- Same level as main. Self-contained.
- relevant to main content

### Region
- An important section not described by main, complementary or navigation
- Must be accompannied by an `aria-label` or `aria-labelledby`

### Form
- Collection of els that create a form 

### Search
- Collection of els that create search 
- A more specific type of role=form

# Common Static WAI-ARIA
- [Example menubar with submenus](https://de.ryerson.ca/wa/aria/jquery/menubar.html)
- [w3.org WAI-ARIA-1.1](https://www.w3.org/TR/wai-aria-1.1)
- [Practical ARIA examples](http://heydonworks.com/practical_aria_examples/)
- **aria-describedby**: similar to aria-labelledby but more verbose
- **aria-labelledby**: references el which should be read when an el is focused (may be offscreen). Has precedence over aria-label
- **aria-label**: define label of el with visible text
- **aria-details**: references el which provides more detail than aria-describedby. Not used in Name Computation or Description Computation. Not converted to string(can reference nested DOM els). Precedence over aria-describedby
- **aria-required** (form): indicate field is required, just like symbols for sighted users
- **aria-controls**: property on an interactive el which indicate which el(s) it alters
- **aria-owns**: list of IDs to defines parent/child relationship where it differs from DOM relationship. Each ID can only be owned by 1 el
- **aria-haspopup**: popup appears as a block of content on top of other content
    - Container must have role of menu, listbox, tree, grid, dialogue. value of aria-haspop must match this role
    - aria-haspopup="true" defaults to "menu"
- **aria-live**: indicates this el will be updated. If not set, use aria-live value of nearest ancestor
    - off (default): updates should not be presented unless user is currently focused on that area
    - polite: presented at next graceful opportunity
    - assertive: highest priority: present immediately
- **aria-relevant**: indicates what accessibility tree semantic changes within a live region should be presented
    - optional on live regions
    - additions, removals, and/or text. (or all)
- **aria-atomic**: true/false(default). Determines whether to present changes up the ancestor tree based on aria-relevant notifications
- **aria-roledescription**: provides human-readable copy for role. To be localized or more descriptive. This is read instead of role.
    - `<div role="region" aria-roledescription="slide">`

# WAI-ARIA Alert and Message Dialogs
- Used to communicate error, confirmation, warning and completion
- excludes tooltips
- use **role="alert"** when no user input is not needed.
- **role="alertdialog"** when user input is expected.
    - Both roles create live regions. default: `aria-live=”assertive”` and `aria-atomic=”true”`
- modal dialogues interrupt users to give important info and require an action. use `role=”alertdialog”` and `aria-modal=”true”`.

# Tabindex
- "roving tabindex" created with scripting
- `tabindex="0"` adds kbd accessibility
- `tabindex="-1"` removes kbd accessibility
- strategy: surrounding div with tabindex="0" which presents instructions for navigating containing el.

# Keyboard Interaction
- everything accessible by mouse should be accessible with keyboard
- follow expected conventions
- [W3.org examples](https://www.w3.org/TR/wai-aria-practices/#aria_ex)

# Application and Presentation Roles
- currently has poor support
- both will disable default kbd functionality (also role="none")
    - nested items WILL still be announced as usual
    - preserves tab focus (and tabindex) and global states/properties
- **role="application"** where there isn't a predefined widget pattern
- Three common uses for **role=”presentation”** include:
    1. Hiding a decorative image; it is equivalent to giving the image null alt text.
    2. Suppressing table semantics for tables used for layout in circumstances where the table semantics do not convey meaningful relationships.
    3. Eliminating semantics of intervening orphan elements in the structure of a composite widget, such as a tablist, menu, or tree as demonstrated in the example above.

# Live Regions
- roles/props that create live regions:
    - **aria-live**: polite, assertive, off
    - **aria-relevant**: additions, removals, text, all
    - **aria-atomic**: true, false
    - **aria-busy**: true, false
    - role=”alert”
    - role=”log”
    - role=”marquee”
    - role=”timer”
    - role=”status”
- Barriers: constantly updating live regions such as timers, carousel, very active feeds