# Follow-up patch prompts

## Step 0, before any patch: look in the Components tab
If components named Button, TextField, TextField2 (or similar) appeared, open
each one. The missing widgets may be inside them. Drag the component onto the
page where the widget should be. Delete components that are empty.

Use after generation when the checklist shows something missing or wrong.
Send ONE patch at a time. Keep each under 400 characters. Replace [PRIMARY].

## Missing TextField
```
Under the Text "[Label]", add an actual TextField widget: 52px height, white fill, radius 12, visible solid [PRIMARY] border 1.5px wide (enabled and focused), hint "[hint]", prefix icon [icon]. Do not create a component.
```

## Missing primary action (use this first, instead of a Button widget)
```
At the [position], add a Container: full width, 52px height, solid [PRIMARY] fill, radius 12, no shadow, containing a centered Row with white bold 16px Text "[Label]" and a white arrow Icon. Do not create a component.
```
Then add the On Tap action by hand (navigate, submit, etc.).

## Missing Button
```
At the [position], add an actual Button widget "[Label]": full width, 52px height, solid [PRIMARY] fill, white bold 16px text, radius 12, no shadow, no elevation. Do not create a component.
```

## Missing full-width text buttons (Continue with Google / Apple)
```
Below the "or" divider row, add a Column with two Containers and a 12px gap. Each Container: full width, 52px height, white fill, 1.5px [PRIMARY] border, fully rounded, containing a centered Row with a 22px Icon and bold 16px dark Text. First: Google logo Icon and "Continue with Google". Second: Apple logo Icon and "Continue with Apple". Do not create a component.
```

## TextField has no hint or icon
Set by hand: select the TextField, then in properties set Hint Text and Prefix
Icon. (Patch prompts for these were not tested.)

## Missing icon-only or social buttons (use Containers)
First check the Widget Tree: if the blank gap already contains a Row, delete it.
```
Below the "Or continue with" row, add a centered Row with three Containers and a 12px gap. Each Container is 56px wide, 44px high, white fill, 1.5px [PRIMARY] border, radius 12, containing one centered Icon 24px: Google logo, Apple logo, Facebook logo. Do not create a component.
```

## Missing header row
```
At the very top of the page, add a Row with space between: on the left [title Text and subtitle Text in a Column]; on the right two actual circular IconButtons, 44px, white fill, light border: [icon 1] and [icon 2].
```

## Missing card
```
Add a white Container card, radius 16, 1px light gray border, 14px padding, [position], containing a Row: [content].
```

## Wrong or random image
```
Remove the image in [place]. Put a plain Container there instead, [W]px wide, light [PRIMARY] tint fill, radius 12.
```

## Image does not fill the card
```
In each [card name], make the Image full card width, [H]px high, fit cover, rounded top corners.
```

## Button looks blurry or has no fill
```
Select the Button "[Label]" and set: fill solid [PRIMARY], shadow none, elevation 0, text white bold. Keep size 52px height, full width.
```

## Inputs invisible
```
Set every TextField on this page to: white fill, border 1.5px solid [PRIMARY] for enabled and focused states, radius 12.
```

## Extra components were created
Do not prompt. Delete the unused components from the Components tab, then
re-check that the page still shows its content.
