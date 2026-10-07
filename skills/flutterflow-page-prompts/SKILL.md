---
name: flutterflow-page-prompts
description: Write FlutterFlow "Generate with AI" page prompts that render correctly, verify the result, and patch what the generator drops (TextFields, Buttons, navigation bars, header rows). Use this skill whenever the user wants a prompt for FlutterFlow, mentions FlutterFlow AI, Gen AI page, "1 prompt = 1 page", a mobile app screen to build in FlutterFlow, or shares a FlutterFlow screenshot where inputs, buttons or nav bars are missing, empty or blurry. Also use it when they show a UI image and ask for a prompt to recreate it in FlutterFlow, even if they do not say "skill" or "template".
---

# FlutterFlow page prompts

FlutterFlow's AI page generator draws static UI well (text, containers, cards,
lists) and often drops interactive widgets (TextField, Button, NavigationBar).
This skill produces prompts that give the best chance of a correct page, then
checks the result and patches it. It does not guarantee a perfect first
generation. What makes it dependable is the verify-and-patch loop.

Read `references/what-works.md` first when unsure: it holds the evidence
(observed vs hypothesis) from real attempts. Append new attempts to it.

## Workflow

1. **Setup (once per project)**
   Tell the user to set Theme Settings (primary, backgrounds, Poppins), delete
   failed pages and AI-made components, and confirm the generate mode says
   Page. See `references/manual-fallbacks.md` section 0. Every generation
   creates a NEW page (OneFlutterflowMobilePageN) and ignores the page name,
   so delete leftover copies and rename by hand.

2. **Write the prompt** using `references/master-prompt-template.md`. Start
   from the proven prompt in `references/known-good-prompts.md` when the page
   is similar, and change ONE thing per run.
   Hard rules:
   - Under about 2,000 characters, at most 12 numbered items.
   - One widget per item, named by type, with size and color inside the item.
   - First and last items are simple (Text or Container).
   - Only TextField is asked as an "actual" interactive widget (it renders).
   - EVERY button, including text buttons ("Continue with Google"), is a
     Container with a Row of Icon and Text. The Log In Container rendered 3 of
     3 times. Button widgets with text were missing or broken in every attempt.
     Container social buttons are still untested.
     Button widgets were dropped, blurred or flaky in every attempt.
   - TextField: visible solid primary border 1.5px, white fill, placed on the
     page background, not inside a white card. Hint text and prefix icons are
     ignored by the generator, so set them by hand.
   - No shadows, gradients or blur.
   - Photos: gray placeholder Containers in the first prompt. Image widgets
     with named subjects are a separate patch, last (they truncated a page).
   - Always include the no-components sentence and "Do not omit any item".
   - Write the prompt in English, in a code block, ready to paste.

3. **From a reference image**: list what is visible top to bottom, group into
   at most 12 items, simplify gradients, shadows and photos, then apply step 2.
   Tell the user the result will be approximate. Attach the image too.

4. **Open the Components tab first.** If components named Button, TextField
   or similar appeared, the missing widgets may be inside them. Drag them onto
   the page (see fix-prompts.md step 0). The no-components sentence is not
   reliable.
   Then **verify** after the user generates. Wait until generation has finished
   (no teal frame can mean still loading). A page that stops mid-prompt is a
   failed run: revert to the known-good prompt and patch. Ask for a screenshot and run the
   checklist below against the prompt's item list.

5. **Patch, do not regenerate.** Output varies run to run (an item present in
   one run was missing in the next), so regenerating is a coin flip. Fix each
   missing or wrong item with ONE short prompt from `references/fix-prompts.md`.
   Before patching a blank gap, tell the user to check the Widget Tree for an
   invisible element and delete it so nothing is duplicated.

6. **Fallback**: if a patch fails once, give manual steps from
   `references/manual-fallbacks.md` (hints, icons, On Tap actions, reusable
   Theme Style Widgets, nav bar, images).

7. **Log**: add a row to the attempts table in `references/what-works.md`.
   Move items between WORKS, FAILS and HYPOTHESIS as new evidence comes in.

## User preference: one full prompt, no patch steps

This user wants ONE complete prompt that contains every element, pasted once.
Default to that. Put every element in the prompt (all buttons as Containers,
icons, checkbox rows, photos), with a fallback sentence inside the prompt for
the photo. Offer at most one safe variant as a single swapped item (for
example the photo replaced by a Container with an Icon) in case the page
truncates. Mention patch prompts only if the user asks for them.

## Verification checklist

Compare the screenshot to the prompt item by item:

- [ ] First item present (header or logo)
- [ ] Every TextField visible as a bordered box, not a blank gap
- [ ] Primary action Container visible with a solid fill and a visible label
- [ ] TextField hint text and icons (expect missing, fix by hand)
- [ ] Page name (expect ignored, rename by hand, delete leftover copies)
- [ ] Icon-only button row present, with icons
- [ ] Lists show all sample items
- [ ] Last item present (page not cut off)
- [ ] Bottom nav bar present
- [ ] No unwanted components in the Components tab
- [ ] Colors match the theme; no stray purple
- [ ] Images are placeholders, not random photos

## Page order for a multi-role app

Build form pages (login, sign up, add/edit) last or by the manual-fallback
method; build list and card pages first because they generate reliably.

## Honest limits to tell the user

- Confirmed: TextField boxes render with an orange border (most runs, not
  all); a primary action built as a Container renders 3 of 3 times.
- Same prompt, two runs, two different pages (I-a, I-b). Keep the best page
  and finish it; do not regenerate for perfection.
- Not confirmed: Containers for social and secondary buttons, and every
  Switch, DropDown, TabBar and NavigationBar (never seen rendered yet).
- Hint text and icons in TextFields were ignored in every attempt.
- Generation is not deterministic, so no prompt guarantees all items. The
  verify-and-patch loop is what makes the result dependable.
- Menu labels in FlutterFlow change between versions; if one is missing,
  use the properties search box or Cmd/Ctrl + K.
