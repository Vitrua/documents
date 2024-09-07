# Portable Java development environment

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/workflows/javaph.jpg?raw=true" alt="javaph" width="300" height="300">
</div>

## Objective
Learn how to create a portable Java development environment using Docker.

### Prerequisites
- **Docker**, installed and active

---

## The Tale of Jaya and the Enchanted Jar

In the mystical realm of Javara, there lived a brilliant sorceress named Jaya. Known for her exceptional mastery over magic, she sought to contain the power of her enchanted **Java Phoenix**, a majestic bird of fire that could solve the most intricate problems. However, like all magical creatures, the Phoenix's power was unpredictable, and it needed a special vessel to ensure its powers could be invoked anywhere in Javara—free from the distractions of dependency demons and configuration curses.

Jaya embarked on a quest to forge the perfect container—a portable jar that could harness the Phoenix’s power anywhere and anytime, allowing the magic of her Java programs to thrive in every corner of Javara.

---

## Containing the Java Phoenix

---

### 1. **Building the Enchanted Jar - The Project Directory**

Jaya’s first task was to create a sacred space to house her magical incantations and artifacts. She called this space the **Phoenix's Nest**, a directory for all her work. Jaya named it `java-phoenix-environment`.

```bash
mkdir java-phoenix-environment
cd java-phoenix-environment
```

In this nest, she carefully crafted four ancient scrolls:
1. `Dockerfile`
2. `Main.java`
3. `pom.xml`
4. `wisdom.txt`

Each scroll would play a crucial role in taming and summoning the Java Phoenix.

---

### 2. **The Dockerfile - The Summoning Ritual**

The first scroll Jaya inscribed was the **Dockerfile**, a summoning spell that would bring forth the Phoenix from its magical realm into a container. Without this, the Phoenix’s magic would be wild and unreliable.

Jaya’s Dockerfile was as follows:

```Dockerfile
# Summon the Phoenix from the sacred Oracle lands
FROM openjdk:24-slim

# Prepare the nest for the Phoenix
WORKDIR /app

# Copy all the enchanted scrolls into the nest
COPY . .

# Compile the Phoenix's spells
RUN javac Main.java

# Command the Phoenix to unleash its magic
CMD ["java", "Main"]
```

- **FROM openjdk:17-alpine**: Jaya summoned the latest and most stable version of the Java Phoenix, ensuring its powers were controlled.
- **WORKDIR /app**: Jaya created a special nest for the Phoenix to reside in.
- **COPY . .**: She copied all her scrolls into this sacred nest.
- **RUN javac Main.java**: With this spell, Jaya instructed the Phoenix to gather its strength by compiling the Java program.
- **CMD ["java", "Main"]**: Finally, Jaya commanded the Phoenix to perform its magic by running the `Main` class.

The next scroll Jaya inscribed was the spell that would tell the Phoenix what to do once it was summoned.

---

### 3. **The Core Spell - `Main.java`**

At the heart of Jaya’s enchantments lay the spell that would instruct the Java Phoenix to read from the **Scroll of Wisdom** and reveal its secrets. She carefully wrote the following code in `Main.java`:

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("wisdom.txt"))) {
            String line;
            System.out.println("Revealing the wisdom of the Phoenix:");
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Error reading the Scroll of Wisdom: " + e.getMessage());
        }
    }
}
```

- **FileReader("wisdom.txt")**: Jaya commanded the Phoenix to open the **Scroll of Wisdom**, a sacred text containing hidden knowledge.
- **BufferedReader**: She used a magic conduit to safely read the secrets line by line.
- **System.out.println**: Finally, Jaya instructed the Phoenix to reveal the ancient wisdom by printing it out for all to see.

But what knowledge was inscribed in this **Scroll of Wisdom**? That would be her next creation…

---

### 4. **The Scroll of Wisdom - `wisdom.txt`**

Jaya penned the **Scroll of Wisdom**—`wisdom.txt`—a simple yet profound artifact that contained the knowledge the Java Phoenix would reveal:

```text
Patience is the key to mastering fire.
Perseverance forges unbreakable code.
```

This scroll held valuable lessons about patience and perseverance, virtues necessary for any mage or coder dealing with the magic of Java.

---

### 5. **The Potion of Dependencies - `pom.xml`**

To ensure the Java Phoenix could always summon the necessary magical libraries, Jaya left behind the **Potion of Dependencies**, known as `pom.xml`. This scroll described the magical ingredients needed to summon the Phoenix’s power:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.javara.phoenix</groupId>
    <artifactId>java-phoenix</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>
</project>
```

This potion ensured that the Phoenix would always use the powers of Java version 17 and would summon any dependencies it might need.

---

### 6. **Forging the Container - The Trial of Fire**

With all her scrolls in place, Jaya made her way to the **Forge of Containers**. She whispered the incantation to summon the Docker container that would house her Java Phoenix:

```bash
docker build -t java-phoenix .
```

This spell would create the container from her Dockerfile, binding the Java Phoenix inside and preparing it to perform its magic.

---

### 7. **The Final Test - Unleashing the Phoenix**

Jaya’s last task was to command the Phoenix to perform its spell. She uttered the final incantation to run the container:

```bash
docker run --rm java-phoenix
```

The Phoenix sprang to life, its fiery wings glowing as it read from the Scroll of Wisdom and revealed the ancient knowledge:

```bash
Revealing the wisdom of the Phoenix:
Patience is the key to mastering fire.
Perseverance forges unbreakable code.
```

Jaya’s spell was a triumph! The Java Phoenix had revealed its wisdom flawlessly, executing the magical commands that Jaya had carefully inscribed.

---

### 8. **The Portable Magic of the Phoenix**

With her enchanted container, Jaya had not only tamed the Java Phoenix but had created a portable tool that could be used by anyone across the kingdom of Javara. Her fellow mages and coders could easily summon the Phoenix, run the spell, and learn the wisdom from the Scroll of Wisdom—no matter where they were.

Jaya’s container was portable, powerful, and immune to the chaos of dependencies and configuration.

---

## Docker Commands Summary:

- `docker build -t java-phoenix .`: Build the Docker image containing the Java Phoenix and its scrolls.
- `docker run --rm java-phoenix`: Command the Java Phoenix to perform its magic and reveal the wisdom of the Scroll of Wisdom.

---

### Project Directory

```markdown
java-phoenix-environment/
├── Dockerfile
├── Main.java
├── pom.xml
└── wisdom.txt
```

- **Dockerfile**: Defines the environment and commands needed to run the Java Phoenix.
- **Main.java**: The core Java spell.
- **pom.xml**: The Maven configuration, ensuring the correct Java version is used.
- **wisdom.txt**: A file with the ancient wisdom the Phoenix will reveal.

---

Thus, Jaya’s tale came to an end. Her Java Phoenix became a symbol of power and portability, and the mages of Javara followed in her footsteps, ensuring their code was always safe from the unpredictable forces beyond the container walls.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>