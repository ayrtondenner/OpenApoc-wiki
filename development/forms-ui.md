# Forms UI Library

The Forms library is OpenApoc's hierarchical, XML-driven UI framework. All game interface screens -- menus, base management, battle HUD, UFOpaedia -- are built from form definitions in `data/forms/` and rendered by the control classes in `forms/`.

## Overview

- **XML-based**: UI layouts are defined in `.form` files parsed by [pugixml](https://pugixml.org).
- **Hierarchical**: Controls form a parent-child tree. A `Form` is the root; all other controls nest inside it.
- **Event-driven**: Controls fire typed events (`ButtonClick`, `CheckBoxChange`, etc.) that game code handles via callbacks.
- **Smart-pointer managed**: All controls are `sp<Control>` (shared pointers from `library/sp.h`).

### Source Files

| Directory | Contents |
|-----------|----------|
| `forms/` | C++ control classes (`control.h`, `form.h`, `label.h`, etc.) |
| `forms/forms_enums.h` | Event types and alignment enumerations |
| `forms/ui.h` | `UI` singleton for form and font management |
| `data/forms/` | XML form definitions (~72 `.form` files) |

## XML Structure

Every form file follows this structure:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<openapoc>
  <form id="FORM_ID">
    <style minwidth="640" minheight="480">
      <!-- controls here -->
    </style>
  </form>
</openapoc>
```

- `<openapoc>` -- root wrapper element.
- `<form id="...">` -- the form definition. The `id` attribute is used for lookup.
- `<style minwidth="..." minheight="...">` -- a resolution-specific layout. The engine selects the style whose minimum dimensions best match the current window size.

### Common Child Elements

All control types support these child elements:

```xml
<!-- Position relative to parent -->
<position x="10" y="20"/>
<!-- x accepts: integer, "left", "centre", "right" -->
<!-- y accepts: integer, "top", "centre", "bottom" -->

<!-- Dimensions -->
<size width="200" height="32"/>
<!-- Accepts: integer, percentage ("50%"), or "item" (for listbox children) -->

<!-- Background colour (RGBA, 0-255; alpha defaults to 255) -->
<backcolour r="0" g="0" b="0" a="128"/>

<!-- Palette for indexed-colour rendering -->
<palette>path/to/palette.pal</palette>

<!-- Tooltip -->
<tooltip text="Tooltip text" font="smallset">
  <border colour="#RRGGBB" alpha="255" width="1"/>
</tooltip>
```

Common attributes on the control element itself:

| Attribute | Description |
|-----------|-------------|
| `id` | Control identifier, used by `findControl()` |
| `visible` | `"Y"` or `"N"` -- initial visibility |
| `border` | Show debug bounds |

### Real-World Example

From `data/forms/mainmenu.form`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<openapoc>
  <form id="FORM_MAINMENU">
    <style minwidth="640" minheight="480">
      <position x="centre" y="centre"/>
      <size width="640" height="480"/>
      <backcolour r="128" g="80" b="80"/>
      <graphic>
        <image>xcom3/ufodata/titles.pcx</image>
        <position x="0" y="0"/>
        <size width="640" height="480"/>
        <label text="OpenApoc">
          <backcolour r="255" g="255" b="255" a="192"/>
          <position x="0" y="0"/>
          <size width="640" height="32"/>
          <alignment horizontal="centre" vertical="centre"/>
          <font>bigfont</font>
        </label>
      </graphic>
      <textbutton id="BUTTON_NEWGAME" text="Start Campaign Game">
        <position x="centre" y="190"/>
        <size width="300" height="32"/>
        <font>smalfont</font>
      </textbutton>
      <textbutton id="BUTTON_QUIT" text="Quit">
        <position x="centre" y="340"/>
        <size width="300" height="32"/>
        <font>smalfont</font>
      </textbutton>
    </style>
  </form>
</openapoc>
```

## Control Types

All controls inherit from the base `Control` class (`forms/control.h`). The following sections document each control type, its XML tag name, key properties, and events.

### Control (Base Class)

**Class**: `Control` (`forms/control.h`)
**XML tag**: `<control>`

The root base class for all UI elements. Provides position, size, visibility, event handling, child management, and data attachment.

**Key properties**:

| Property | Type | Description |
|----------|------|-------------|
| `Name` | `UString` | Control identifier (set from `id` attribute) |
| `Location` | `Vec2<int>` | Position relative to parent |
| `Size` | `Vec2<int>` | Width and height |
| `SelectionSize` | `Vec2<int>` | Alternative hit-test area |
| `BackgroundColour` | `Colour` | RGBA background colour |
| `Visible` | `bool` | Visibility flag |
| `Enabled` | `bool` | Whether control accepts input |
| `takesFocus` | `bool` | Whether control can receive keyboard focus |
| `Controls` | `vector<sp<Control>>` | Child controls |
| `ToolTipText` | `UString` | Tooltip text |
| `ToolTipFont` | `sp<BitmapFont>` | Tooltip font |

**Key methods**:

| Method | Description |
|--------|-------------|
| `findControl(UString ID)` | Recursively search for a child by ID |
| `findControlTyped<T>(name)` | Type-safe search with dynamic_pointer_cast |
| `addCallback(FormEventType, callback)` | Register an event handler |
| `click()` | Simulate a mouse click |
| `setVisible(bool)` | Toggle visibility |
| `setData(sp<void>)` / `getData<T>()` | Attach/retrieve arbitrary user data |
| `createChild<T>(args...)` | Create and parent a new child control |
| `align(HAlign)` / `align(VAlign)` | Align within parent |

---

### Form

**Class**: `Form : public Control` (`forms/form.h`)
**XML tag**: `<form>` (root element, not used as a nested control)

Top-level container for a UI screen. Forms are loaded from `.form` files and serve as the root of the control hierarchy.

**Key methods**:

| Method | Description |
|--------|-------------|
| `Form::loadForm(path)` | Static -- load a form from an XML file path |
| `readFormStyle(node)` | Parse a `<style>` element |

**XML**:

```xml
<form id="FORM_NAME">
  <style minwidth="640" minheight="480">
    <!-- child controls -->
  </style>
</form>
```

**Subforms**: A form can embed another form using `<subform src="FORM_ID"/>`, which loads the referenced form via `ui().getForm()` and nests it as a child.

---

### Label

**Class**: `Label : public Control` (`forms/label.h`)
**XML tag**: `<label>`
**Events**: `ButtonClick` (when clicked)

Text display control with optional word wrapping and scroll support.

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `text` | `UString` | Display text (via `getText()`/`setText()`) |
| `font` | `sp<BitmapFont>` | Rendering font |
| `TextHAlign` | `HorizontalAlignment` | Horizontal text alignment |
| `TextVAlign` | `VerticalAlignment` | Vertical text alignment |
| `WordWrap` | `bool` | Enable word wrapping |
| `Tint` | `Colour` | Colour tint overlay |
| `scroller` | `sp<ScrollBar>` | Optional linked scrollbar for long text |

**XML**:

```xml
<label id="MY_LABEL" text="Hello World" scrollbarid="SCROLL_ID">
  <position x="0" y="0"/>
  <size width="200" height="20"/>
  <font>smalfont</font>
  <alignment horizontal="centre" vertical="top"/>
</label>
```

The `text` attribute can also be set in the element attributes. The optional `scrollbarid` attribute links an existing ScrollBar for scrollable content.

---

### TextButton

**Class**: `TextButton : public Control` (`forms/textbutton.h`)
**XML tag**: `<textbutton>`
**Events**: `ButtonClick`

A clickable button with text label. Supports three visual styles: Flat, Bevel, and Menu.

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `text` | `UString` | Button label (via `getText()`/`setText()`) |
| `font` | `sp<BitmapFont>` | Text font |
| `TextHAlign` | `HorizontalAlignment` | Horizontal text alignment |
| `TextVAlign` | `VerticalAlignment` | Vertical text alignment |
| `RenderStyle` | `ButtonRenderStyle` | `Flat`, `Bevel`, or `Menu` |

**XML**:

```xml
<textbutton id="BUTTON_OK" text="OK">
  <position x="centre" y="200"/>
  <size width="100" height="32"/>
  <font>smalfont</font>
</textbutton>
```

---

### GraphicButton

**Class**: `GraphicButton : public Control` (`forms/graphicbutton.h`)
**XML tag**: `<graphicbutton>`
**Events**: `ButtonClick`

An image-based button with separate images for normal, pressed, and hover states. Can be linked to ScrollBar controls for navigation (scroll prev/next).

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `image` | `sp<Image>` | Normal state image |
| `imagedepressed` | `sp<Image>` | Pressed state image |
| `imagehover` | `sp<Image>` | Hover state image |
| `ScrollBarPrev` | `sp<ScrollBar>` | Linked scrollbar (scroll backward on click) |
| `ScrollBarNext` | `sp<ScrollBar>` | Linked scrollbar (scroll forward on click) |
| `ScrollBarPrevHorizontal` | `sp<ScrollBar>` | Horizontal scroll backward |
| `ScrollBarNextHorizontal` | `sp<ScrollBar>` | Horizontal scroll forward |

**XML**:

```xml
<graphicbutton id="BUTTON_SCROLL_UP" scrollprev="MY_SCROLLBAR">
  <position x="0" y="0"/>
  <size width="24" height="24"/>
  <image>path/to/normal.png</image>
  <imagedepressed>path/to/pressed.png</imagedepressed>
  <imagehover>path/to/hover.png</imagehover>
</graphicbutton>
```

The `scrollprev` and `scrollnext` attributes reference a ScrollBar control by ID.

---

### Graphic

**Class**: `Graphic : public Control` (`forms/graphic.h`)
**XML tag**: `<graphic>`
**Events**: None (display-only, but can contain interactive children)

Displays an image with configurable alignment and fill method. Can auto-resize to match image dimensions.

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `image` | `sp<Image>` | Image to display |
| `ImageHAlign` | `HorizontalAlignment` | Horizontal image alignment |
| `ImageVAlign` | `VerticalAlignment` | Vertical image alignment |
| `ImagePosition` | `FillMethod` | `Stretch`, `Fit`, or `Tile` |
| `AutoSize` | `bool` | Auto-resize control to match image size |

**XML**:

```xml
<graphic id="BACKGROUND">
  <position x="0" y="0"/>
  <size width="640" height="480"/>
  <image>xcom3/ufodata/titles.pcx</image>
  <alignment horizontal="centre" vertical="centre"/>
  <imageposition>stretch</imageposition>
  <autosize>false</autosize>
</graphic>
```

---

### CheckBox

**Class**: `CheckBox : public Control` (`forms/checkbox.h`)
**XML tag**: `<checkbox>`
**Events**: `CheckBoxChange`, `CheckBoxSelected`, `CheckBoxDeSelected`

A toggle control with separate images for checked and unchecked states.

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `Checked` | `bool` | Current state (via `isChecked()`/`setChecked()`) |
| `imagechecked` | `sp<Image>` | Image when checked |
| `imageunchecked` | `sp<Image>` | Image when unchecked |

**XML**:

```xml
<checkbox id="CHECK_OPTION">
  <position x="10" y="10"/>
  <size width="24" height="24"/>
  <image>path/to/unchecked.png</image>
  <imagechecked>path/to/checked.png</imagechecked>
</checkbox>
```

---

### RadioButton

**Class**: `RadioButton : public CheckBox` (`forms/radiobutton.h`)
**XML tag**: `<radiobutton>`
**Events**: `CheckBoxChange`, `CheckBoxSelected`, `CheckBoxDeSelected` (inherited from CheckBox)

Extends CheckBox with mutual exclusion within a group. Only one radio button in a group can be checked at a time.

**Properties**: Inherits all CheckBox properties. Additionally uses a `RadioButtonGroup` identified by the `groupid` XML attribute.

**XML**:

```xml
<radiobutton id="RADIO_OPTION_1" groupid="MY_GROUP">
  <position x="10" y="10"/>
  <size width="24" height="24"/>
  <image>path/to/unchecked.png</image>
  <imagechecked>path/to/checked.png</imagechecked>
</radiobutton>
<radiobutton id="RADIO_OPTION_2" groupid="MY_GROUP">
  <position x="10" y="40"/>
  <size width="24" height="24"/>
  <image>path/to/unchecked.png</image>
  <imagechecked>path/to/checked.png</imagechecked>
</radiobutton>
```

The `groupid` attribute is **required**. Radio buttons with the same `groupid` form a mutually exclusive group.

---

### TriStateBox

**Class**: `TriStateBox : public Control` (`forms/tristatebox.h`)
**XML tag**: `<tristatebox>`
**Events**: `TriStateBoxChange`, `TriStateBoxState1Selected`, `TriStateBoxState2Selected`, `TriStateBoxState3Selected`

A three-state toggle control. Each click advances to the next state (0 -> 1 -> 2 -> 0).

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `State` | `int` | Current state 0, 1, or 2 (via `getState()`/`setState()`) |
| `image1` | `sp<Image>` | Image for state 0 |
| `image2` | `sp<Image>` | Image for state 1 |
| `image3` | `sp<Image>` | Image for state 2 |

**XML**:

```xml
<tristatebox id="TRISTATE_FILTER">
  <position x="10" y="10"/>
  <size width="24" height="24"/>
  <image>path/to/state0.png</image>
  <image2>path/to/state1.png</image2>
  <image3>path/to/state2.png</image3>
</tristatebox>
```

---

### ScrollBar

**Class**: `ScrollBar : public Control` (`forms/scrollbar.h`)
**XML tag**: `<scroll>`
**Events**: `ScrollBarChange`

A scrollbar control used for scrolling content or as a numeric slider. Supports both vertical and horizontal orientations.

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `Value` | `int` | Current position (via `getValue()`/`setValue()`) |
| `Minimum` | `int` | Range minimum (via `getMinimum()`/`setMinimum()`) |
| `Maximum` | `int` | Range maximum (via `getMaximum()`/`setMaximum()`) |
| `BarOrientation` | `Orientation` | `Vertical` or `Horizontal` |
| `RenderStyle` | `ScrollBarRenderStyle` | `Flat` or `Menu` |
| `GripperColour` | `Colour` | Colour of the scroll gripper |
| `ScrollChange` | `int` | Step size per click |
| `ScrollPercent` | `int` | Percentage of range per mouse wheel step |

**Key methods**:

| Method | Description |
|--------|-------------|
| `scrollPrev(amount)` | Scroll backward by amount (0 = use ScrollChange) |
| `scrollNext(amount)` | Scroll forward by amount |
| `scrollMin()` / `scrollMax()` | Jump to minimum/maximum |
| `scrollWheel(Event *e)` | Handle mouse wheel input |

**XML**:

```xml
<scroll id="MY_SCROLLBAR" scrollpercent="10" scrollchange="1">
  <position x="200" y="0"/>
  <size width="16" height="256"/>
  <gripperimage>path/to/gripper.png</gripperimage>
  <grippercolour r="220" g="192" b="192" a="255"/>
  <range min="0" max="100"/>
</scroll>
```

Note: The XML tag is `<scroll>`, not `<scrollbar>`.

---

### ListBox

**Class**: `ListBox : public Control` (`forms/listbox.h`)
**XML tag**: `<listbox>`
**Events**: `ListBoxChangeHover`, `ListBoxChangeSelected`

A scrollable list of child controls. Items are typically added programmatically via `addItem()`. Can use an internal or external ScrollBar.

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `scroller` | `sp<ScrollBar>` | Linked scrollbar (internal or external) |
| `ItemSize` | `int` | Height (vertical) or width (horizontal) of each item |
| `ItemSpacing` | `int` | Spacing between items in pixels |
| `ListOrientation` | `Orientation` | `Vertical` or `Horizontal` |
| `ScrollOrientation` | `Orientation` | Scroll direction (can differ from list direction) |
| `HoverColour` | `Colour` | Overlay colour for hovered item |
| `SelectedColour` | `Colour` | Overlay colour for selected item |
| `HoverImage` | `sp<Image>` | Alternative image for hover effect |
| `SelectedImage` | `sp<Image>` | Alternative image for selection effect |
| `AutoSelect` | `bool` | Automatically select first item (default: true) |

**Key methods**:

| Method | Description |
|--------|-------------|
| `addItem(sp<Control>)` | Add a control as a list item |
| `removeItem(sp<Control>)` | Remove an item |
| `clear()` | Remove all items |
| `setSelected(sp<Control>)` | Set the selected item |
| `getSelectedItem()` | Get the currently selected item |
| `getHoveredItem()` | Get the currently hovered item |
| `getSelectedData<T>()` | Get data attached to the selected item |
| `getHoveredData<T>()` | Get data attached to the hovered item |
| `removeByData<T>(sp<T>)` | Remove an item by its attached data |

**XML**:

```xml
<listbox id="MY_LIST" scrollbarid="MY_SCROLLBAR">
  <position x="0" y="0"/>
  <size width="200" height="300"/>
  <item size="32" spacing="6"/>
  <hovercolour r="255" g="255" b="255" a="64"/>
  <selcolour r="128" g="128" b="255" a="128"/>
</listbox>
```

The `scrollbarid` attribute references an existing `<scroll>` element. If omitted, the listbox creates an internal scrollbar. Items are added programmatically -- child controls with `<size height="item"/>` will auto-size to match `ItemSize`.

---

### MultilistBox

**Class**: `MultilistBox : public Control` (`forms/multilistbox.h`)
**XML tag**: `<multilistbox>`
**Events**: `ListBoxChangeHover`, `ListBoxChangeSelected`

Like ListBox, but supports selecting multiple items simultaneously. Provides customizable callbacks for visibility filtering, selection handling, and render effects.

**Properties**: Same as ListBox (`ItemSize`, `ItemSpacing`, `ListOrientation`, `ScrollOrientation`, `HoverColour`, `SelectedColour`, etc.).

**Additional methods**:

| Method | Description |
|--------|-------------|
| `setSelected(sp<Control>, bool)` | Select or deselect a specific item |
| `selectAll()` | Select all items |
| `clearSelection()` | Deselect all items |
| `getSelectedItems()` | Get ordered vector of selected items |
| `getSelectedSet()` | Get the set of selected controls directly |
| `setFuncIsVisibleItem(func)` | Custom visibility filter for items |
| `setFuncHandleSelection(func)` | Custom selection logic |
| `setFuncHoverItemRender(func)` | Custom hover rendering |
| `setFuncSelectionItemRender(func)` | Custom selection rendering |

**XML**: Same structure as `<listbox>`.

---

### TextEdit

**Class**: `TextEdit : public Control` (`forms/textedit.h`)
**XML tag**: `<textedit>`
**Events**: `TextChanged`, `TextEditFinish`, `TextEditCancel`, `KeyDown`, `KeyPress`

A text input field with cursor, character filtering, and max-length support. Text is stored internally as UTF-32.

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `text` | `U32String` | Input text (via `getText()`/`setText()` which convert to/from UString) |
| `font` | `sp<BitmapFont>` | Rendering font |
| `cursor` | `UString` | Cursor character (default: `"*"`) |
| `SelectionStart` | `unsigned int` | Cursor position |
| `TextHAlign` | `HorizontalAlignment` | Horizontal text alignment |
| `TextVAlign` | `VerticalAlignment` | Vertical text alignment |

**Key methods**:

| Method | Description |
|--------|-------------|
| `setText(UString)` / `getText()` | Set/get text content |
| `setAllowedCharacters(UString)` | Restrict input to specific characters (empty = all) |
| `setTextMaxSize(size_t)` | Set maximum text length |
| `setCursor(UString)` | Set cursor display character |

**XML**:

```xml
<textedit id="INPUT_NAME" text="initial text">
  <position x="10" y="10"/>
  <size width="200" height="24"/>
  <font>smalfont</font>
  <alignment horizontal="left" vertical="centre"/>
</textedit>
```

Click to start editing, press Enter or click outside to finish (fires `TextEditFinish`). Press Escape to cancel (fires `TextEditCancel`).

---

### Ticker

**Class**: `Ticker : public Control` (`forms/ticker.h`)
**XML tag**: `<ticker>`
**Events**: None (display-only)

A scrolling text marquee that displays queued messages one at a time with an animation effect.

**Properties**:

| Property | Type | Description |
|----------|------|-------------|
| `TextHAlign` | `HorizontalAlignment` | Horizontal text alignment |
| `TextVAlign` | `VerticalAlignment` | Vertical text alignment |

**Key methods**:

| Method | Description |
|--------|-------------|
| `addMessage(UString)` | Queue a message for display |
| `hasMessages()` | Check if any messages remain (queued or displayed) |

**Timing**: Each message animates in over 60 ticks and displays for 600 ticks (~10 seconds at 60 FPS).

**XML**:

```xml
<ticker id="NEWS_TICKER">
  <position x="0" y="460"/>
  <size width="640" height="20"/>
  <font>smalfont</font>
  <alignment horizontal="centre" vertical="centre"/>
</ticker>
```

---

## Events Reference

All event types are defined in `forms/forms_enums.h` as `FormEventType`:

### Input Events

| Event | Description |
|-------|-------------|
| `MouseEnter` | Mouse cursor enters control bounds |
| `MouseLeave` | Mouse cursor leaves control bounds |
| `MouseDown` | Mouse button pressed inside control |
| `MouseUp` | Mouse button released inside control |
| `MouseMove` | Mouse moved inside control |
| `MouseClick` | Complete click (down + up) inside control |
| `KeyDown` | Key pressed while control has focus |
| `KeyPress` | Key character generated while focused |
| `KeyUp` | Key released while control has focus |
| `TextInput` | Text input event (IME/composition) |

### Focus Events

| Event | Description |
|-------|-------------|
| `GotFocus` | Control received keyboard focus |
| `LostFocus` | Control lost keyboard focus |

### Tooltip

| Event | Description |
|-------|-------------|
| `ToolTip` | Tooltip display triggered |

### Control-Specific Events

| Event | Fired By | Description |
|-------|----------|-------------|
| `ButtonClick` | TextButton, GraphicButton, Label | Click completed |
| `CheckBoxChange` | CheckBox, RadioButton | Checked state changed |
| `CheckBoxSelected` | CheckBox, RadioButton | Became checked |
| `CheckBoxDeSelected` | CheckBox, RadioButton | Became unchecked |
| `TriStateBoxChange` | TriStateBox | State changed |
| `TriStateBoxState1Selected` | TriStateBox | Entered state 0 |
| `TriStateBoxState2Selected` | TriStateBox | Entered state 1 |
| `TriStateBoxState3Selected` | TriStateBox | Entered state 2 |
| `ScrollBarChange` | ScrollBar | Value changed |
| `TextChanged` | TextEdit | Text content modified |
| `TextEditFinish` | TextEdit | Editing completed (Enter or click outside) |
| `TextEditCancel` | TextEdit | Editing cancelled (Escape) |
| `ListBoxChangeHover` | ListBox, MultilistBox | Hovered item changed |
| `ListBoxChangeSelected` | ListBox, MultilistBox | Selected item changed |

### Registering Callbacks

```cpp
auto button = form->findControlTyped<TextButton>("BUTTON_OK");
button->addCallback(FormEventType::ButtonClick, [](FormsEvent *e) {
    LogInfo("OK button clicked");
});
```

Multiple callbacks can be registered for the same event type on the same control.

## Enumerations

Defined in `forms/forms_enums.h`:

```cpp
enum class HorizontalAlignment { Left, Centre, Right };
enum class VerticalAlignment   { Top, Centre, Bottom };
enum class FillMethod          { Stretch, Fit, Tile };
enum class Orientation         { Vertical, Horizontal };
```

In XML, these are specified as lowercase strings: `"left"`, `"centre"`, `"right"`, `"top"`, `"bottom"`, `"stretch"`, `"fit"`, `"tile"`, `"vertical"`, `"horizontal"`.

## Image Path Formats

Controls that display images accept paths in several formats:

1. **Direct file path**: `xcom3/ufodata/titles.pcx` -- loads an image file from the virtual filesystem.
2. **PCK sprite**: `PCK:pck_file:tab_file:sprite_index:palette_file` -- extracts a single sprite from a packed sprite sheet. Example: `PCK:xcom3/ufodata/newbut.pck:xcom3/ufodata/newbut.tab:26:xcom3/ufodata/base.pcx`.

## Form Loading

### From File

```cpp
auto form = Form::loadForm("data/forms/mainmenu.form");
```

### Via the UI Singleton

The `UI` class (`forms/ui.h`) caches loaded forms and fonts:

```cpp
auto form = ui().getForm("FORM_MAINMENU");
auto font = ui().getFont("smalfont");
```

| Method | Description |
|--------|-------------|
| `ui().getForm(UString ID)` | Load or retrieve a cached form by ID |
| `ui().getFont(UString name)` | Load or retrieve a cached font by name |
| `ui().getFormIDs()` | List all available form IDs |
| `ui().reloadFormsXml()` | Reload all form definitions from disk |

### Loading Pipeline

1. `Form::loadForm()` reads the XML file.
2. `readFormStyle()` selects the appropriate `<style>` node based on window dimensions.
3. `configureFromXml()` recursively processes the DOM:
   - `configureSelfFromXml()` parses the element's own attributes and child elements.
   - `configureChildrenFromXml()` iterates child elements, creates the appropriate control class by tag name, and recurses.
4. Cross-references (scrollbar links, radio groups) are resolved as controls are created.

## Programmatic Usage Patterns

### Finding Controls

```cpp
// Untyped lookup (returns sp<Control>)
auto ctrl = form->findControl("BUTTON_OK");

// Type-safe lookup (returns sp<TextButton>, logs error if not found or wrong type)
auto button = form->findControlTyped<TextButton>("BUTTON_OK");
```

### Creating Controls in Code

```cpp
auto label = parent->createChild<Label>("Hello World", font);
label->Location = {10, 20};
label->Size = {200, 32};
```

### Attaching User Data

Controls can carry arbitrary data via `setData()`/`getData<T>()`. This is commonly used with ListBox items:

```cpp
// Attach data to a list item
auto item = mksp<Label>(vehicle->name, font);
item->setData(vehicle);
listbox->addItem(item);

// Retrieve data from the selected item
auto selectedVehicle = listbox->getSelectedData<Vehicle>();
```

### Embedding Subforms

Use `<subform>` to embed one form inside another:

```xml
<subform src="FORM_OTHER_ID">
  <position x="0" y="100"/>
  <size width="640" height="380"/>
</subform>
```

The `src` attribute specifies the form ID to load via `ui().getForm()`.

## Form Files in the Repository

Form files are organized under `data/forms/`:

| Directory | Contents |
|-----------|----------|
| `data/forms/` | Top-level screens (main menu, options, base, research, recruit, save/load, etc.) |
| `data/forms/battle/` | Battle interface forms |
| `data/forms/city/` | Cityscape interface forms |

Notable files: `mainmenu.form`, `options.form`, `basescreen.form`, `aequipscreen.form`, `researchscreen.form`, `ufopaedia.form`, `battle/battle.form`.

## See Also

- [Architecture](architecture.md) -- codebase structure overview
- [Coding Style](coding-style.md) -- code style conventions
- [Data Formats](data-formats.md) -- XML data format reference
