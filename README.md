# Nanopore interactive demos

Two interactive demos for the lecture on nanopores and single-molecule technologies for nanomedicine
(Department of Chemistry, Imperial College London).

Live address once published: https://ivanov-ic.github.io/nanopore-demos/

| File | What it is |
|---|---|
| `index.html` | The landing page. |
| `n1-1-pore-counter.html` | N1.1, the pore as a molecule counter. Proteins and 9.1 kbp DNA carriers, with a slow-motion view, a live record, and a long record. |
| `n1-2-event-statistics.html` | N1.2, how many events do you need. Counting statistics for healthy and patient samples. |
| `javascript-test.html` | A page that tests whether scripts run in the place a demo is opened. |
| `OFL.txt` | The licence of the embedded typefaces. |

Each demo is one self-contained file: no build step, no network request, fonts embedded. Open any of them
directly from disk to test.

## Publishing on GitHub Pages

1. In the repository `ivanov-ic.github.io`, copy this whole folder to the repository root, so that it sits
   beside `sli-demos/`:
   ```
   ivanov-ic.github.io/
     sli-demos/
     nanopore-demos/      <- this folder
   ```
2. Commit and push to the default branch. A user site rebuilds in a minute or two.
3. Open https://ivanov-ic.github.io/nanopore-demos/ and check the three addresses below. If a page is
   missing, wait for the Pages build to finish (Actions tab) and hard-refresh.

```
https://ivanov-ic.github.io/nanopore-demos/
https://ivanov-ic.github.io/nanopore-demos/n1-1-pore-counter.html
https://ivanov-ic.github.io/nanopore-demos/n1-2-event-statistics.html
```

Do not rename the demo files after you have printed QR codes or linked them from a slide deck or a course
page. Links in the index are relative, so the folder also works from any other host.

## Using them in teaching

- **In a lecture:** open the demo in a browser window next to the slides, press F11 for full screen, and use
  the keys 1, 2, and 3 in N1.1 to switch between the slow motion, the live record, and the long record.
- **In Canvas:** a file uploaded to Canvas has its scripts blocked, so embed the published page instead.
  In the HTML view of a page, add
  `<iframe src="https://ivanov-ic.github.io/nanopore-demos/n1-1-pore-counter.html" width="100%" height="2200" title="The pore as a molecule counter"></iframe>`
  The demos detect the frame and tighten their layout.
- **On slides:** see the notes that came with the deck. A hyperlink and a QR code on the slide is the most
  reliable way; a recorded video is the offline fallback.

## Checking after a change

- Open each page at 360 px and at 1920 px wide, in light and dark themes, and confirm there is no
  horizontal scroll.
- Open `javascript-test.html` from the published address and from inside the frame.
- Confirm that the browser makes no request outside `ivanov-ic.github.io` (the pages should make none).

## Licence

The demos are © 2026 Aleksandar P. Ivanov, licensed CC BY-NC-ND 4.0
(https://creativecommons.org/licenses/by-nc-nd/4.0/). The embedded typefaces are under the SIL Open Font
License 1.1 (`OFL.txt`).
