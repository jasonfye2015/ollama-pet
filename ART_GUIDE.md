# Ollama Pet - Art Guide

Everything an artist (or an AI image generator) needs to make a new **image set** - the look of a pet.
There are two ways to supply one; both show up in the New Pet window automatically:

- **A sprite sheet (easiest):** one picture with all 37 poses, saved as `Images\<Name>.png` - for example
  `Images\Red Fox.png`. See section 0 below.
- **A folder of single pictures:** a folder next to `ollama_pet.py` named `Images - <Name>` with one PNG per pose
  (sections 1-3).

---

## 0. Sprite sheets

**Layout:** cards arranged in rows on a **white** background, each card a picture with its label in a light strip
underneath - **4 rows of 7 cards, then a row of 9** (37 cards). Cards are read left to right, top to bottom, so
the **order matters**; the exact size and spacing don't (the program finds the cards itself by looking for the
white gaps between them and the light label strips). Keep the white gaps clean and at least a few pixels wide.

**Save as:** a real PNG, any size (the included sheets are 1254 x 1254). The file name is the name shown for the
look ("Red Fox.png" -> "Red Fox").

**The 37 poses, in order:**

| # | Pose | # | Pose | # | Pose |
|---|---|---|---|---|---|
| 1 | Neutral | 14 | Angry | 27 | Bronze trophy |
| 2 | Amused | 15 | Defensive | 28 | Gold trophy |
| 3 | Laughing | 16 | Shocked | 29 | Rainy |
| 4 | Hungry | 17 | Confused | 30 | Snowy |
| 5 | Crying | 18 | Talking | 31 | Sunny |
| 6 | Sick | 19 | Thinking | 32 | Hot |
| 7 | Defeated | 20 | Yawning | 33 | Cold |
| 8 | Sleeping | 21 | Stretching | 34 | Birthday |
| 9 | Dead | 22 | Reading a letter | 35 | Halloween |
| 10 | On vacation | 23 | Writing a letter | 36 | Christmas |
| 11 | Playing | 24 | Roaming (backpack) | 37 | New Year |
| 12 | Being petted | 25 | Presenting a gift | | |
| 13 | Disgusted | 26 | Silver trophy | | |

**When the extra poses (18-37) appear:**

| Pose | When |
|---|---|
| Talking / Thinking | while the pet is replying / waiting for the AI to start |
| Yawning | when tired late at night |
| Stretching | when it wakes up |
| Reading a letter | when PetBook mail arrives |
| Writing a letter | while it writes a letter, a Wall post or its diary |
| Roaming | while in Free Roam |
| Presenting a gift | its daily gift (Good Friend and above), or sending a gift in a letter |
| Bronze / Silver / Gold trophy | when a trophy of that tier is earned |
| Rainy / Snowy / Hot / Cold / Sunny | its everyday look when the real weather matches (not while very happy) |
| Birthday / Halloween / Christmas / New Year | its everyday look on its weekly birthdays, Oct 25-31, Dec 24-26, and Dec 31 - Jan 1 |

Urgent states always win: if the pet is asleep, sick, hungry, tired or sad, you see that instead of an outfit.
Life-stage variants (`baby_` etc.) are for folder sets only.

