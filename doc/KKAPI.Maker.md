## `AccessoriesApi`

Collection of methods useful for interfacing with character accessories. Has methods both for chara maker and  everywhere else.  Abstracts away MoreAccessories so you don't have to worry if it's installed or not.
```csharp
public static class KKAPI.Maker.AccessoriesApi

```

Static Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `Boolean` | AccessoryCanvasVisible | Returns true if the accessory tab in maker is currently selected.  If you want to know if the user can actually see the tab on the screen check `KKAPI.Maker.MakerAPI.IsInterfaceVisible`. | 
| `Boolean` | MoreAccessoriesInstalled | True if the MoreAccessories mod is installed.  Avoid relying on this and instead use other methods in this class since they will handle this for you. | 
| `Int32` | SelectedMakerAccSlot | Get the index of the currently selected accessory slot under Accessories group in Chara Maker.  If none are selected or chara maker is not opened, returns -1. 0-indexed.  Use `KKAPI.Maker.AccessoriesApi.SelectedMakerAccSlotChanged` to get notified when the selected slot changes. | 


Static Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `Int32` | GetAccessoryIndex(this `ChaControl` character, `GameObject` accessoryRootObject) | Get index of this accessory, or -1 if it doesn't exist for the specified character. | 
| `GameObject` | GetAccessoryObject(this `ChaControl` character, `Int32` index) | Get accessory objects of specified index for this character.  null will be returned if an accessory slot exists but has no accessory in it, or if the slot doesn't exist.  If index is below 0 or the character is null an exception will be thrown. | 
| `GameObject[]` | GetAccessoryObjects(this `ChaControl` character) | Get a list of all accessory objects for this character.  If an accessory slot exists but has no accessory in it, it will appear as null on the list. | 
| `Int32` | GetMakerAccessoryCount() | Get count of the UI entries for accessories (accessory slots).  Returns 0 outside of chara maker. | 
| `GameObject` | GetMakerAccessoryPageObject(`Int32` index = -1) | Get the root gameobject of the maker UI page for the specified accessory.  Returns null if the page doesn't exist or can't be accessed (e.g. when outside maker). | 
| `ChaControl` | GetOwningCharacter(`GameObject` accessoryRootObject) | Get the character that owns this accessory | 


Static Events

| Type | Name | Summary | 
| --- | --- | --- | 
| `EventHandler<AccessoryCopyEventArgs>` | AccessoriesCopied | Fires after user copies accessories between coordinates by using the Copy window. | 
| `EventHandler<AccessorySlotEventArgs>` | AccessoryKindChanged | Fires when user selects a different accessory in the accessory window. | 
| `EventHandler<AccessoryTransferEventArgs>` | AccessoryTransferred | Fires after user copies an accessory within a single coordinate by using the Transfer window. | 
| `EventHandler<AccessorySlotEventArgs>` | MakerAccSlotAdded | A new slot was added by MoreAccessories. Adding 10 slots triggers this 10 times. | 
| `EventHandler<AccessorySlotEventArgs>` | SelectedMakerAccSlotChanged | Fires whenever the index of the currently selected accessory slot under Accessories group in Chara Maker is changed.  This happens when user click on another slot. | 


## `AccessoryContolVisibilityArgs`

Event args for events that are related to accessory control visibility.
```csharp
public class KKAPI.Maker.AccessoryContolVisibilityArgs
    : EventArgs

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `Boolean` | Show | Visibility state of accessory control | 


## `AccessoryControlWrapper<T, TVal>`

A wrapper for custom controls used in accessory window (added by using `KKAPI.Maker.MakerAPI.AddAccessoryWindowControl``1(``0)`).  It abstracts away switching between accessory slots and provides a simple list of values for each accessory.
```csharp
public class KKAPI.Maker.AccessoryControlWrapper<T, TVal>

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `T` | Control | The wrapped control. | 
| `Int32` | CurrentlySelectedIndex | Index of the currently selected accessory. | 
| `Boolean` | IsDisposed | If true, the control has been disposed and can no longer be used, likely because the character maker exited.  A new control has to be created to be used again. | 


