# Master prompt template for FlutterFlow "Generate with AI" (Page mode)

Fill the placeholders in [BRACKETS]. Keep the finished prompt under about
2,000 characters and at most 12 numbered items. If the page needs more, split
it: generate the top half first, then add the rest with patch prompts
(see fix-prompts.md).

Rule of the skill, from attempts A to G:
- Only TextField is asked as an actual interactive widget (it renders).
- Every tappable thing is a Container: primary action (CONFIRMED to render),
  social icon buttons, secondary buttons (these two UNTESTED).
- Add On Tap actions and TextField hints by hand afterwards.

---

## The template

```
Generate one FlutterFlow mobile page: [PageName].
Use a Scaffold with a SafeArea and a vertically scrollable Column. Set the background to [BG_HEX], primary to [PRIMARY_HEX], dark text [DARK_HEX], gray text [GRAY_HEX], and use Poppins.
Create these actual widgets in this exact order:

1. [FIRST ITEM: a simple Text or Container, never an interactive widget]
2. ...
N. [LAST ITEM: a simple Row of Text, or a Container. Put tappable items before it]

Widget rules:
- Every TextField is an actual TextField widget: [H]px height, white fill, radius 12, a visible solid [PRIMARY_HEX] border 1.5px wide when enabled and when focused.
- The primary action is a tappable Container (NOT a Button widget): full width, [H]px height, solid [PRIMARY_HEX] fill, fully rounded, no shadow, containing a centered Row with bold white Text "[Label]" and an optional white arrow Icon.
- Icon-only buttons are tappable Containers: [W]px wide, [H]px high, white fill, 1.5px [PRIMARY_HEX] border, radius 12, each containing one centered Icon 24px.
- Cards: white Container, radius 16, 1px light gray border, no shadow.

Use [16 or 20]px horizontal page padding and 12 to 20px vertical spacing. Build everything inline on this single page: do not create any component, shared component, nested component or custom widget. Do not replace TextField widgets with Text widgets, and do not skip any Container. Use plain gray placeholder Containers for photos. Do not omit any item. Keep all [N] items. Fit a 393 x 852 screen.
```

---

## Writing rules for the numbered items

1. One widget per item, type named: Text, Container, Row, Column, ListView,
   Image, TextField. Sizes and colors go inside the item.
2. Say "actual" only before TextField.
3. Forms: label Text above (optional), then the TextField, stacked. Not in one Row.
4. Lists: say how many sample items and give their text.
5. No nesting deeper than two levels in one item. Split into two items.
6. Navigation bar: expect to set it up by hand (manual-fallbacks.md).
7. No shadows, gradients or blur.
7b. Photos: Image widget with the subject named in words, plus a gray Container
   fallback in the widget rules. Not behind overlaid text.
8. Hint text and TextField prefix icons are ignored by the generator. Do not
   count on them.
9. The page name is ignored. Rename by hand.

---

## Filled example

The proven baseline (9 of 11 items rendered) is in
`known-good-prompts.md`: "Burger Bros login, baseline v2". Copy its structure.
Do not use the v3 variant (Image widgets and Container icons in the first
prompt): it truncated the page after item 3.
