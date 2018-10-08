# WCAG and Basic WAI-ARIA

# WCAG
- Web Content Accessibility Guidelines

## POUR
1. Perceivable
2. Operable
3. Understandable
4. Robust

## Conformance levels: 
- importance in removing barriers
- A: These MUST be resolved: significant barriers
- AA: SHOULD be resolved, can be circumvented with some effort.
    - Generally accepted level of conformance
- AAA: COULD be resolved.

# WAI-ARIA
- Web Accessibility Initiative: Accessible Rich Internet Applications
- 1.0 relreased March 2014
- 1.1 released Dec 2017
- Javascript/scripting required

## WAI-ARIA and HTML 5
- WAI-ARIA was released as a complement to HTML5
Make divs appear as button to a screenreader:
`<div role=”button” aria-pressed=”false” tabindex=”0”>Press Me</div>`

- “WAI-ARIA provides a framework for adding attributes to identify features for user interaction, how they relate to each other, and their current state” (Source W3C (Links to an external site.)Links to an - external site.).

### When to use:
 - make a web app or widget understandable
 - native HTML elements are better w/e possible: standardized, have all semantics by default
    - newer HTML 5 elements (`nav`, `main`) can have a `role="navigation`' etc to accomodate insonsistent support
 - h3 with a `role` will not have h3 meaning. Better to wrap in div:
 `<div role="button"><h3>Chapter 3</h3></div>`

 ## Roles
- main indicator of type.
- should not change over time or with user input
- 6 Groupings:
    - Abstract role (not to be used by authors in content, the base for the WAI-ARIA ontology)
    - Widget roles (e.g. button, link, menuitem)
    - Document structure roles (e.g. article, feed, list, table)
    - Landmark roles (e.g. banner, navigation, main, complementary)
    - Live region roles (e.g. alert, log, timer)
    - Window roles (e.g. alertdialog, dialog)

```
<ul role=”menubar”>
    <li role="menuitem">Blog</li>
    <li role="menuitem">Contact</li>
</ul>
```
- [List of all aria-roles](https://www.w3.org/TR/2017/REC-wai-aria-1.1-20171214/#role_definitions)

 ## States and Properties
- States and Properties are both referred to as Attributes
- [List of all attributes](https://www.w3.org/TR/2017/REC-wai-aria-1.1-20171214/#global_states)

### States
- dynamic property which defines functional status
- changes as it's being used/ on user input
- `aria-` prefixed
- Examples:
    - aria-busy
    - aria-checked
    - aria-expanded
    - aria-disabled
    - aria-hidden

 ### Properties
 - static (usually)
 - Examples:
    - aria-describedby
    - aria-atomic
    - aria-autocomplete
    - aria-colcount
    - aria-colspan
    - aria-controls
- Some are expected to change (w/ JS):
    - aria-activedescendant
    - aria-valuenow
    - aria-valuetext

## Static vs Dynamic WAI-ARIA
[List with descriptions](http://whatsock.com/training/matrices/)
[Cheat Sheet](https://www.cheatography.com/jreiche/cheat-sheets/wai-aria-1-1/)
### Global static properties

- aria-describedby: Identifies the element (or elements) that describes the object.
- aria-labelledby: Identifies the element (or elements) that labels the current element.
- aria-label: Defines a string value that labels the current element.
- aria-controls: Identifies the element (or elements) whose contents or presence are controlled by the current element.
- aria-owns: Identifies an element (or elements) in order to define a visual, functional, or contextual parent/child relationship between DOM elements where the DOM hierarchy cannot be used to represent the relationship.
- aria-details: Identifies the element that provides a detailed, extended description for the object.

```
<div id="chooser">
Use this menu to browse through our offerings, and choose courses you wish to register for.
</div>
<div id="navhowto" style="position:absolute;left:-11110px">
Use the tab key to enter and exit the menu. Use the arrow keys to navigate within the menu
</div>
<div id="menu_container" tabindex="0" aria-details="chooser">
    <ul role="menubar" aria-activedescendant="{ home || courses }" id="offerings" aria-describedby="navhowto" tabindex="0">
        <li role="menuitem" id="home">Home</li>
        <li role="menuitem" aria-haspopup="true" id="courses">Courses
            <ul role="menu" aria-expanded="{ true || false }">
                <li role="menuitem" id="economics">Economics</li>
                <li role="menuitem" id="compsci">Computer Science</li>
            </ul>
        </li>
    </ul>
</div>
```
- Example demonstrates:
    - Offscreen text
    - aria-labelledby / -details
    - role=menuitem, menu
    - aria-activedescendant
    - submenu:
        - aria-haspopup / -expanded

### Widget static attributes
- aria-haspopup: Indicates the availability and type of interactive popup element, such as menu or dialog, that can be triggered by an element.
- aria-modal: Indicates whether an element is modal when displayed
- aria-readonly: Indicates that the element is not editable but is otherwise operable.
- aria-required: Indicates that user input is required on the element before a form may be submitted.

### Live static regions
- aria-live: Indicates that an element will be updated and describes the types of updates the user agents, assistive technologies, and user can expect from the live region.
- aria-atomic: Indicates whether assistive technologies will present all, or only parts of, the changed region based on the change notifications defined by the aria-relevant attribute.
- aria-relevant: Indicates what notifications the user agent will trigger when the accessibility tree within a live region is modified.

## Browser and Screen Reader Support for WAI-ARIA
- May require short-term workarounds until support for WAI-ARIA is fully implemented
- [Support table](https://www.powermapper.com/tests/screen-readers/aria/)

## Graceful Degradation vs Progressive Enhancement
- progressive enhancement is preferred, since it focuses on always providing base functionality and planning for future enhancements
- expensive assistive tech = less upgrades = need to support +5 yrs
- Example: page nav
    - WAI-ARIA: landmarks
    - Always works: bypass links next to nav elements and at top of main content area
- Also: use redundant roles for new HTML el (nav, main)

## Validating WAI-ARIA
[W3C Web-based HTML Validator.](https://validator.w3.org/) Validates WAI-ARIA as part of HTML5
[Lighthouse.](https://developers.google.com/web/tools/lighthouse/) Adds a "Audit" tab
[ARIA Validator](https://chrome.google.com/webstore/detail/aria-validator/oigghlanfjgnkcndchmnlnmaojahnjoc)
[aXe](https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd)