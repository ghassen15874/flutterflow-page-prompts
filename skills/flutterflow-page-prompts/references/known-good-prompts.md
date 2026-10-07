# Known-good baseline prompts

Always start from the best proven prompt and change ONE thing per run.
Result column = what rendered, from the attempts table in what-works.md.

## Burger Bros login, baseline v2 (attempt G: 9 of 11 items rendered)

Rendered: texts, both TextFields (orange border, no hint), solid Login
Container, divider row, gray placeholders, sign-up row.
Missing: the three social outlined Buttons. Add them with a patch.

```
Generate one FlutterFlow mobile page: BurgerBrosLoginPage.
Use a Scaffold with a SafeArea and a vertically scrollable Column. Set the background to #F7EEDC, primary to #B5472A, dark text #5A1A14, gray text #8A7B72, and use Poppins.
Create these actual widgets in this exact order:

1. Text "BURGER BROS", 34px, extra bold, dark, centered.
2. Text "Smash Burgers & Fries", 13px, dark, centered.
3. Text "Welcome back! Craving Burgers?", 26px, bold, dark, centered.
4. Actual TextField, hint "Email or username".
5. Actual TextField, obscure text on, hint "Password".
6. Right-aligned Text "forgot password?", 13px, dark.
7. Tappable Container "Login" with a white arrow Icon (primary action).
8. Row with a divider, the Text "Or continue with" in dark 13px, and a divider.
9. Row of three actual outlined Buttons with icons only: Google, Apple, Facebook, each 56px wide and 44px high.
10. Row of two gray placeholder Containers, each 150px wide and 120px high, radius 16.
11. Centered Row with Text "Don't have an account?" and clickable Text "Sign up" in primary, bold.

Widget rules:
- Every TextField is an actual TextField widget: 52px height, white fill, radius 12, a visible solid #B5472A border 1.5px wide when enabled and when focused.
- The primary action is a tappable Container (NOT a Button widget): full width, 52px height, solid #B5472A fill, fully rounded, no shadow, containing a centered Row with bold white 16px Text "Login" and a white arrow Icon.
- Outlined Buttons are actual Button widgets: white fill, 1.5px #B5472A border, no shadow.

Use 20px horizontal page padding and 12 to 20px vertical spacing. Build everything inline on this single page: do not create any component, shared component, nested component or custom widget. Do not replace TextField or Button widgets with Text widgets, and do not skip the primary action Container. Do not omit any item. Keep all 11 items. Fit a 393 x 852 screen.
```

## Burger Bros login, v3 (attempt H): FAILED, do not reuse as a first prompt

Changes vs v2, all at once: social row as Containers with Icons, bottom row as
two Image widgets with photo descriptions, longer widget rules.
Result: only items 1 to 3 rendered, page empty after the welcome text.
Cause unconfirmed. Suspect: the Image widgets with photo descriptions.
Use these changes only as separate patches, one at a time.

## Tortilla login, full single prompt (candidate, UNTESTED)

All 11 elements in one prompt: burrito Image in the heading Row, two
TextFields, Remember me row with checkbox Container, Log In Container, divider,
Google and Apple as full-width Containers (Icon + Text), sign-up row with arrow.
Safe variant: swap item 3 so the Image becomes a Container with a food Icon.
Log the result in what-works.md after the next run.

## Tortilla home, full single prompt (candidate, UNTESTED)

8 items, all buttons as Containers (header icons, Order Now, plus buttons,
Join Now), hero banner as a Row (text column + Image, not image behind text),
bottom nav built inline as a Container with a Row of 5 items instead of the
NavigationBar widget (which was dropped in attempt D). Safe variant: swap the
hero Image for a Container with a food Icon. Log the result after the next run.

## Tortilla sign up, full single prompt (candidate, UNTESTED)

12 items. Role selector (Customer / Restaurant Staff) dropped on purpose: only
clients sign up in this app. Back arrow merged into the title row; Google and
Apple merged into one Column item; 5 separate TextFields with label + hint +
prefix icon; terms row with checkbox Container; Create Account Container;
burrito Image in the heading row. Risk: five identical TextFields may trigger
component extraction (TextField, TextField2 appeared earlier with two fields).
Safe variant: swap the heading-row Image for a Container with a food Icon.
Log the result after the next run.