Events

| Type | Name | Summary | 
| --- | --- | --- | 
| `EventHandler<AccessorySlotEventArgs>` | AccessoryKindChanged | Fires when user selects a different accessory in the accessory window. | 
| `EventHandler<AccessoryWindowControlValueChangedEventArgs<TVal>>` | ValueChanged | Fired when the value of this control changes for any of the accessories. | 
| `EventHandler<AccessorySlotEventArgs>` | VisibleIndexChanged | Fired when the currently visible accessory was changed by the user clicking on one of the slots. | 


Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `TVal` | GetSelectedValue() | Get value of the control for the currently selected accessory. | 
| `TVal` | GetValue(`Int32` accessoryIndex) | Get value of the control for the specified accessory. | 
| `void` | SetSelectedValue(`TVal` value) | Set value of the control for the currently selected accessory. | 
| `void` | SetSelectedValue(`TVal` value, `Boolean` fireEvents) | Set value of the control for the currently selected accessory. | 
| `void` | SetValue(`Int32` accessoryIndex, `TVal` value) | Set value of the control for the specified accessory. | 
| `void` | SetValue(`Int32` accessoryIndex, `TVal` value, `Boolean` fireEvents) | Set value of the control for the specified accessory. | 


Static Events

| Type | Name | Summary | 
| --- | --- | --- | 
| `EventHandler<AccessoryCopyEventArgs>` | AccessoriesCopied | Fires after user copies accessories between coordinates by using the Copy window. | 
| `EventHandler<AccessoryTransferEventArgs>` | AccessoryTransferred | Fires after user copies an accessory within a single coordinate by using the Transfer window. | 


## `AccessoryCopyEventArgs`

Event args for accessory copy events.
```csharp
public class KKAPI.Maker.AccessoryCopyEventArgs
    : EventArgs

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `IEnumerable<Int32>` | CopiedSlotIndexes | Indexes of accessories that were selected to be copied. | 
| `CoordinateType` | CopyDestination | Coordinate the accessories are copied into. | 
| `CoordinateType` | CopySource | Coordinate the accessories are copied from. | 


## `AccessorySlotEventArgs`

Event args for events that are related to accessory slot indexes.
```csharp
public class KKAPI.Maker.AccessorySlotEventArgs
    : EventArgs

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `Int32` | SlotIndex | Currently opened accessory slot index. 0-indexed. | 


## `AccessoryTransferEventArgs`

Event args for accessory transfer events.
```csharp
public class KKAPI.Maker.AccessoryTransferEventArgs
    : EventArgs

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `Int32` | DestinationSlotIndex | Index the source accessory is copied to. | 
| `Int32` | SourceSlotIndex | Index of the source accessory. | 


## `AccessoryWindowControlValueChangedEventArgs<TVal>`

Event args used in `KKAPI.Maker.AccessoryControlWrapper`2`.
```csharp
public class KKAPI.Maker.AccessoryWindowControlValueChangedEventArgs<TVal>
    : EventArgs

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `TVal` | NewValue | Newly assigned value. | 
| `Int32` | SlotIndex | Index of the accessory the value was assigned to. | 


## `ChaFileLoadedEventArgs`

```csharp
public class KKAPI.Maker.ChaFileLoadedEventArgs
    : EventArgs

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `Boolean` | Body |  | 
| `ChaFileControl` | CharacterInstance |  | 
| `Boolean` | Coordinate |  | 
| `Boolean` | Face |  | 
| `String` | Filename |  | 
| `Boolean` | Hair |  | 
| `ChaFile` | LoadedChaFile | Use this to get extended data on the character | 
| `Boolean` | Parameter |  | 
| `Byte` | Sex |  | 


