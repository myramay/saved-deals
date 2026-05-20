# saved-deals

Take-home project for Scout --> single HTML file, no build step

## what it does

Displays a saved deals list with loading, populated, and empty states. Clicking a deal opens a modal where you can set a price-drop notification threshold. The input validates that your target is (a) a real number and (b) actually lower than the current price, otherwise it tells you why it's wrong, inline, before you submit.

## how it works

Everything lives in one `index.html` file (sorry I'm on my personal laptop today- I will get XCode set up for future projects) inline CSS, inline JS, no dependencies. The deal data is a plain JS array at the top of the script. On load, a CSS-only shimmer skeleton plays for 800ms (simulating a fetch), then `renderDeals()` builds the card list from the array. State is kept in two variables: `activeDeals` (the live working set) and `ORIGINAL_DEALS` (a frozen snapshot for the restore button). The modal is always in the DOM, shown/hidden via opacity and pointer-events so the CSS transition has something to animate from.

## one decision I'm proud of

Percent-off is computed from the price fields rather than stored as a separate value in the data. It's a small thing, but it means the badge and the prices can never drift out of sync. There's no way to end up with a card that says "40% off" next to prices that math out to 32%. I've seen that bug in real products and it always looks quite sloppy. Keeping derived values derived felt like the right thing to do, even at this scale.

## one thing I'd do differently

The notify input currently lives and dies with the modal. If you set a threshold, close it, and reopen, it's gone. With more time I'd persist thresholds per deal, probably just a plain JS object keyed by product name, nothing fancy, so the input remembers what you told it. Right now the feature works but doesn't feel sticky the way a real saved-deals screen would.

One other thing worth mentioning: I went with HTML/JS because I don't currently have Xcode set up on this machine, as I am using my personal laptop rather than a school-issued device/lab computer. I'm installing it on my personal laptop so I can work in SwiftUI going forward. I know that's the production stack and I'd rather meet you there next time.

## one thing I'd love feedback on

2 things actually, if that's okay.

First: I went back and forth on modal vs. full detail view. I landed on modal because it keeps the list in context and for a saved-deals screen, comparison-scanning feels like the main job. That said, I could see a slide-in panel or a dedicated screen making more sense if the detail view ever gets heavier, including price history, retailer info, that kind of thing. Curious whether that matches how you all thinks about it.

Second: design is honestly not my strongest suit. I kept the UI minimal on purpose, partly because the prompt said polish wasn't the point, but also because clean and simple is a safer bet for me than reaching for something decorative I can't fully pull off. For the visual layer I used Claude Code to help me make better UI choices than I would have landed on alone. The structure, logic, states, and comments are all mine, I just didn't want to pretend I have design instincts I'm still developing. I'd genuinely appreciate feedback on where things felt visually weak or where one small change would have gone a long way. Specific critique is way more useful to me than general encouragement.

## how to run it :)

Download `index.html`, open in browser
