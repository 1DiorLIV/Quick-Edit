This project is a Chrome extension called "Quick Edit" that allows users to quickly edit selected text on a webpage through a right-click context menu.

### Features
* **Context Menu Integration**: Right-click on any selected text to bring up the "Quick Edit" option.
* **Intuitive Editor Popup**: A sleek, modern popup appears with the selected text, ready for editing. The popup features a glassmorphism design, adapting to light and dark modes.
* **Keyboard Shortcuts**:
    * `Enter`: Saves the changes and closes the editor.
    * `Escape`: Discards changes and closes the editor.
    * `Tab`: Inserts a new line within the editor.
* **Drag-and-Drop Functionality**: The editor popup can be dragged and repositioned on the screen.
* **Snackbar Notifications**: Provides subtle feedback (e.g., "Changes saved!") using a temporary snackbar.
* **Responsive Design**: The popup adjusts its size and position to fit within the viewport.
* **Cross-Browser Compatibility**: Designed for Chrome, but the core functionalities are standard web technologies.

### Files

* `background.js`: This script is the service worker for the Chrome extension.
    * It listens for the `onInstalled` event to create a context menu item named "Quick Edit".
    * This context menu item only appears when text is selected.
    * When the "Quick Edit" menu item is clicked, it executes a script in the active tab to send a message containing the selected text to the content script.

* `content.js`: This script is injected into every webpage.
    * It dynamically inserts CSS for the snackbar and the editor popup, including styles for light and dark modes and scrollbar hiding.
    * The `showSnackbar` function displays a temporary notification message at the bottom of the screen.
    * It listens for messages from `background.js` to trigger the creation of the editor popup.
    * The `sanitizeText` function prevents XSS attacks by sanitizing user input.
    * The `replaceTextInRange` function handles replacing the original selected text with the edited text, supporting single and multi-node text selections.
    * The `createEditorPopup` function creates, styles, and manages the interactive editor popup, including:
        * Setting up the textarea with the selected text.
        * Implementing keyboard shortcuts for saving (Enter), canceling (Escape), and new lines (Tab).
        * Adding drag functionality for the popup header.
        * Applying zoom and fade effects for opening and closing the popup.

* `manifest.json`: This file provides essential information about the extension.
    * It declares the manifest version, name, version, and description.
    * It requests `contextMenus` and `scripting` permissions.
    * It defines the `background.js` as the service worker.
    * It specifies `content.js` to be injected into all URLs at `document_idle` run time.
    * It requests `host_permissions` for all URLs (`<all_urls>`).
    * It defines the extension's icons and default action.

### Installation

To install this Chrome extension:

1.  Download the project files.
2.  Open Chrome and navigate to `chrome://extensions/`.
3.  Enable "Developer mode" in the top right corner.
4.  Click "Load unpacked" and select the project directory.
5.  The "Quick Edit" extension icon will appear in your browser toolbar.

### Usage

1.  Select any text on a webpage.
2.  Right-click on the selected text.
3.  Choose "Quick Edit" from the context menu.
4.  An editor popup will appear with the selected text.
5.  Edit the text as desired.
6.  Press `Enter` to save your changes, or `Escape` to cancel.
7.  Use `Tab` for a new line within the editor.
