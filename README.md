# AI learning log

Hi, I'm Karoliina. This is where I keep what I make, test and learn in AI.

I've always been curious about the world of AI and I started learning AI video making this summer when I also made my first 3D models. My background is project management and web analytics, so I like to test things properly and write down what I find.

**How I work:** I study with Claude, ChatGPT, random online sources and courses. With chatbots I ask them to explain the concepts, to make me guess the result before every test, and to explain why things happened. I run the tests, write down my guesses and judge the results myself. Each experiment says exactly who did what. The goal of most of my experiments is to learn.

---

## Creative work

**[Experiment 4 — One apartment, three AI models](experiment-04.md)**
I rebuilt my parents' apartment in 3D three times between July and November. Each time I used a newer AI model and I witnessed big improvements. Try [Round 1](https://claude.ai/artifact/G5kgYgDm56qwGTLdSSsH7w) and [Round 2](https://claude.ai/artifact/DgagVXnPVq53nVFKwBR2Qf) in your browser.

![The same living room in three rounds](images/E4_three-rounds_living-room.jpg)

---

## Interior rendering: from sketch to photo

I wanted to test and understand MyArchitectAI, then later rebuilt a similar process myself in ComfyUI. What I wanted to find out: can AI make my sketch look like a real photo and still keep the original plan/drawing accurate?

- **[Experiment 1 — MyArchitectAI](experiment-01.md):** floor edits on a photo of my living room and what can I get from a very basic sketch.
- **[Experiment 2 — ComfyUI basics](experiment-02.md):** my first time in ComfyUI, playing around with the prompt and the seed.
- **[Experiment 3 — ControlNet](experiment-03.md):** giving the model my sketch as an image and comparing different guides (canny and depth)

| My sketch | My best render so far (Experiment 3) |
| --- | --- |
| ![sketch](images/B_input_line-sketch.jpg) | ![depth + canny](images/D_combo_depth0.60_canny0.30.png) |

**What I found so far:**
1. **A style template makes it prettier but moves things.** In MyArchitectAI, about 74% of my sketch lines stayed in place without a style, and about 53% with one (measured by Claude).
2. **The prompt decides *what*, the seed decides *where*.** With a short and basic prompt, a new seed gives a completely different room.
3. **Two guides together work better than one.** (at least in my experiment) Canny kept my lines but looked fake, depth looked real but lost some details, accuracy suffered. Both together gave the best balance.
4. **One number is never enough.** My most accurate render looked the least real. I always look at the picture myself (critically) and try more than one seed.

<details>
<summary><b>How I measure geometry</b></summary>

I put my sketch lines on top of the render and count how many of them still have an edge nearby (within about 8 pixels, less than 1% of the image width). More lines kept = the AI moved less of my room.

- It only makes sense when the render is made *from* my sketch, so the camera stays the same.
- It's not perfect: a render that just paints my lines on top scores high, and wooden floor planks can match by accident. That's why I always look with my own eyes too.
- Changing only the seed moves the score by about 6 points, so smaller differences can be just random.

The script is [measure_geometry.py](measure_geometry.py). Claude wrote it with me, and I ran it myself in Google Colab to check that it gives the same numbers as in my logs.

</details>

---

## Tools I've used

Midjourney · Nano Banana · Promptwise · Higgsfield · Runway · MyArchitectAI · ComfyUI · Claude · Claude Code · ChatGPT · Codex · Google Colab

## Next

- Test MLSD, a ComfyUI guide that only follows straight lines and is made for architecture.
- Use a better input for rendering: a screenshot from a 3D model, like architects would give a renderer.
- Add Round 3 of the 3D apartment as an explorable model.
