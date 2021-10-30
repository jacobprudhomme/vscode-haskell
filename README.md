# Haskell for Visual Studio Code

[![vsmarketplacebadge](https://vsmarketplacebadge.apphb.com/version/haskell.haskell.svg)](https://marketplace.visualstudio.com/items?itemName=haskell.haskell)

This extension adds language support for [Haskell](https://haskell.org), powered by the [Haskell Language Server](https://github.com/haskell/haskell-language-server).  
As almost all features are provided by the server you might find interesting read its [documentation](https://haskell-language-server.readthedocs.io).

## Features

You can watch demos for some of these features [here](https://haskell-language-server.readthedocs.io/en/latest/features.html#demos).

- Warning and error diagnostics from GHC
- Type information and documentation on hover, [including your own comments](./configuration.md#how-to-show-local-documentation-on-hover).
- Jump to definition: [for now only for local code definitions](https://github.com/haskell/haskell-language-server/issues/708)
- Document symbols
- Highlight references in document
- Code completion
- Show documentation and sources in hackage
- Formatting via [Brittany](https://github.com/lspitzner/brittany), [Floskell](https://github.com/ennocramer/floskell), [Fourmolu](https://github.com/fourmolu/fourmolu), [Ormolu](https://github.com/tweag/ormolu) or [Stylish Haskell](https://github.com/haskell/stylish-haskell)
- [Multi-root workspace](https://code.visualstudio.com/docs/editor/multi-root-workspaces) support
- [Code evaluation](https://haskell-language-server.readthedocs.io/en/latest/features.html#code-evaluation), see its [Tutorial](https://github.com/haskell/haskell-language-server/blob/master/plugins/hls-eval-plugin/README.md)
- [Integration with](https://haskell-language-server.readthedocs.io/en/latest/features.html#retrie-integration) [retrie](https://hackage.haskell.org/package/retrie), a powerful, easy-to-use codemodding tool
- [Code lenses for explicit import lists](https://haskell-language-server.readthedocs.io/en/latest/features.html#explicit-import-lists)
- [Generate functions from type signatures, and intelligently complete holes using](https://haskell-language-server.readthedocs.io/en/latest/features.html#wingman) [Wingman (tactics)](https://github.com/haskell/haskell-language-server/tree/master/plugins/hls-tactics-plugin)
- [Integration](https://haskell-language-server.readthedocs.io/en/latest/features.html#hlint) with [hlint](https://github.com/ndmitchell/hlint), the most used haskell linter, to show diagnostics and apply hints via [apply-refact](https://github.com/mpickering/apply-refact)
- [Module name suggestions](https://haskell-language-server.readthedocs.io/en/latest/features.html#module-names) for insertion or correction
- [Call hierarchy support](https://haskell-language-server.readthedocs.io/en/latest/features.html#call-hierarchy)

## Requirements

- For standalone `.hs`/`.lhs` files, [ghc](https://www.haskell.org/ghc/) must be installed and on the PATH. The easiest way to install it is with [ghcup](https://www.haskell.org/ghcup/) or [Chocolatey](https://www.haskell.org/platform/windows.html) on Windows.
- For Cabal based projects, both ghc and [cabal-install](https://www.haskell.org/cabal/) must be installed and on the PATH. It can also be installed with [ghcup](https://www.haskell.org/ghcup/) or [Chocolatey](https://www.haskell.org/platform/windows.html) on Windows.
- For Stack based projects, [stack](http://haskellstack.org) must be installed and on the PATH.
- If you are installing from an offline VSIX file, you need to install [language-haskell](https://github.com/JustusAdam/language-haskell) too after installation (either from the marketplace or offline).

## Configuration options

For a general picture about the server configuration, including the project setup, [you can consult the server documentation about the topic](https://haskell-language-server.readthedocs.io/en/latest/configuration.html).

### Path to server executable

If your server is manually installed and not on your path, you can also manually set the path to the executable.

```json
"haskell.serverExecutablePath": "~/.local/bin/haskell-language-server"
```

There are a few placeholders which will be expanded:

- `~`, `${HOME}` and `${home}` will be expanded into your users' home folder.
- `${workspaceFolder}` and `${workspaceRoot}` will expand into your current project root.

#### Security warning

The option has `resource` scope so it can be changed per workspace.
This supposes it could be used to execute arbitrary programs adding a `.vscode/settings.json` in the workspace folder including this option with the appropiate path.
For this reason its scope will be changed to `machine` so users only will be able to change it globally.
See #387 for more details.

### Downloaded binaries

This extension will download `haskell-language-server` binaries to a specific location depending on your system. If you find yourself running out of disk space, you can try deleting old versions of language servers in this directory. The extension will redownload them, no strings attached.

| Platform | Path                                                                      |
| -------- | ------------------------------------------------------------------------- |
| macOS    | `~/Library/Application\ Support/Code/User/globalStorage/haskell.haskell/` |
| Windows  | `%APPDATA%\Code\User\globalStorage\haskell.haskell`                       |
| Linux    | `$HOME/.config/Code/User/globalStorage/haskell.haskell`                   |

Note that if `haskell-language-server-wrapper`/`haskell-language-server` is already on the PATH, then the extension will launch it directly instead of downloading binaries.

### Supported GHC versions

These are the versions of GHC that there are binaries of `haskell-language-server` for. Building from source may support more versions!

| GHC                                                                              | Linux | macOS | Windows |
| -------------------------------------------------------------------------------- | ----- | ----- | ------- |
| 9.0.1 ([limited](https://github.com/haskell/haskell-language-server/issues/297)) | ✓     | ✓     | ✓       |
| 8.10.7                                                                           | ✓     | ✓     | ✓       |
| 8.10.6                                                                           | ✓     | ✓     | ✓       |
| 8.10.5                                                                           | ✓     | ✓     | ✓       |
| 8.10.4                                                                           | ✓     | ✓     | ✓       |
| 8.10.3                                                                           | ✓     | ✓     | ✓       |
| 8.10.2                                                                           | ✓     | ✓     | ✓       |
| 8.8.4                                                                            | ✓     | ✓     | ✓       |
| 8.8.3                                                                            | ✓     | ✓     |         |
| 8.6.5                                                                            | ✓     | ✓     | ✓       |
| 8.6.4                                                                            | ✓     | ✓     | ✓       |

The exact list of binaries can be checked in the last release of haskell-language-server: <https://github.com/haskell/haskell-language-server/releases/latest>  
You can check the current GHC versions support status and the policy followed for deprecations [here](https://haskell-language-server.readthedocs.io/en/latest/supported-versions.html).

## Using multi-root workspaces

First, check out [what multi-root workspaces](https://code.visualstudio.com/docs/editor/multi-root-workspaces) are. The idea of using multi-root workspaces, is to be able to work on several different Haskell projects, where the GHC version or stackage LTS could differ, and have it work smoothly.

The language server is now started for each workspace folder you have in your multi-root workspace, and several configurations are on a resource (i.e. folder) scope, instead of window (i.e. global) scope.

## Investigating and reporting problems

1. Go to extensions and right click `Haskell Language Server` and choose `Extensions Settings`
2. Scroll down to `Haskell › Trace: Server` and set it to `messages`
3. Set `Haskell › Trace: Client` to `debug`
4. Restart vscode and reproduce your problem
5. Go to the main menu and choose `View -> Output` (`Ctrl + Shift + U`)
6. On the new Output panel that opens on the right side in the drop down menu choose `Haskell (<your project>)`

Please include the output when filing any issues on the [haskell-language-server](https://github.com/haskell/haskell-language-server/issues/new) issue tracker.

### Troubleshooting

- Sometimes the language server might get stuck in a rut and stop responding to your latest changes.
  Should this occur you can try restarting the language server with <kbd>Ctrl</kbd> <kbd>shift</kbd> <kbd>P</kbd>/<kbd>⌘</kbd> <kbd>shift</kbd> <kbd>P</kbd> > Restart Haskell LSP Server.
- Usually the error or unexpected behaviour is already reported in the [haskell language server issue tracker](https://github.com/haskell/haskell-language-server/issues). Finding the issue could be useful to help resolve it and sometimes includes a workaround for the issue.

## Contributing

If you want to help, get started by reading [Contributing](https://github.com/haskell/vscode-haskell/blob/master/Contributing.md) for more details.

## Release Notes

See the [Changelog](https://github.com/haskell/vscode-haskell/blob/master/Changelog.md) for more details.
