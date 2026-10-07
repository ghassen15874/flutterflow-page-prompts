# Manual fallbacks (when a patch prompt fails once)

Exact menu labels can differ between FlutterFlow versions. If a label below is
not found, search the right-hand properties panel (it has a search box) or use
the command palette (Cmd/Ctrl + K).

## 0. Project setup, done once before any generation

1. Theme Settings: Primary = brand hex, Primary Background = page background,
   Secondary Background = card color, font = Poppins.
   Reason: the AI uses the project theme, and a purple default beat the hex in
   the prompt (attempt A).
2. Delete leftover failed pages and AI-made components.
3. In the generate dialog, confirm the mode says Page, not Component.

## 1. A reusable TextField (build once)

1. Add a TextField widget to any page.
2. Set: hint text, prefix icon, fill white, height 52, radius 12.
3. Enabled border and focused border: solid primary color, width 1.5.
4. Text style: Poppins 14, dark.
5. Right-click the widget and choose Save as Theme Style Widget. Name it
   app_textfield.
6. On other pages, drag it in (or copy and paste), then change hint, icon,
   and obscure-text for passwords.

## 2. A reusable Button (build once)

1. Add a Button widget. Fill primary color, white bold text, height 52,
   full width, radius 12, elevation 0, no shadow.
2. Save as Theme Style Widget. Name it app_button.
3. Outlined variant: white fill, 1.5px primary border, primary text. Save as
   app_button_outlined.

## 3. Bottom navigation bar

The nav bar is configured on the page itself (the Nav Bar Item properties
section in the right panel, and the app's navigation settings). Create the
items, set icons and labels, selected color = primary, unselected = dark/gray.
Typical client app: Home, Orders, Addresses, Profile.

## 4. Replace images

Upload your own images as assets or to Firebase Storage, then set them in the
Image widget properties. Never keep AI-chosen stock photos.

## 5. Copy rather than regenerate

After one form page looks right, copy its TextField rows and Button to the
other form pages instead of generating them again.

## 6. TextField hint text and icons (ignored by the generator, every attempt)

Select the TextField, then in the properties panel (use its search box):
Hint Text = "Email or username"; Prefix Icon = mail; for password also turn on
Obscure Text and add a visibility Suffix Icon. Label names vary by version.

## 7. On Tap actions for Containers

Select the Container, open the Actions tab (lightning icon) in the right
panel, add On Tap, then Navigate To or Backend Call. Containers support
actions like buttons do.

## 8. Social icon row by hand (if the patch fails)

1. Add a Row under the "Or continue with" row. Main axis: center.
2. Inside it add a Container: width 56, height 44, fill white, border 1.5
   primary, radius 12, alignment center.
3. Put an Icon widget inside (search the icon picker for "google"; then "apple"
   and "facebook" for the others). Size 24.
4. Copy and paste the Container twice, change the icons, add 12 spacing between.
