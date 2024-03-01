---
title: Julia 之 VSCode 插件之快捷键与命令
authors: Ethan Lin
year: 2024-02-08
tags:
  - 类型/笔记
  - 日期/2024-02-08
  - 类型/转载
  - 内容/编程语言/Julia
---
# Julia 之 VSCode 插件之快捷键与命令





# [Keybindings & Commands](https://www.julia-vscode.org/docs/dev/userguide/keybindings/#Keybindings-and-Commands)

This page was auto-generated from [julia-vscode's package.json](https://github.com/julia-vscode/julia-vscode/blob/main/package.json) version 1.66.0.

## [Keyboard shortcuts](https://www.julia-vscode.org/docs/dev/userguide/keybindings/#Keyboard-shortcuts)

- Julia: Execute Code in REPL and Move: <kbd>Shift+Enter</kbd>
- Julia: Execute Code in REPL: <kbd>Ctrl+Enter</kbd>
- Julia: Execute Code Cell in REPL: <kbd>Alt+Enter</kbd>
- Julia: Execute Code Cell in REPL and Move: <kbd>Alt+Shift+Enter</kbd>
- Julia: Interrupt Execution: <kbd>Ctrl+C</kbd>
- Julia: Clear Current Inline Result: <kbd>Escape</kbd>
- Julia: Clear Inline Results In Editor: <kbd>Alt+J Alt+C</kbd>
- Julia: Select Current Module: <kbd>Alt+J Alt+M</kbd>
- Julia: New Julia File: <kbd>Alt+J Alt+N</kbd>
- Julia: Start REPL: <kbd>Alt+J Alt+O</kbd>
- Julia: Stop REPL: <kbd>Alt+J Alt+K</kbd>
- Julia: Restart REPL: <kbd>Alt+J Alt+R</kbd>
- Julia: Change Current Environment: <kbd>Alt+J Alt+E</kbd>
- Julia: Show Documentation: <kbd>Alt+J Alt+D</kbd>
- Julia: Show Plot: <kbd>Alt+J Alt+P</kbd>
- REPLVariables.focus: Alt+J Alt+W
- Julia: Interrupt Execution: <kbd>Ctrl+Shift+C</kbd>
- Julia: Browse Back Documentation: <kbd>Left</kbd>
- Julia: Browse Forward Documentation: <kbd>Right</kbd>
- Julia: Show Previous Plot: <kbd>Left</kbd>
- Julia: Show Next Plot: <kbd>Right</kbd>
- Julia: Show First Plot: <kbd>Home</kbd>
- Julia: Show Last Plot: <kbd>End</kbd>
- Julia: Delete plot: <kbd>Delete</kbd>
- Julia: Delete All Plots: <kbd>Shift+Delete</kbd>

## [Command overview](https://www.julia-vscode.org/docs/dev/userguide/keybindings/#Command-overview)

You can discover these yourself by opening the Command Palette with Ctrl/Cmd-Shift-P and searching for "julia".

- Julia: New Julia File (`language-julia.newJuliaFile`)
- Julia: Re-Index Language Server Cache (`language-julia.refreshLanguageServer`)
- Julia: Restart Language Server (`language-julia.restartLanguageServer`)
- Julia: Open Package Directory in New Window (`language-julia.openPackageDirectory`)
- Julia: Tag new package version (experimental) (`language-julia.tagNewPackageVersion`)
- Julia: Change Current Environment (`language-julia.changeCurrentEnvironment`)
- Julia: Start REPL (`language-julia.startREPL`)
- Julia: Connect external REPL (`language-julia.connectREPL`)
- Julia: Stop REPL (`language-julia.stopREPL`)
- Julia: Restart REPL (`language-julia.restartREPL`)
- Julia: Stop Test Process (`language-julia.stopTestProcess`)
- Julia: Disconnect external REPL (`language-julia.disconnectREPL`)
- Julia: Execute Code in REPL (`language-julia.executeCodeBlockOrSelection`)
- Julia: Send Current Line or Selection to REPL (`language-julia.executeJuliaCodeInREPL`)
- Julia: Execute Code in REPL and Move (`language-julia.executeCodeBlockOrSelectionAndMove`)
- Julia: Execute File in REPL (`language-julia.executeFile`)
- Julia: Execute active File in REPL (`language-julia.executeActiveFile`)
- Julia: Interrupt Execution (`language-julia.interrupt`)
- Julia: Toggle Linter (`language-julia.toggleLinter`)
- Julia Weave: Open Preview (`language-julia.weave-open-preview`)
- Julia Weave: Open Preview to the Side (`language-julia.weave-open-preview-side`)
- Julia Weave: Save to File... (`language-julia.weave-save`)
- Julia: Show Documentation (`language-julia.show-documentation`)
- Julia: Show Documentation Pane (`language-julia.show-documentation-pane`)
- Julia: Show Profiler (`language-julia.openProfiler`)
- Julia: Next Profiler (`language-julia.nextProfile`)
- Julia: Previous Profile (`language-julia.previousProfile`)
- Julia: Delete Profile (`language-julia.deleteProfile`)
- Julia: Delete All Profiles (`language-julia.deleteAllProfiles`)
- Julia: Save Profile (`language-julia.saveProfileToFile`)
- Julia: Show Plot Navigator (`language-julia.show-plot-navigator`)
- Julia: Browse Back Documentation (`language-julia.browse-back-documentation`)
- Julia: Browse Forward Documentation (`language-julia.browse-forward-documentation`)
- Julia: Show Plot (`language-julia.show-plotpane`)
- Julia: Show Next Plot (`language-julia.plotpane-next`)
- Julia: Show Previous Plot (`language-julia.plotpane-previous`)
- Julia: Show First Plot (`language-julia.plotpane-first`)
- Julia: Enable Plot Pane (`language-julia.plotpane-enable`)
- Julia: Disable Plot Pane (`language-julia.plotpane-disable`)
- Julia: Show Last Plot (`language-julia.plotpane-last`)
- Julia: Delete plot (`language-julia.plotpane-delete`)
- Julia: Copy Plot (`language-julia.copy-plot`)
- Julia: Save Plot (`language-julia.save-plot`)
- Julia: Delete All Plots (`language-julia.plotpane-delete-all`)
- Julia: Execute Code Cell in REPL (`language-julia.executeCell`)
- Julia: Execute Code Cell in REPL and Move (`language-julia.executeCellAndMove`)
- Julia: Move to Previous Cell (`language-julia.moveCellUp`)
- Julia: Move to Next Cell (`language-julia.moveCellDown`)
- Julia: Select Code Block (`language-julia.selectBlock`)
- Open in VS Code (`language-julia.showInVSCode`)
- Go to definition (`language-julia.workspaceGoToFile`)
- Julia: Clear All Inline Results (`language-julia.clearAllInlineResults`)
- Julia: Clear Inline Results In Editor (`language-julia.clearAllInlineResultsInEditor`)
- Julia: Clear Current Inline Result (`language-julia.clearCurrentInlineResult`)
- Julia: Select Current Module (`language-julia.chooseModule`)
- Julia: Run File in New Process (`language-julia.runEditorContents`)
- Julia: Debug File in New Process (`language-julia.debugEditorContents`)
- Julia: Change to This Directory (`language-julia.cdHere`)
- Julia: Activate This Environment (`language-julia.activateHere`)
- Julia: Activate Parent Environment (`language-julia.activateFromDir`)
- Julia: Clear Runtime Diagnostics (`language-julia.clearRuntimeDiagnostics`)
- Julia: Clear Runtime Diagnostics by Provider (`language-julia.clearRuntimeDiagnosticsByProvider`)
- Julia: Clear Inlay Hints (`language-julia.clearInlayHints`)
- Remove from compiled modules/functions (`language-julia.switchToInterpreted`)
- Julia: Add to compiled modules/functions (`language-julia.switchToCompiled`)
- Julia: Switch all to interpreted (`language-julia.switchAllToInterpreted`)
- Julia: Switch all to compiled (`language-julia.switchAllToCompiled`)
- Julia: Apply default compiled modules/functions (`language-julia.apply-compiled-defaults`)
- Julia: Clear compiled modules/functions (`language-julia.reset-compiled`)
- Julia: Refresh Compiled/Interpreted Pane (`language-julia.refreshCompiled`)
- Julia: Add symbol to compiled modules/functions (`language-julia.set-compiled-for-name`)
- Julia: Set current compiled modules/functions as default (`language-julia.set-current-as-default-compiled`)
- Julia: Enable Compiled Mode for the debugger (`language-julia.enable-compiled-mode`)
- Julia: Disable Compiled Mode for the debugger (`language-julia.disable-compiled-mode`)
- Restart (`language-julia.restartKernel`)
- Stop (`language-julia.stopKernel`)
- Show modules in Workspace (`language-julia.showModules`)
- Hide modules in Workspace (`language-julia.hideModules`)
