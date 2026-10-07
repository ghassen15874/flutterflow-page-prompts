# FlutterFlow AI page generation: evidence log

Source: 5 real generation attempts on the FoodDi project (screenshots from the
user), plus FlutterFlow docs and GitHub issues. Status labels:

- OBSERVED = seen directly in a screenshot
- DOCS = stated in FlutterFlow documentation or site
- HYPOTHESIS = my interpretation, not confirmed. Re-test before relying on it.

Update this file after every new attempt. It is the memory of the skill.

---

## Attempts

| # | Prompt style | Result |
|---|---|---|
| A | Short vague prompt: "modern login page, orange, Poppins" | Primary color came out PURPLE. Logo, title, OR divider, Google/Apple buttons rendered. Email/Password inputs missing (blank gap). Login button missing. |
| B | Long prompt: "Generate ALL elements, do not omit any" | Labels rendered but no input boxes. Google/Apple had no icons. AI created extra components: InputGroup, TextField, SocialButton, NavItem, BottomNav, ClientHomeStyle. |
| C | Numbered widget list + long design-system line (shadows, borders) + white card | Card, logo, texts, links rendered. Inputs = blank gaps. Login button = blurry peach rectangle (looks like shadow only, no fill, no label). Google/Apple row missing, page cut off after "OR". No components created. |
| D | Tortilla home page, 8 numbered items | Rendered well: hero banner, horizontal category list, Popular Picks cards, rewards card, colors. Missing: top header row (logo, bell, profile), "Deliver to" card, "Order Now" button, "Join Now" button, bottom nav bar. Banner image = random giraffe photo overlapping text. Card images only half width. |
| E | User's own original numbered login prompt | User reported it as the good format (structure copied for all later prompts). Output not captured. |
| F | Burger Bros login, skill v1 prompt: 11 items, simple first and last item, widget-rules block, orange-bordered fields, no card | BEST SO FAR. All 11 slots present except one. Rendered: title, subtitle, welcome text, TWO visible orange-bordered white TextFields, 'forgot password?', divider row, THREE outlined social buttons with real icons and orange borders, two gray placeholder Containers, sign-up row. Missing: the solid 'Login' Button (gap between 'forgot password?' and the divider). TextFields had no hint text and no prefix icons. AI ignored the page name (created OneFlutterflowMobilePage3). No components created. |
| G | Burger Bros login, skill v2: same 11 items, but primary action asked as a tappable Container, no prefix icons asked | Rendered: title, subtitle, welcome text, TWO orange-bordered white TextFields (still no hint text), 'forgot password?', SOLID TERRACOTTA 'Login' pill with arrow (FIRST TIME a primary button rendered), divider row, two gray placeholders (no icons inside this time), sign-up row. Missing: the three outlined social Buttons (blank gap between divider and placeholders), although the same row rendered in attempt F. AI created OneFlutterflowMobilePage4, old copies 1 to 3 still present. |
| H | Burger Bros login v3: v2 plus three changes at once (social row as Containers with Icons, two Image widgets with photo descriptions, longer rules) | WORST RESULT. Only items 1 to 3 rendered (title, subtitle, welcome text). Nothing after, not even the TextFields. Page may have been mid-generation (no teal frame) or generation stopped early. Page 5 created, copies 1 to 4 still present. Cause unconfirmed, suspect the Image widgets. |
| I-a | Tortilla login (12 items, baseline rules, Log In Container, full-width outlined Google/Apple Buttons) run 1 -> page 7 | BEST PAGE SO FAR, 10 of 12 items. Rendered: title, tagline, Welcome Back, GOOD FOOD AWAITS!, description, TWO pill TextFields with orange border (empty, no hint, no icon), Remember me row (the AI added a real checkbox) with Forgot password? on the right, solid Log In Container with arrow, divider 'or', sign-up row with arrow. Missing: Google and Apple buttons. |
| I-b | SAME prompt, run 2 -> page 8 | Worse. Same texts, Log In Container, divider, sign-up row. Missing: BOTH TextFields, the Remember me row (Forgot password? left aligned alone), Google and Apple buttons. |
| I (side effect) | Project tree after the two runs | New COMPONENTS appeared (diamond icons): Button, TextField, TextField2, OneFlutterflowMobile, OneFlutterflowMobile2, despite the no-components sentence. Red error badge '2' in the top bar. Eight OneFlutterflowMobilePageN copies now exist. |

---

## What WORKS (OBSERVED)

- Text widgets with size, weight, color. Always rendered.
- Containers with fill, radius, border. Cards render reliably.
- Row/Column layouts, dividers, "OR" separators.
- Horizontal and vertical ListView with sample items (category chips, food cards).
- Badges / pills made from Container + Text.
- Icons inside Containers (logo tile).
- Hex colors for page background and accents, once the project theme matches.
- Numbered "exact order" lists with named widget types.
- The line "Do not create any component..." coincided with zero components created
  in attempts C and D. (Correlation only: HYPOTHESIS that it caused this.)

