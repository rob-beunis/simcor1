# DECORRELATOR – the decorrelation procedure of the ELL

Live demos accompanying the article:

> Beunis R. (2022). The electrosensory lateral line lobe (ELL) in mormyrid fish : a stepping stone to the understanding of the cerebellum ? (Part 1/2 : the ELL). Zenodo. https://doi.org/10.5281/zenodo.17602438

The electrosensory lateral line lobe (ELL) of electric fish removes from the signals it receives the disturbances that the fish generates itself: it extracts the component of the signal that is *not* correlated with the use of the electric organ. The program 'visualizes' this decorrelation procedure. A signal S3, the sum of a signal S1 that is the same at every iteration and a signal S2 that is different at every iteration, is fed 250 times to a decorrelation procedure. S4 emerges as the correlated component, S5 as the uncorrelated one; the projected outlines show how well S4 matches S1 and S5 matches S2, and the yellow histogram shows the 'fit' at every iteration. The demos start with a plain averaging formula and then add, step by step, the implementation requirements of a neural circuit: fixed percentages for potentiation (P) and depression (D), a variable input load, wrong addressing, the ELL with its broad spike (B) threshold, and the 'lifting' of the signal by non-associative potentiation or by added excitation.


## Live program

https://rob-beunis.github.io/simcor1/

It runs in any modern web browser, with nothing to install. Every demo of the article can be opened directly with its number, the number of the video ("demo-1-N") in the earlier versions of the article: for example

- Demo 5 – Basic simulation, SUM and AVG (Part 1, Fig. 1, p. 3):
  https://rob-beunis.github.io/simcor1/?demo=5
- Demo 27 – ELL simulation, na-P constant, BSa-D 2% (Part 1, Fig. 13, p. 32):
  https://rob-beunis.github.io/simcor1/?demo=27

The panel to the right of the demo lists all demos of the article (5–49), grouped by section of the article, with figure and page. Page numbers are those printed at the bottom of the pages of the article.

A demo starts at once. The first iteration is drawn in slow motion, at the speed of the original program; after it, the demo runs twice as fast as the original. The buttons "Interrupt" (then "Resume") and "Stop" at the top of the panel interrupt and stop the run; as in the original program, clicking and right-clicking the text box at the bottom left do the same. Every run takes a different random course (the random signal S2).

Optional additions to the address:

- `&speed=0.5` plays back at half speed. Values from 0.25 to 16 are accepted. At 1x the first iteration runs at the speed of the original in Visual FoxPro 9, the rest twice as fast. The speed can also be changed with the buttons below the panel, also while a demo is running.
- `&seed=123` gives a reproducible run.

Every button has an explanation (tooltip). With a mouse, rest the pointer on the button; on a tablet or phone, press and hold the button for about half a second.

The page counts anonymous visits and demo starts with GoatCounter (no cookies, no personal data).


## Contents of this repository

- `index.html`
  The web version (JavaScript, a single self-contained file). This is the live program.

- `python/decorrelator.py` (with `python/START_DECORRELATOR.bat`)
  The Python/Tkinter version. It requires Python 3 and Pillow (`pip install pillow`).
  Start it with `python decorrelator.py`, or with options: `--demo 27`, `--speed 0.5`, `--seed 123`, `--scale 1.5`.

- `vfp/decorrelator.prg`
  The original Visual FoxPro 9.0 program, with its comments translated into English. Start it with `DO decorrelator` (interactive mode, with the dashboard) or `DO decorrelator WITH "27"` (demo 27).

- `vfp/decorrelator_original_dutch_comments.prg`
  The same program with its original Dutch comments.

The figures and videos of the article were made with the DECORRELATOR form of the author's article reader, a larger Visual FoxPro program (`CEREBREADER.PRG`). The forms DECORRELATOR and DASHBOARD and their helper classes are copied unchanged into `decorrelator.prg`; only a short start-up part and a minimal base class (with the methods of the article reader these forms use, also unchanged) were added, so that it runs on its own.

The Python and web versions follow the VFP code procedure by procedure, with the same procedure names (DEMO, MEM, STEP, MAKE_S1, MAKE_S2, SUBTRACT, ONECYCLE, DRAWALLLINES, LBPCAPTION, ...), rules and parameters, and the same screen layout as the screenshots in the article. Every value that VFP stores in a table field is rounded the way VFP does it, and the line objects are drawn at the same whole pixels. They were checked against runs of the original in Visual FoxPro 9: with the same random numbers, all demos give identical results (all table values after the first, second, tenth and last iteration, the number of random numbers used, the positions of all line objects, and all texts on the screen). They differ from the original in a few deliberate ways:

- Random numbers: the random number generator differs from VFP's `RAND()`, so an individual VFP run cannot be reproduced exactly.
- Speed: 1x is the speed measured in VFP 9 for the first iteration, and twice that speed after it. The original waits for a key before it starts ("Press any key to continue..."); the demos here start at once.
- Parameters: the parameter table `MEM.DBF` is not kept between sessions; every demo starts from its demo values.
- Modes: the modes used in this article are translated: the basic simulation and the ELL simulation (MGC). The eye blink (EBR) modes of the form belong to other articles.
- Additions: a demo panel, Interrupt/Stop buttons and a playback speed control. The dashboard of the original (the form with all settings) is used internally, because the text of a demo is built from it, but it is not shown.
- The form has the size it had on the author's screen when the figures were made (632 x 542 pixels).


## Acknowledgement

The original program was written by the author in Visual FoxPro 9.0. The translations into Python and into the web version were made with the assistance of Claude (Anthropic), an AI assistant, under the direction of the author, and were checked against the original program.


## Author

Rob Beunis, independent researcher (retired clinical neuropsychiatrist), Antwerp, Belgium.
