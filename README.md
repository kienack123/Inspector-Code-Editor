# Inspector Code Editor

Edit C# scripts and text files right in the Inspector, with no IDE.

Select a `.cs` file or a text asset (`.txt`, `.json`, `.xml`, `.csv`, `.yaml`, `.md`, …) in the Project window. The Inspector shows the file in an editable code view instead of Unity's read-only preview. Press **Ctrl+S** (Cmd+S) to save. A saved script compiles right away.

Any other text file (`.shader`, `.hlsl`, `.asmdef`, `.uss`, `.uxml`, …) opens with **Assets > Open in Code Editor Window**, or with the **Open Window** button.

To open the script behind a component, right-click its header in the Inspector and choose **Code Editor**. This also works on a ScriptableObject asset. The window opens on the class declaration. Scripts that are compiled into DLLs have no source, so the item doesn't appear for them.

## Install

Add this line to `dependencies` in `Packages/manifest.json`:

```json
"com.kienack123.inspector-code-editor": "https://github.com/kienack123/Inspector-Code-Editor.git#1.1.0"
```

## Features

- Syntax highlighting for C#, ShaderLab/HLSL, JSON, XML/UXML, JavaScript, USS/CSS, and YAML/INI.
- Every file has its own undo history of up to 500 steps. Typing goes back one word per step.
  - Ctrl+Z / Ctrl+Y (or Ctrl+Shift+Z) work on the file only while the caret is in its code. Anywhere else, including the find bar, they stay Unity's normal Undo, so changing the selection never gets between the steps of a file.
  - The history survives selecting other assets, script compilation and Play Mode. The 30 most recent files keep theirs.
- Unsaved text survives script compilation and Play Mode. Unity asks before quitting if a file is still unsaved.
- The file keeps its encoding (UTF-8, UTF-8 BOM or UTF-16) and its line endings (CRLF or LF) when saved.
- Indentation follows the file: tabs or spaces, detected per file.
- Smart Home, auto-indent on Enter, and Tab / Shift+Tab to indent or outdent a selection.
- Find and replace, with match case.
- Toggle line comment (Ctrl+/) and duplicate line or selection (Ctrl+D).
- Changes made outside Unity are picked up:
  - A file with no unsaved edits reloads by itself, and you can undo the reload.
  - A file with unsaved edits shows a banner to load the disk version or keep yours.
- Only the visible lines are drawn, so long scripts stay fast.
- Files in immutable packages (registry, git and built-in) open read-only. So do files that are not valid UTF-8, and `.bytes` files.

## Keys

| Key | Action |
|---|---|
| Ctrl+S | Save |
| Ctrl+Z / Ctrl+Y / Ctrl+Shift+Z | Undo / Redo in this file (caret in the code) |
| Ctrl+F, F3, Shift+F3 | Find, next, previous |
| Ctrl+G | Go to a line, or line:column. Clicking the Ln/Col status does the same |
| Ctrl+/ | Toggle line comment |
| Ctrl+D | Duplicate line or selection |
| Ctrl+A, Ctrl+C, Ctrl+X, Ctrl+V | Select all, copy, cut, paste. With nothing selected, copy and cut take the whole line |
| Tab / Shift+Tab | Indent / outdent |
| Ctrl+Left/Right, Ctrl+Backspace/Delete | Move or delete by word |
| Ctrl+Home / Ctrl+End | Start / end of file |
| Ctrl+Scroll (Cmd+Scroll) | Make the text bigger or smaller. The line under the mouse stays in place, and the size is kept as the Font size setting |

While the code view has focus, its shortcuts take priority over Unity's. Ctrl+S saves the file, not the scene, and keys such as W, E, R, F and Delete type text instead of changing tools. You can rebind them under **Edit > Shortcuts > Inspector Code Editor**.

## Settings

**Tools > Inspector Code Editor > Settings…** opens a window with a live preview. You can also reach it with **Settings…** in the code view's right-click menu.

The preview shows sample code in C#, JSON, Shader and XML.

- **Theme.** Pick one of the built-in themes, each shown with a strip of its colors:
  - Auto: Dark Modern in the dark editor skin, Light Modern in the light one
  - Dark Modern, Light Modern
  - Monokai, Dracula, One Dark
  - Solarized Dark, Solarized Light
  - GitHub Dark, GitHub Light
- **Colors.** Every color of the theme can be changed. Changing one copies the current theme into a **Custom** theme, which then shows up in the list. **Copy a Theme into Custom…** starts Custom over from any built-in theme.
- **Text.**
  - Font: a list of the monospace fonts installed on the computer, or any font name typed in.
  - Font size (Ctrl+Scroll over the code changes it too), tab size, and the indent style for files that don't show one.
  - Syntax highlighting on or off.
  - Line numbers: hidden, shown, or relative to the caret line.
- **Inspector.**
  - Turn the editor on or off for scripts and for text assets. When it is off, Unity's preview comes back.
  - Fill the Inspector height, or use a fixed height.
- **File Types.**
  - **Edit in the Inspector:** tick the text asset extensions that open in the code editor. The others keep Unity's preview. You can add extensions of your own.
  - **Highlight as:** pick the language used to color an extension, for example `.txt` as JSON. Unlisted extensions use their usual language. A file type added here can also be opened with Open in Code Editor Window.
- **Files.** Import after save, and the largest file to open.

The same settings, without the preview, are also under **Edit > Preferences > Inspector Code Editor**. Everything is stored per user in EditorPrefs.

## Notes

- The text is laid out on a fixed character grid. Characters wider than one cell, such as CJK and emoji, make the caret drift on that line. Latin text, including Vietnamese, lines up.
- Lines longer than 4,000 characters are drawn without highlighting.
- Mixed line endings are written back as the file's main line ending.
- Open in IDE opens the saved file. Save first if the IDE should see your current changes.
- Tested on Unity 6000.5. Unity 2022.3 or newer is required.