- (F) TextField with a visible solid 1.5px orange border and white fill, placed
  directly on the page background (no white card): the box RENDERS. First time
  inputs appeared at all.
- (F) Row of three outlined Buttons with icons only (Google, Apple, Facebook):
  RENDERS with icons and the orange border.
- (F) Gray placeholder Containers instead of photos: render, no random photos.
- (F) 11 items with a simple Text first and a simple Row last: nothing was cut
  off at the start or end. Supports the "short prompt, simple first and last
  item" rule.
- (F) Clickable "Sign up" Text inside a Row renders.

- (G) Primary action built as a tappable Container (solid fill, fully rounded,
  centered Row with bold Text and arrow Icon): RENDERS exactly as asked.
  CONFIRMED once. Containers have now rendered in every attempt.
- (G) TextField with orange border and white fill rendered again (2 of 2).

- (D) Image widgets inside food cards, when the dish is named in the item
  ("Chicken California Burrito", "Korean BBQ Chicken Bowl"): the AI chose
  relevant food photos. Naming the subject seems to work for small photos.
  (Photos still can be wrong, replace by hand if needed.)

- (H) Truncated generation is possible: the page stopped after the third item.
  Treat any result that ends mid-prompt as a failed run, not a style problem.

- (I) Log In tappable Container with arrow: rendered in BOTH runs. Now 3 of 3
  attempts (G, I-a, I-b). Treat as reliable.
- (I) Divider row with centered text, sign-up row with arrow Icon, large bold
  heading text, left-aligned description text: render in every run.
- (I-a) Remember me row rendered, with a real checkbox the AI added itself.

## What FAILS (OBSERVED)

- TextField: rendered as blank space or omitted, in attempts A, B, C.
- Solid-fill Button: omitted (A) or rendered as blurry shadow (C).
- Outlined Button row at the end of a page (Google/Apple): omitted in C.
- NavigationBar: omitted in D.
- Top-of-page header row with IconButtons: omitted in D.
- Icons inside outlined social buttons: omitted in B.
- Stock images for a hero banner with text on top: random unrelated photo (giraffe on a burrito banner, attempt D).
- Hex color in prompt does NOT override a project theme with purple primary (A).

- (F) Solid-fill primary "Login" Button with a text label: MISSING a third time
  (A missing, C blurry, F missing). Outlined buttons with icons render fine in
  the same prompt, so the failure is specific to the solid primary text button.
- (F) TextField hint text and prefix icons: NOT rendered (boxes are empty), even
  though the prompt asked for both.
- (F) Page name in the prompt is ignored. FlutterFlow names pages
  OneFlutterflowMobilePage, ...Page2, ...Page3. Rename by hand and delete the
  old ones.
- (F) Soft cream pill look from the reference image is not reproduced: social
  buttons come out as plain outlined rounded squares. Expect approximate styling.

- (G) Row of three outlined Buttons with icons: MISSING, although it rendered in
  attempt F from almost the same wording. So output is NOT deterministic.
- (G) TextField hint text missing again (F and G). Two of two. Treat as
  never generated.
- (G) Page name ignored again; each generation adds another leftover page.

- (I) Full-width outlined Buttons with a text label and logo (Continue with
  Google / Apple): missing in BOTH runs. Button widgets with text have now
  failed in every attempt: A (Login), C (Login blurry), F (Login), G (social),
  I-a and I-b (social). Only icon-only outlined Buttons rendered once (F).
- (I) Same prompt, two different pages (I-a vs I-b): the TextFields and the
  Remember me row appeared in one run and not in the other. Proof of
  non-determinism from identical input.
- (I) The no-components sentence did NOT prevent components this time. It
  coincided with zero components in C to H, and failed in I. Downgrade it from
  "seems to work" to "unreliable".

## Likely causes (HYPOTHESIS unless marked)

1. Interactive widgets (TextField, Button, NavigationBar) are the weak spot.
   Static widgets are strong. (Consistent across A to D.)
2. Items at the very start and very end of a long prompt get dropped. In C the
   page stopped after "OR". In D the header (item 1) and nav bar (last) were lost.
   Keep prompts short: <= 12 items, about 2,000 characters.
3. White input fill on a white card with a light border makes inputs invisible
   even if they exist. Always use a visible border (orange 1.5px) and put
   fields on the page background, not on a white card.
4. Shadows on buttons (soft orange shadow) can render as the whole button body.
   Use "no shadow, no elevation" on buttons.
