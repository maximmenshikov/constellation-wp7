# constellation-wp7

This is one workspace for the Windows Phone 7 FullUnlock components. One
`basis install` clones all of them side by side. The workspace defines no build,
run, or test actions. Each project targets Visual Studio 2008, Windows Mobile 6,
and the WP7 SDK (ARMv4I). You build them on Windows with those toolchains, not
here.

Author: Maxim Menshikov (ultrashot).

## Components

On-device modules (the unlock chain):

- `clkflt` — a WinCE file-system filter (`clkflt.dll`). It redirects file
  lookups, so the OS serves patched copies of stock system modules.
- `ulv` — a loader verifier (`ulv.dll`). It stands in for
  `\Windows\mslvmod.dll` and relaxes module authentication, so unsigned code
  loads.
- `upl` — a policy engine (`upl.dll`). It stands in for the stock policy engine
  and grants access that the OS would normally deny. It links `ulv.lib` and
  `iri.lib`.

Usermode helpers:

- `accman` — an account manager (`accman.exe`). It elevates account privileges
  to full trust through the ADB API and `HKLM\Software\OEM\Accman`. It uses the
  shared `common` headers (github.com/maximmenshikov/common) as a git submodule.
- `uplhlp` — a policy helper (`uplhlp.exe`). It is the companion to `upl`. It
  watches the policy message queue and shows localized toast notifications. It
  links `StringLoader.lib`.

Shared library:

- `StringLoader` — a resource-string loader (`StringLoader.lib`). It loads
  localized strings from WP7 `.mui` resources. `uplhlp` uses it.

## Install

Run `basis install` to clone every component into this workspace. Each component
is its own git repository (`github.com/maximmenshikov/<name>`). Read each
component's README for its build steps.