## `CharacterLoadFlags`

Specifies which parts of the character will be loaded when loading a card in character maker.  (It's the toggles at the bottom of load window) Only includes stock toggles.
```csharp
public class KKAPI.Maker.CharacterLoadFlags

```

Fields

| Type | Name | Summary | 
| --- | --- | --- | 
| `Boolean` | Body |  | 
| `Boolean` | Clothes |  | 
| `Boolean` | Face |  | 
| `Boolean` | Hair |  | 
| `Boolean` | Parameters |  | 


## `CharaLocalTextures`

API for global toggling of locally saved textures in Maker.  This module is activated only if Activate is called, SaveType is read / set, or if an action is registered to SaveTypeChangedEvent.
```csharp
public static class KKAPI.Maker.CharaLocalTextures

```

Static Fields

| Type | Name | Summary | 
| --- | --- | --- | 
| `EventHandler<CharaTextureSaveTypeChangedEventArgs>` | SaveTypeChangedEvent | Fired whenever SaveType changes | 


Static Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `CharaTextureSaveType` | SaveType | The type of texture saving that plugins should use | 


Static Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `Boolean` | Activate() | Activates the LocalTextures API | 


## `CharaTextureSaveType`

Options for the type of texture saving that plugins should use in Maker.
```csharp
public enum KKAPI.Maker.CharaTextureSaveType
    : Enum, IComparable, IFormattable, IConvertible

```

Enum

| Value | Name | Summary | 
| --- | --- | --- | 
| `0` | Bundled | Textures should be bundled with the card. | 
| `2` | Local | Textures should be saved separately from the card in a local folder. | 


## `CharaTextureSaveTypeChangedEventArgs`

Event argument used for when texture save type for cards is changed
```csharp
public class KKAPI.Maker.CharaTextureSaveTypeChangedEventArgs
    : EventArgs

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `CharaTextureSaveType` | NewSetting | The new state of the setting | 


## `CoordinateLoadFlags`

Specifies which parts of the coordinate will be loaded when loading a clothing card in character maker.
```csharp
public class KKAPI.Maker.CoordinateLoadFlags

```

Fields

| Type | Name | Summary | 
| --- | --- | --- | 
| `Boolean` | Accessories |  | 
| `Boolean` | Clothes |  | 


## `MakerAPI`

Provides a way to add custom items to the in-game Character Maker, and gives useful methods for interfacing with the maker.
```csharp
public static class KKAPI.Maker.MakerAPI

```

Static Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `Boolean` | CharaListIsLoading | Use to avoid unnecessary processing cards when they are loaded to the character list.  For example, don't load extended data for these characters since it's never used. | 
| `Boolean` | InsideAndLoaded | Maker is fully loaded and running | 
| `Boolean` | InsideMaker | The maker scene is currently loaded. It might still be loading! | 
| `ChaFile` | LastLoadedChaFile | ChaFile of the character currently opened in maker. Do not use to save extended data, or it will be lost when saving the card.  Use ChaFile from <code>ExtendedSave.CardBeingSaved</code> event to save extended data instead. | 


Static Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `T` | AddAccessoryWindowControl(`T` control) | Add a control to the accessory selection and settings window.  For editable controls that depend on the selected accessory use `KKAPI.Maker.MakerAPI.AddEditableAccessoryWindowControl``2(``0)`. | 
| `T` | AddAccessoryWindowControl(`T` control, `Boolean` automate_visible) | Add a control to the accessory selection and settings window.  For editable controls that depend on the selected accessory use `KKAPI.Maker.MakerAPI.AddEditableAccessoryWindowControl``2(``0)`. | 
| `T` | AddControl(`T` control) | Add custom controls. If you want to use custom sub categories, register them by calling AddSubCategory. | 
| `AccessoryControlWrapper<T, TVal>` | AddEditableAccessoryWindowControl(`T` control) | Add a control to the accessory selection and settings window. The control is wrapped to properly respond to changes in selected accessory slot (has unique values for each slot). | 
| `AccessoryControlWrapper<T, TVal>` | AddEditableAccessoryWindowControl(`T` control, `Boolean` automate_visible) | Add a control to the accessory selection and settings window. The control is wrapped to properly respond to changes in selected accessory slot (has unique values for each slot). | 
| `T` | AddSidebarControl(`T` control) | Add a control to the right sidebar in chara maker (the "Control Panel" where you set eye blinking, mouth expressions etc.) | 
| `ChaControl` | GetCharacterControl() | Get the ChaControl of the character serving as a preview in character maker.  Outside of character maker and early on in maker load process this returns null. | 
| `CharacterLoadFlags` | GetCharacterLoadFlags() | Get values of the default partial load checkboxes present at the bottom of the  character load window (load face, body, hair, parameters, clothes).  Returns null if the values could not be collected (safe to assume it's the same as being enabled). | 
| `CoordinateLoadFlags` | GetCoordinateLoadFlags() | Get which parts of the coordinate will be loaded when loading a clothing card in character maker.  Returns null if the values could not be collected (safe to assume it's the same as being enabled). | 
| `CoordinateType` | GetCurrentCoordinateType() | Currently selected maker coordinate | 
| `CustomBase` | GetMakerBase() | Returns current maker logic instance.  Same as `Singleton`1.Instance` | 
| `Int32` | GetMakerSex() | 0 is male, 1 is female | 
| `Boolean` | IsInsideClassMaker() | Check if the maker was loaded from within classroom select screen in main game | 
| `Boolean` | IsInterfaceVisible() | Check if maker interface is currently visible and not obscured by settings screen or other things.  Useful for knowing when to display OnGui mod windows in maker. | 


Static Events

| Type | Name | Summary | 
| --- | --- | --- | 
| `EventHandler<AccessoryContolVisibilityArgs>` | AccessoryContolVisibility | Fired when the visbility state of accessory controls, added by `KKAPI.Maker.MakerAPI.AddAccessoryWindowControl``1(``0)`, should change state if not managed automatically by the api. | 
| `EventHandler` | InsideMakerChanged | Firen whenever `KKAPI.Maker.MakerAPI.InsideMaker` changes. This is the earliest event fired when user starts the character maker. | 
| `EventHandler<RegisterCustomControlsEvent>` | MakerBaseLoaded | Maker is fully loaded. Use to load mods that rely on something that is loaded late, else use MakerStartedLoading.  This is the last chance to add custom controls!  Warning: All custom subcategories and custom controls are cleared on maker exit and need to be re-added on next maker  start. | 
| `EventHandler` | MakerExiting | Fired after the user exits the maker. Use this to clean up any references and resources.  You want to return to the state you were in before maker was loaded. | 
| `EventHandler` | MakerFinishedLoading | Maker is fully loaded and the user has control.  Warning: Avoid loading mods or doing anything heavy in this event. | 
| `EventHandler<RegisterCustomControlsEvent>` | MakerStartedLoading | Early in the process of maker loading. Most game components are initialized and had their Start methods ran.  Warning: Some components and objects might not be loaded or initialized yet, especially if they are mods.  Warning: All custom subcategories and custom controls are cleared on maker exit and need to be re-added on next maker  start. | 
| `EventHandler<RegisterSubCategoriesEvent>` | RegisterCustomSubCategories | This event is fired every time the character maker is being loaded, near the very beginning.  This is the only chance to add custom sub categories. Custom controls can be added now on later in `KKAPI.Maker.MakerAPI.MakerBaseLoaded`.  Warning: All custom subcategories and custom controls are cleared on maker exit and need to be re-added on next maker start.  It's recommended to completely clear your GUI state in `KKAPI.Maker.MakerAPI.MakerExiting` in preparation for loading into maker again. | 
| `EventHandler` | ReloadCustomInterface | Fired after character or coordinate is loaded in maker, after all controllers had their events fired.  This event is only fired when inside the character maker. Use this to update values of custom controls.  EventArgs can be either `KKAPI.Chara.CharaReloadEventArgs` or `KKAPI.Chara.CoordinateEventArgs` depending on why the reload happened. | 


## `MakerCardSave`

API for modifying the process of saving cards in maker.
```csharp
public static class KKAPI.Maker.MakerCardSave

```

Static Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `void` | RegisterNewCardSavePathModifier(`DirectoryPathModifier` directoryPathModifier, `CardNameModifier` filenameModifier) | Add a function that can modify the path of the saved cards.  Use sparingly and insert/replace parts of the path instead of overwriting the whole path to keep compatibility with other plugins. | 


## `MakerCategory`

Specifies a category inside character maker.
```csharp
public class KKAPI.Maker.MakerCategory

```

Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `String` | CategoryName | Main category gameObject name. Main categories are the square buttons at the top-left edge of the screen.  They contain multiple subcategories (tabs on the left edge of the screen). | 
| `String` | DisplayName | The text displayed on the subcategory tab on the left edge of the screen. | 
| `Int32` | Position | Numeric position of the subcategory.  When making new subcategories you can set this value to be in-between stock subcategories. | 
| `String` | SubCategoryName | Sub category gameObject name. Sub categories are the named tabs on the left edge of the screen.  They contain the actual controls (inside the window on the right of the tabs). | 


Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `Boolean` | Equals(`Object` obj) |  | 
| `Int32` | GetHashCode() |  | 
| `String` | ToString() | Get combined name for logging etc. | 


## `MakerConstants`

Useful values from the character maker. Mostly built-in categories for use with registering custom controls.
```csharp
public static class KKAPI.Maker.MakerConstants

```

Static Fields

| Type | Name | Summary | 
| --- | --- | --- | 
| `Color` | DefaultControlTextColor | Default text color for maker controls. | 


Static Properties

| Type | Name | Summary | 
| --- | --- | --- | 
| `IEnumerable<MakerCategory>` | BuiltInCategories | All ategories that are built-into the character maker by default. | 


Static Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `MakerCategory` | GetBuiltInCategory(`String` category, `String` subCategory) | Quick search for a built-in category. If you know what category you want to use at  compile time you can use the shortcuts instead, e.g. `KKAPI.Maker.MakerConstants.Face.Ear` | 


## `RegisterCustomControlsEvent`

Event fired when character maker is starting and plugins are given an opportunity to register custom controls
```csharp
public class KKAPI.Maker.RegisterCustomControlsEvent
    : EventArgs

```

Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `T` | AddControl(`T` control) | Add custom controls. If you want to use custom sub categories, register them by calling AddSubCategory. | 
| `MakerCoordinateLoadToggle` | AddCoordinateLoadToggle(`MakerCoordinateLoadToggle` toggle) | Add a toggle to the bottom of the "Load coordinate/clothes" window that allows for partial loading of coordinate cards. | 
| `MakerLoadToggle` | AddLoadToggle(`MakerLoadToggle` toggle) | Add a toggle to the bottom of the "Load character" window that allows for partial loading of characters. | 
| `T` | AddSidebarControl(`T` control) | Add a control to the right sidebar in chara maker (the "Control Panel" where you set eye blinking, mouth expressions etc.) | 


## `RegisterSubCategoriesEvent`

Event fired when character maker is starting and plugins are given an opportunity to register custom categories and controls
```csharp
public class KKAPI.Maker.RegisterSubCategoriesEvent
    : RegisterCustomControlsEvent

```

Methods

| Type | Name | Summary | 
| --- | --- | --- | 
| `void` | AddSubCategory(`MakerCategory` category) | Add custom sub categories. They need to be added before maker starts loading,  or in the RegisterCustomSubCategories event. | 