5. Repeated label + field patterns encourage the AI to extract components
   (DOCS: nested components are generated as reusable pieces).
6. The Page/Component toggle can silently flip to Component after attaching a
   file (DOCS: FlutterFlow GitHub issues #6853, #6569). Check it before sending.
7. In FlutterFlow, the bottom navigation bar is a page-level property, not a
   normal widget, which may be why generation skips it. (HYPOTHESIS, unverified.)

8. The generator may drop the primary solid Button because it is treated like
   the app's theme-styled primary action. UNTESTED fix: build the primary
   button as a tappable Container (solid fill, radius, Row with Text and Icon),
   because Containers render reliably. Add the On Tap action by hand later.
   CONFIRMED in attempt G for the primary action: the Container version
   rendered, the Button version never did. Extension to social buttons and
   other tappable things is UNTESTED (next run).
9. Hint text and prefix icon are set in TextField properties that the generator
   may not populate. Set them by hand (2 clicks) or try a patch prompt.
10. Simple, plain wording per item (no extra adjectives, no shadows) plus a
    short widget-rules block improved completeness from attempt C to F.
    Consistent with the length hypothesis, still not proven.

11. Generation varies from run to run (outlined button row appeared in F, not
    in G, with near-identical prompts). Regenerating is a coin flip; patching
    one missing item is more reliable than regenerating the whole page.
    (Supported by F vs G, two data points.)
12. The generator seems to treat Button widgets as unreliable but Containers as
    reliable. Working rule: only TextField is requested as an actual
    interactive widget; every tappable thing is a Container.
    (Based on A to G, still a pattern not a proof.)

13. The components named Button, TextField and TextField2 match exactly the
    widget types that went missing from the page. The generator may build the
    TextFields and the outlined Buttons as components and fail to place them
    on the page. UNTESTED check: open the Components tab, open these
    components, and see whether the missing widgets are inside. If so, drag
    the components onto the page.
14. Components appear only in some runs (none in F, G, H). Run-to-run variation.

## DOCS facts

- FlutterFlow AI uses the project theme: colors and text styles go with the
  prompt, so output matches the existing app theme.
- Generated components can include nested components as separate reusable pieces.
- Theme widgets (Save as Theme Style Widget) let one styled TextField or Button
  be reused across pages.

---

## Decisions that follow from the evidence

1. Set the project theme BEFORE generating (primary #hex, background, Poppins).
2. Generate the layout with the AI. Do not trust it for TextFields, Buttons, NavBar.
3. Ask for them anyway, with the strictest wording, then VERIFY with the checklist.
4. Patch anything missing with ONE short follow-up prompt per widget.
5. If a widget is still missing after one patch, build it by hand once, save it
   as a Theme Style Widget, and paste it everywhere.
6. Bottom nav bar: set up by hand from the page's nav bar settings.
7. Images: always plan to replace them by hand.

8. Primary action button: ask for a tappable Container, not a Button widget
   (untested, try first on the next page). Keep outlined icon Buttons as Buttons.
9. Do not rely on hint text and prefix icons from the prompt. Fix by hand.
10. Rename pages by hand. Delete leftover OneFlutterflowMobilePage copies.
11. Keep the fields on the page background with an orange border. Do not put
    them inside a white card.

12. Every tappable element (primary action, social icons, secondary buttons) is
    asked as a Container with a Row or Icon. Add On Tap actions by hand.
13. Do not regenerate to fix one missing item. Patch it. Delete leftover
    OneFlutterflowMobilePage copies after each generation.
14. Hint text: never asked as a requirement. Set by hand.

15. Photos: do NOT put Image widgets with photo descriptions in the first
    prompt. Attempt H (which added them) truncated after item 3. Keep gray
    placeholder Containers, then try a photo patch last, alone. Undo if the
    page breaks. Name the subject in words (it worked inside Tortilla food cards).
16. Change ONE thing per run. Start from references/known-good-prompts.md.
    Attempt H changed three things at once and nothing could be learned.
17. Before judging a result, wait until generation finishes and click the canvas.
    A page with no teal frame may still be loading.

18. After EVERY generation open the Components tab. Look for new components
    named after missing widgets (Button, TextField). Check inside them and drag
    instances onto the page before writing any patch prompt.
19. When two runs of the same prompt differ, keep the better page (the more
    complete one) and delete the rest. Do not regenerate hoping for a perfect
    page; finish the best one by patching or by hand.
20. Every button with a text label (secondary, social) is built as a Container
    with a Row of Icon and Text. Request it that way from the start (Log In
    Container proved the idea 3 of 3). Container social buttons still untested.

## Log of new attempts (append below)

| Date | Page | What was asked | What rendered | What was missing | Fix used |
|---|---|---|---|---|---|