The card positions are remembered in `Images\_layout_cache.json` after the first time a sheet is opened (you can
delete that file any time; it's rebuilt automatically).

---

## 1. Technical specs

| | |
|---|---|
| **File type** | PNG |
| **Size** | Square. **512 x 512** is ideal (256 x 256 minimum). Larger is fine - it's scaled down. |
| **Background** | Transparent if possible, otherwise plain white. No scenery. |
| **Framing** | Same character, **same size and same position in every image** (head in roughly the same spot). This keeps the pet from "jumping" when its mood changes - and makes future dress-up (hats, glasses) possible. |
| **Style** | Same art style, line weight, colours and lighting across the whole set. |
| **No text** | No words, speech bubbles or watermarks inside the images. |
| **File names** | Lowercase, exactly as listed below (e.g. `neutral.png`). |

**Where the images appear (and how big):**

| Place | Size shown | Which image |
|---|---|---|
| Main window | 200 x 200 | current mood or reaction |
| Mini mode | 110 x 110 | current mood or reaction |
| New Pet window tile | 100 x 100 | `amused.png` (or `neutral.png`) |
| Swap pet slots | 96 x 96 | `neutral.png` |
| Diary pages | 110 x 110 | the mood of that day |
| Casino ("watching you") | 64 x 64 | current mood |

Because some places are small, make sure the expression still reads clearly at **64 x 64**.

---

## 2. The images in a set

The app looks for each picture by a list of names, **first match wins**. Either name works - the current art uses
the *emotion* names (second column), but you can also supply the *mood* names (first column) to give each
situation its own picture.

### Moods (shown while the pet is in that state)

| Mood | File name(s) | When it shows | Art direction |
|---|---|---|---|
| Neutral | **`neutral.png`** *(required)* | Everyday mood (wellness 30-60). **Also used whenever another image is missing.** | Relaxed, friendly, looking at the viewer. The "default" portrait. |
| Content | `content.png` or `amused.png` | Wellness 60-80 | Small, pleased smile. Calm and happy. |
| Happy | `happy.png` or `laughing.png` | Wellness above 80 | Big smile or laugh, bright eyes. |
| Hungry | `hungry.png` | Hunger below 25 | Licking lips, looking at an empty bowl, or holding tummy. |
| Sad | `sad.png` or `crying.png` | Wellness below 30 | Teary eyes, droopy ears, slumped. |
| Sick | `sick.png` | Health below 30 | Pale, dizzy, thermometer or ice pack, half-closed eyes. |
| Tired | `tired.png` or `defeated.png` | Energy below 25 | Heavy eyelids, yawning, slouched. |
| Sleeping | `sleeping.png` | Asleep | Curled up, eyes closed, maybe "z". *If missing, a text face is shown instead (not neutral).* |
| Dead | `dead.png` | Health reached 0 | Gentle, not gory - angel halo, ghost, or peacefully lying down. *Text face if missing.* |
| Vacation | `vacation.png` *(optional)* | On vacation / at the pet hotel | Sunglasses, suitcase, beach towel. *Falls back to `sleeping.png`.* |

Mood priority (if several apply): dead > vacation > sleeping > sick > hungry > tired > sad > happy > content > neutral.

### Reactions (shown for about 3 seconds after something happens)

| Reaction | File name(s) | When it shows | Art direction |
|---|---|---|---|
| Eating | `eating.png` or `laughing.png` | Feed, Treat, treats from the Toy Box | Munching, crumbs, happy chewing. |
| Playing | `playing.png` | Play, toys, winning a minigame | Bouncing, pouncing, chasing a ball. |
| Loved | `loved.png` or `attracted.png` | Being petted | Blushing, hearts, leaning into a hand. |
| Disgusted | `disgusted.png` | Medicine, or overfed | Tongue out, "yuck" face, green tint. |
| Grumpy | `grumpy.png` or `angry.png` | Woken up too early | Frowning, puffed up, arms crossed. |
| Refusing | `refusing.png` or `defensive.png` | Won't go to bed / bored of a toy | Turned away, paws up, "no thanks". |
| Surprised | `surprised.png` or `shocked.png` | Level up (5 seconds) | Wide eyes, open mouth, sparkles. |
| Confused | `confused.png` | The AI had an error | Head tilt, question mark, puzzled. |

`sick.png`, `hungry.png` and `tired.png` are also briefly shown when the pet refuses to play for that reason.

### Minimum and complete sets

- **Minimum:** `neutral.png` alone works - everything else falls back to it (or a text face for sleeping/dead).
- **Recommended starter (6):** `neutral`, `happy`/`laughing`, `hungry`, `sick`, `sleeping`, `dead`.
- **Current full set (16):** neutral, amused, laughing, hungry, crying, sick, defeated, sleeping, dead, playing,
  attracted, disgusted, angry, defensive, shocked, confused.
- **Complete set (18 distinct pictures):** the 16 above, plus `vacation.png` and a separate `eating.png`
  (so eating no longer shares `laughing.png` with "happy").

---

## 3. Growing up: life-stage variants (already supported)

Put a life stage in front of any file name and it's used first while the pet is that age:

| Prefix | Age |
|---|---|
| `baby_` | first day |
| `child_` | from 1 day |
| `teenager_` | from 3 days |
| `adult_` | from 7 days |
| `elder_` | from 30 days |

Example: `baby_neutral.png`, `baby_sleeping.png`, `elder_neutral.png`. You don't need a full set per stage -
`baby_neutral.png` + `baby_sleeping.png` is enough to make a pet visibly "grow up"; any missing baby image uses the
normal one.

---

## 4. Making a consistent set with an AI image generator

1. **Make a character sheet first.** Generate one clear, front-facing neutral portrait you love. That image is your
   reference for everything else.
2. **Give that image back as a reference for every mood**, and ask for only the expression/pose to change.
3. **Keep the same prompt "frame"** and change one line each time.
4. **Check each result at small size** (64 x 64) - is the emotion still obvious?
5. **Remove backgrounds** if the tool didn't make them transparent, and crop every image to the same square.

**Prompt template** (fill in the brackets):

> Cute cartoon [species] character, [colours / markings], [art style, e.g. clean line art with soft cel shading],
> waist-up portrait, centered, facing the viewer, same character and proportions as the reference image,
> plain transparent background, no text. Expression: **[e.g. "yawning with heavy eyelids, very sleepy"]**.

**Consistency checklist:** same colours and markings · same outline thickness · same size in frame · head in the
same place · same lighting · nothing cut off at the edges.

**Licensing:** only use art you made, generated yourself, or have permission to share. Check the image tool's
terms for public use, and consider releasing your sets under a simple license (for example CC0 or CC BY) so others
can use them too.

---

## 5. Ideas for expanding (wish list)

These need small code changes before the app uses them - but if a set includes them, wiring them up is easy.
Suggested file names are given so sets made now will "just work" later.

### Everyday life
| File | Idea |
|---|---|
| `talking.png` | Mouth open - shown while the pet's reply is being written or read aloud (Voice). |
| `thinking.png` | Paw on chin - shown while the AI is thinking. |
| `yawning.png` | Late at night, before bed. |
| `morning.png` | Stretching - the first greeting of the day. |
| `bathing.png` | For a future "Clean" / cleanliness stat. |

### PetBook and Free Roam
| File | Idea |
|---|---|
| `reading_letter.png` | Holding a letter - when mail arrives. |
| `writing.png` | With a pencil - while writing a letter or Wall post. |
| `roaming.png` | Little backpack, out exploring - while in Free Roam. |
| `gift.png` | Holding out a present - the daily gift at Good Friend and above. |

### Casino and games
| File | Idea |
|---|---|
| `jackpot.png` | Showered in coins - big wins. |
| `worried.png` | Biting nails - losing streak or nearly broke. |
| `trophy.png` | Holding up a trophy - when one is earned. |

### Weather (the pet already knows the real weather)
| File | Idea |
|---|---|
| `rainy.png` | Umbrella or raincoat. |
| `snowy.png` | Scarf and mittens, snowflakes. |
| `sunny.png` | Sunglasses. |
| `hot.png` / `cold.png` | Fanning itself / shivering. |
| `stormy.png` | Hiding under a blanket. |

### Holidays and special days
| File | Idea |
|---|---|
| `birthday.png` | Party hat and cake (weekly birthdays). |
| `halloween.png` | Costume. |
| `christmas.png` | Santa hat. |
| `newyear.png` | Party horn and confetti. |

### Bond stages
| File | Idea |
|---|---|
| `shy.png` | Peeking from behind something - Stranger stage. |
| `adoring.png` | Heart eyes - Soulmate stage. |

### Dress-up (future)
Accessories drawn as **separate transparent PNGs on the same 512 x 512 canvas**, positioned for the head/neck in the
standard pose, so they can be layered on top of any mood picture:
`hat_party.png`, `hat_santa.png`, `glasses_round.png`, `bow_red.png`, `scarf_blue.png`, `collar_bell.png`.
This only works if every mood keeps the head in the same place - another reason to keep framing consistent.

### Animation (future)
Two or three frames per mood (`neutral_1.png`, `neutral_2.png` ...) for a gentle idle animation - blinking,
breathing, tail wag.
