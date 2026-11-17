# Family Game Night Picker

A small Python app that helps a parent choose a game the whole family can play together on the family's Mac.

> A sample project for MIST 4600 (Computer Programming in Business) at UGA's Terry College of Business, Fall 2026.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/eunsol-cho-uga/family-game-night-picker/blob/main/family_game_night_picker.ipynb)

## Problem

A parent wants to buy one game for family game night. It has to be fine for kids, run on the family's Mac, and be something the family can play together, not just one person at a time. Steam has thousands of games, and the store page doesn't answer all three questions at once.

**My app helps a parent decide which game to buy for family game night by checking each game's age rating, whether it runs on the family's Mac, and whether the family can play it together.**

## What it does

The app answers three sub-questions with the data, then puts the answers together into a shortlist.

| # | Sub-question | How the app answers it |
|---|---|---|
| 1 | **Age:** how many well-known games are rated for all ages, and how do their reviews compare with age-rated games? | Groups every game by its minimum age, keeps games with at least 100,000 reviews, and compares the groups' positive reviews (pandas) |
| 2 | **Mac:** of the well-reviewed all-ages games, how many run on a Mac? | Keeps all-ages games with at least 90% positive reviews and counts how many run on a Mac (pandas) |
| 3 | **Together:** can a family play each shortlisted game together on one computer, only online, or only alone? | Sends each game's store description to Gemini and accepts only three answers: couch, online, or solo |

**Together:** the 5 most-reviewed all-ages Mac games with great reviews, each with how the family can play it, plus the ones that are best for game night. Saved to `game_night.csv`.

## How to run it

1. Click **Open in Colab** above, or open `family_game_night_picker.ipynb` from this repository in [Google Colab](https://colab.research.google.com).
2. Put `steam_games.csv` (in this repository) in your Google Drive, in the same folder as the notebook.
3. Get a free Gemini API key at [aistudio.google.com](https://aistudio.google.com) (use a personal Gmail account). In Colab, click the key icon on the left (Secrets), add a secret named `GOOGLE_API_KEY` with your key as its value, and turn on **Notebook access**.
4. Choose **Runtime → Run all**. Allow access to Google Drive when Colab asks. The last cell takes about 30 seconds.

Never type your Gemini key into the notebook: this repository is public.

## Example output

**Sub-question 1:** most well-known games are rated for all ages, and their reviews are just as good:

```
age_group
all ages     119
age-rated     50

age_group
age-rated    86.1
all ages     88.0
```

**Sub-question 2:** 40 of the 67 well-reviewed all-ages games run on a Mac (60%), compared with 65 of all 169 well-known games (38%).

**The shortlist:** the 5 most-reviewed well-reviewed all-ages games that run on a Mac:

| Game | Price | Positive reviews |
|---|---|---|
| Terraria | $9.99 | 97% |
| Garry's Mod | $5.99 | 96% |
| Stardew Valley | $14.99 | 98% |
| Euro Truck Simulator 2 | $19.99 | 97% |
| Unturned | free | 91% |

Each game is printed as a card with how the family can play it (from Gemini), followed by the ones that are best for game night. See the last cell of the notebook for the cards from the latest run.

**Recommendation for the parent:** buy one of the games on the "Best for game night" list. They are rated for all ages, well reviewed, run on a Mac, and the family can play them together on one computer.

## Data

`steam_games.csv`: the 1,000 Steam games with the most reviews, from the [Steam Games Dataset](https://www.kaggle.com/datasets/artermiloff/steam-games-dataset) on Kaggle (collected March 2025), shared under the MIT License. Titles with adult content were removed for class.

## Built with

- Python and [pandas](https://pandas.pydata.org/), in Google Colab
- [Google Gemini API](https://ai.google.dev/) through the `google-genai` library: labeling how each game is played

## AI Use Disclosure

- **I used AI tools:** Yes
- **Tools:** Claude
- **What I asked:** to draft the notebook's code and text cells from my question, sub-questions, and plan.
- **What I added, changed, or fixed in the AI's output:** chose the user, the decision, and the sub-questions; set the cutoffs (100,000 reviews, 90% positive); checked every result against the data.
- **What I designed and wrote entirely myself:** the project idea and the recommendation.
- **I understand every line of code I am submitting:** Yes

## Author

Eunsol Cho · MIST 4600, Fall 2026
