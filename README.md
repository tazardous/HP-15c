# RPN-15 Scientific Programmable

Emulator of the HP-15C, keystroke for keystroke. One self-contained HTML file, no
build step. The only network request is for Google Fonts. Offline, the page falls
back to system fonts.

## Deploy

Settings -> Pages -> Deploy from a branch -> main -> / (root). Then open the URL in
Chrome on the phone and use the menu to Add to Home screen.

Everything is relative-pathed, so a project subdirectory works.

## Behaviour

Built from the HP-15C Owner's Handbook. Numbers are held to 10 significant digits
and every result is rounded to 10 digits, as on the real machine.

- **Stack** — four levels plus LAST X. Stack lift is enabling, disabling or neutral
  as listed in Appendix B. ENTER, CLx, ← and Σ+/Σ− disable lift.
- **Memory** — the 64 shared registers from Appendix C. They are split between data
  registers, program bytes (one- and two-byte instructions), matrix elements and the
  imaginary stack. `g MEM` shows `dd uu pp-b`. `f DIM (i)` moves the boundary.
  Indirect addressing through `(i)` reaches R0–R65.
- **Programming** — up to 448 bytes. Supported: labels A–E, 0–9 and .0–.9, GTO/GSB
  (including `GTO I`, `GSB I` and negative-I line numbers), seven subroutine levels,
  DSE/ISG, flags, the TEST 0–9 comparisons, PSE and R/S. SST and BST step in both
  modes, and `GTO CHS nnn` jumps to a line. In USER mode, matrix STO/RCL lines
  record as `u` and skip the next line when the last element wraps around.
- **SOLVE and ∫xy** — call the user's program as f(x). The integration accuracy
  follows the display format. A SOLVE or ∫ nested inside itself gives Error 7.
- **Complex mode** — `f I`, `f Re⇄Im`, `f (i)` and flags 8/9. There is an imaginary
  stack. Complex versions cover arithmetic, yˣ, roots, logs, trig, hyperbolics and
  their inverses, plus →P/→R on X.
- **Matrices** — A–E, up to 64 elements in all, with a result matrix and USER-mode
  element sequencing. Supported: `STO/RCL g`, scalar and matrix arithmetic, the
  inverse, the AX = B solve (LU form shown with dashes) and `MATRIX 0–9`. `Py,x` and
  `Cy,x` convert between the complex-matrix forms.
- **Errors** — 0 through 11 and Pr Error, as in Appendix A.
- **ON combinations** — with the calculator off, `−` then ON resets Continuous
  Memory. `.` then ON swaps the decimal point and comma.

The page also has an example runner, live stack, register, matrix and program-memory
panels, a physical-keyboard map, and a flip-over reference card. State is saved in
the browser's localStorage, which acts as Continuous Memory.

Differences from the real machine: the RAN# sequence, the self-tests, and the
hold-key displays. Those displays (f (i), PREFIX, MEM, matrix element names) are
shown briefly instead of for as long as the key is held.

## Updating

Edit, bump `CACHE` in `sw.js`, push. Without the version bump the phone keeps
serving the cached copy.
