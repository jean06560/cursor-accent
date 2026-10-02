# Changelog

## 1.2.0 (2026-10-02)

- The pointer body now uses the theme's `foreground` instead of
  `dark_background`, which some themes don't define. The body then blended
  into the background; `foreground` contrasts with it by design. The outline
  still follows the theme's accent.
- The new color is drawn immediately. `hyprctl setcursor` reloads the theme
  but Hyprland keeps the old image until the pointer is hidden and shown
  again, so the color only changed after hovering another window. After
  `setcursor` the script now sends a virtual `F24` key press with `wtype`
  (hides the pointer through `cursor:hide_on_key_press`), then reissues the
  pointer position with `movecursor` (shows it again, forcing a redraw). If
  `wtype` is missing it is skipped.

## 1.1.0 (2026-09-22)

- The cursor is re-applied at every login. A post-boot hook joins the
  theme-set hook, because a cursor set with `hyprctl setcursor` lasts only
  for the running compositor and Omarchy sets no `HYPRCURSOR_THEME`, so a
  fresh boot could come up with whatever theme hyprcursor found first. The
  two hooks and the shell service take a lock so they cannot race on the
  shared build and install folders.
- The README documents the optional Style > Cursor menu picker with a
  screenshot, and its Remove section names the hook files that exist.

## 1.0.0 (2026-09-18)

- First listing. Recolors the system cursor to the active Omarchy theme's
  accent on every theme switch, using Hyprland's own `hyprcursor-util`,
  with a fixed-color or system-default option and a choice of pointer
  shape.
