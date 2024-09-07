# Portable Python development environment

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/workflows/pythor.jpg?raw=true" alt="pythor" width="300" height="300">
</div>

## Objective
Learn how to easily create a local, portable Python script development environment using Docker.

### Prerequisites

- **Docker**, installed and eventually active

## The Tale of Pythor and the Python Serpent

In the ancient kingdom of Codoria, the young wizard Pythor dreamed of wielding the power of the Python Serpent—a mighty creature capable of interpreting and manipulating the sacred Scrolls of Knowledge (data). But the Serpent was wild, prone to errors and dependencies on the chaotic forces outside.

Pythor knew that to harness this beast, he would need the power of a **Container**—a vessel that could hold the Python Serpent and keep it safe, pure, and portable.

His quest began by creating the essential scrolls that would forge his portable Python environment…

---

## Taming the Python Serpent

---

### 1. **Preparing the Sacred Chamber - The Project Directory**

Pythor began by crafting a special chamber—a directory to hold all his magical scrolls. He named this sanctuary `py-snake-environment`, where he could safely perform his spells.

```bash
mkdir py-snake-environment
cd py-snake-environment
```

Within this chamber, he would craft four sacred scrolls:
1. `Dockerfile`
2. `py-script.py`
3. `requirements.txt`
4. `spellbook.json`

But these scrolls were not ordinary texts. Each one held a vital part of the spell to control the Python Serpent and overcome the obstacles that lay ahead.

---

### 2. **The Dockerfile - The Binding Spell**

The first scroll Pythor had to craft was the **Dockerfile**, a powerful binding spell that would summon and contain the Python Serpent inside a magical chamber. Without this spell, the Serpent would run wild, affected by the outside world.

Pythor crafted his Dockerfile as follows:

```Dockerfile
# Summon the Python Serpent from the ancient "slim-bullseye" lineage
FROM python:slim-bullseye

# Prepare a sacred chamber for the Serpent to work in
WORKDIR /magic

# Copy all the magical scrolls into the chamber
COPY . .

# Install any additional spells, if needed (none for now)
# RUN pip install -r requirements.txt

# Command the Serpent to cast the core spell
CMD ["python", "py-script.py"]
```

- **FROM python:slim-bullseye**: Pythor called upon a lightweight, ancient breed of the Python Serpent—slim, agile, and reliable.
- **WORKDIR /magic**: He defined a mystical chamber, `/magic`, where all the spells would be performed.
- **COPY . .**: Pythor gathered all his scrolls and placed them inside the chamber.
- **CMD ["python", "py-script.py"]**: Finally, he commanded the Python Serpent to perform the core spell, written in `py-script.py`.

But this was just the beginning. Pythor needed to write the core spell that would command the Serpent to reveal the ancient knowledge hidden in the **Scroll of Secrets**.

---

### 3. **The Core Spell - `py-script.py`**

The heart of Pythor’s quest lay in controlling the Python Serpent to read from the **Scroll of Secrets**. To do this, he penned a powerful spell in `py-script.py`.

```python
import json

# The Spell of Knowledge – commanding the Serpent to read from the Scroll of Secrets
if __name__ == "__main__":
    # Open the enchanted scroll and read its contents
    with open('spellbook.json', 'r') as scroll:
        secrets = json.load(scroll)

    # Reveal the sacred knowledge hidden within
    print("Ancient Secrets Revealed:")
    print(f"Spell Name: {secrets['spell_name']}")
    print(f"Spell Power: {secrets['spell_power']}")
```

- **import json**: Pythor summoned the **Artifact of Parsing**, a spell that allowed the Python Serpent to understand and interpret JSON scrolls.
- **with open('spellbook.json', 'r')**: This line commanded the Python Serpent to carefully unroll the **Scroll of Secrets** and absorb its contents.
- **print()**: The final flourish, where the Serpent would reveal the hidden knowledge of the scroll.

But what secrets did the Scroll of Secrets hold? For this, Pythor needed to craft another magical scroll…

---

### 4. **The Scroll of Secrets - `spellbook.json`**

Pythor created a sacred scroll, `spellbook.json`, a record of ancient knowledge that held information on powerful magic. The Python Serpent would be tasked with interpreting and revealing these secrets:

```json
{
    "spell_name": "Dragon's Flame",
    "spell_power": "Unleashes a firestorm upon all enemies."
}
```

This scroll described the legendary **Dragon’s Flame**, a spell of immense power. It was said that only those who could contain and control the Python Serpent could reveal such ancient secrets.

But Pythor was not yet finished. To complete his journey, he needed to ensure his environment could grow, should he need additional spells.

---

### 5. **The Spell Repository - `requirements.txt`**

Though Pythor’s current spell needed no additional artifacts, he left behind the **Repository of Spells**, known as `requirements.txt`. This scroll would allow him—or future adventurers—to call upon additional spells, should the need arise:

```text
# No additional spells are required for now, but here is where you can summon them:
# Example:
# requests
# pandas
```

This scroll was a placeholder for future magic. Whenever new spells or libraries needed to be summoned, they would be recorded here.

---

### 6. **Summoning the Container - The First Trial**

With all his scrolls prepared, Pythor approached the Summoning Circle, where he would bind the Python Serpent into a Docker container. He knew the incantation well:

```bash
docker build -t py-serpent .
```

This powerful command would forge the container, pulling the Python Serpent from the mystical ether and trapping it in a perfectly controlled environment.

---

### 7. **The Final Adversity - Running the Spell**

But building the container was only half the battle. The true test lay in commanding the Python Serpent to cast the spell from within its container. Pythor chanted the final command:

```bash
docker run --rm py-serpent
```

The ground trembled. For a moment, the air was still. Then, the Python Serpent, obedient and contained, revealed the secrets of the Scroll of Secrets:

```bash
Ancient Secrets Revealed:
Spell Name: Dragon's Flame
Spell Power: Unleashes a firestorm upon all enemies.
```

The spell had worked. The Python Serpent had read the Scroll of Secrets, revealing the legendary power of the Dragon’s Flame! Pythor had successfully contained the serpent, protected from the dependency demons and version conflicts that lurked in the wild.

---

### 8. **The Legacy - A Portable Magic**

Pythor had triumphed. With his Docker container, he could summon his environment anywhere in Codoria. He could share it with fellow wizards, who could build and run the Python Serpent in perfect isolation, no matter where they roamed.

His spell was now portable, repeatable, and immune to the wilds of Codoria. The Python Serpent, once wild and unpredictable, was now a loyal servant of Pythor’s magic.

---

## Docker Commands Summary:

- `docker build -t py-script .`: Build a new Docker image for your project.
- `docker run --rm py-script`: Run the Python script inside the container and remove it after.

   ```markdown
   py-snake-environment/
   ├── Dockerfile
   ├── py-script.py
   ├── requirements.txt
   └── spellbook.json
   ```

- **Dockerfile**: Defines the environment and the commands needed to run the Python script.
- **requirements.txt**: A list of additional Python packages, the dependencies that your script might need.
- **py-script.py**: The Python script that contains your logic.
- **data.json**: A file with data that your script will read from.

---

Thus, Pythor’s journey came to a victorious end. His tale spread across Codoria, inspiring future wizards to wield the power of the Python Serpent with Docker, ensuring their spells were safe, portable, and free from the chaos of the outside world.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>