# Reflection

## 1. flex-direction: row vs column

`row` places items side by side horizontally. `column` stacks them vertically. On my site the navbar uses `row` so my name is on the left and the links are on the right. On mobile I switch it to `column` so the links stack under each other.

## 2. Relative units vs px

`px` is a fixed size that doesn't change no matter what screen you're on. If you use `rem` or `%` instead, the layout adjusts to the screen and also respects when someone has a larger font size set in their browser. I used `rem` for font sizes and padding so things scale properly on mobile instead of being stuck at desktop sizes.

## 3. AI Attribution

Prompt I used:
> follow instructions in the pdf and do the assignment [path to WD_HW2 (4).pdf]

The AI initially wrote the mobile nav CSS with `align-items: center` on `.nav-links`, which made each link only as wide as its text — small and hard to tap on a phone. I changed it to `width: 100%` with `display: block` on the links so they span the full width and are easy to tap.
