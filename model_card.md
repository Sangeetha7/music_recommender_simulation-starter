# 🎧 Model Card: Music Recommender Simulation

## 1. Model Name  

Give your model a short, descriptive name.  
Example: **VibeFinder 1.0**  

---

## 2. Intended Use  

Describe what your recommender is designed to do and who it is for. 

Prompts:  

- What kind of recommendations does it generate  
- What assumptions does it make about the user  
- Is this for real users or classroom exploration  

---

## 3. How the Model Works  

Explain your scoring approach in simple language.  

Prompts:  

- What features of each song are used (genre, energy, mood, etc.)  
- What user preferences are considered  
- How does the model turn those into a score  
- What changes did you make from the starter logic  

Avoid code here. Pretend you are explaining the idea to a friend who does not program.

---

## 4. Data  

Describe the dataset the model uses.  

Prompts:  

- How many songs are in the catalog  
- What genres or moods are represented  
- Did you add or remove data  
- Are there parts of musical taste missing in the dataset  

---

## 5. Strengths  

Where does your system seem to work well  

Prompts:  

- User types for which it gives reasonable results  
- Any patterns you think your scoring captures correctly  
- Cases where the recommendations matched your intuition  

---

## 6. Limitations and Bias 

Where the system struggles or behaves unfairly. 

- **Features it does not consider:** The recommender currently ignores several rich audio features available in the dataset like tempo, valence, and acousticness. It also lacks any understanding of lyrics, cultural context, or collaborative user behavior (like skip rates or replay history).
- **Genres or moods underrepresented:** The small 17-song catalog is heavily polarized towards extreme high-energy (pop/EDM/rock) or extreme low-energy (lofi/ambient/classical). This severely underserves users who prefer mid-range, moderate-energy music.
- **Overfitting and "Echo Chambers":** Because genre and mood are scored as exact string matches, the system traps users in a filter bubble. If a user asks for "lofi", they will only be recommended lofi songs, leaving zero room for serendipitous discovery of a mathematically similar jazz or acoustic track.
- **Unintentional user favoritism:** The system systematically favors users who happen to guess the exact text taxonomy of the database (e.g., typing "chill" instead of "relaxed" or "calm"). Additionally, the "energy gap" calculation uses a symmetrical absolute variance; for an intense workout playlist, the math treats a slightly slower song and a vastly faster song as equally "bad", whereas a human would strongly prefer the faster track.  

---

## 7. Evaluation  

How you checked whether the recommender behaved as expected. 

- **Profiles Tested:** I tested standard, harmonious user profiles like "High-Energy Pop", "Chill Lofi", and "Deep Intense Rock". I also tested "adversarial" edge-case profiles designed to trick the math, like "High-Energy Sad", "Zero-Energy EDM", and "Aggressive Lullaby".
- **What I looked for:** I analyzed the terminal output to see if the top 3-5 songs actually resonated with the requested vibe, and if the generated explanation text logically justified the score.
- **What Surprised Me:** I was surprised by how much a simple points-based system struggles with contradictions. Before tweaking the weights, someone asking for "Zero-Energy EDM" was given the loudest, most energetic club track just because it had the "EDM" label. After changing the math to favor energy over genre, they were given sad classical string music! It showed how hard it is to balance categorical labels against acoustic reality.
- **Simple Tests:** I verified the underlying logic by running `pytest` to ensure mathematical changes to the scoring formula were sound, and repeatedly ran the standard `main.py` simulation to visually inspect changes in the ranked outputs.

---

## 8. Future Work  

Ideas for how you would improve the model next.  

Prompts:  

- Additional features or preferences  
- Better ways to explain recommendations  
- Improving diversity among the top results  
- Handling more complex user tastes  

---

## 9. Personal Reflection  

A few sentences about your experience.  

Prompts:  

- What you learned about recommender systems  
- Something unexpected or interesting you discovered  
- How this changed the way you think about music recommendation apps  
