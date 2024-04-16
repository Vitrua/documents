# Basic Workflow

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/git/firemagic.jpg?raw=true" alt="wiz" width="300" height="300">
</div>

Once upon a time in the enchanted land of Vitrua, there lived a wizard named Wizzle. Wizzle was not your ordinary wizard; he was part of an order of fellow wizards and sorcerers who shared all their spells through a big cauldron. One day, Wizzle got an idea to upgrade the Fire spell, and he extracted a magical paper named `fire.spell` from the cauldron. 

```
git clone https://github.com/vitrua/spellbook
```

Inscribed on the paper was the spell to conjure flames - a simple yet powerful "Fire" spell. Wizzle was excited to make it even more powerful.

## The Spellcasting Ritual:

1. **Create a New Branch - Fireball**:

    * Wizzle opened his enchanted terminal and invoked the Git spell to create a new branch named "ball": 
    ```
    git branch ball
    ```
    * With a flick of his wand, he switched to the "fireball" branch: 
    ```
    git checkout ball
    ```

2. **Update the Spell - Fireball**:

    * Wizzle opened the magical `fire.spell` paper using his text-editor visualization spell.
    * He modified the incantation from `Fire` to `Fireball`, bringing the new spell to life.
    * Wizzle added the updated spell to the magical Git cauldron.
    ```
    git add fire.spell
    ```
    * With a wave of his hand, he committed the changes, letting the other wizards know what you can do with the new spell: 
    ```
    git commit -m "Cast Fireball spell"
    ```

3. **Merge the Fireball Magic:**

    * Satisfied with the powerful Fireball spell, Wizzle decided to merge it into the main spellbook. He switched back to the main branch: 
    ```
    git checkout main
    ```
    * He merged the Fireball magic into the main spellbook: 
    ```
    git merge fireball
    ```

**The Grand Finale:**

With a sense of accomplishment, Wizzle pushed the updated main spellbook to the magical cauldron: 
```
git push origin main
```
His fellow wizards and sorcerers, connected through the magical network, marveled at the newfound powers of the Fireball spell.

And so, in the land of Vitrua, Wizzle the Spellcaster continued to weave his magical Git commands, creating powerful spells and enchantments for the entire magical community.

## Magical Git Commands Summary:

- `git branch <branch_name>`: Create a new branch.
- `git checkout <branch_name>`: Switch to a branch.
- `sed -i 's/Fire/Fireball/' fire.spell`: Update spell text.
- `git add fire.spell`: Add changes to the staging area.
- `git commit -m "Commit message"`: Commit changes.
- `git merge <branch_name>`: Merge changes from another branch.
- `git push origin <branch_name>`: Push changes to a remote repository.

And so, the tale of Wizzle the Git Spellcaster goes down in the magical scrolls of Vitrua, inspiring wizards and developers alike to wield the power of Git for enchanting collaborative creations.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>