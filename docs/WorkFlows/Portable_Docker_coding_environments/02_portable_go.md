# Portable Go development environment

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/workflows/ggopher.jpg?raw=true" alt="ggopher" width="300" height="300">
</div>

## Objective
Learn how to create a local, portable Go script development environment using Docker.
### Prerequisites

- **Docker**, installed and active

## The Quest of Goro and the Golden Gopher

In the distant lands of Gophoria, there lived a skilled engineer named Goro. Goro was known far and wide for his craftsmanship, but his greatest companion was the mythical **Golden Gopher**, a creature capable of solving the most complex puzzles and computations. However, much like the Python Serpent, the Gopher needed to be tamed and contained to ensure its magic was portable, efficient, and free from the wild influences of dependency dragons and configuration goblins.

Goro set out on a journey to build the perfect vessel to contain the Golden Gopher—a container that could be summoned anywhere, ensuring his magical Go scripts could be run flawlessly across all of Gophoria.

---

## Containing the Golden Gopher

---

### 1. **Forging the Chamber - The Project Directory**

Goro’s first task was to create a special chamber to house his spells and artifacts. This would be the **Gopher's Den**, a directory where the magic would unfold. Goro called it `go-gopher-environment`.

```bash
mkdir go-gopher-environment
cd go-gopher-environment
```

Inside this chamber, Goro crafted four scrolls:
1. `Dockerfile`
2. `main.go`
3. `go.mod`
4. `data.json`

Each of these scrolls would play a vital role in taming the Golden Gopher.

---

### 2. **The Dockerfile - The Summoning Spell**

The first scroll Goro penned was the **Dockerfile**, a summoning spell that would call forth the Golden Gopher into a contained realm. Without this, the Gopher’s magic would be scattered and unreliable.

Goro’s Dockerfile was as follows:

```Dockerfile
# Summon the Gopher from the mystical Go lands
FROM golang:alpine

# Create a chamber for the Gopher's magic
WORKDIR /app

# Copy all the sacred scrolls into the chamber
COPY . .

# Run the Go spell to build the magical artifact
RUN go build -o golden-gopher .

# Command the Gopher to perform its magic
CMD ["./golden-gopher"]
```

- **FROM golang:1.20**: Goro called upon the most stable and powerful breed of the Golden Gopher.
- **WORKDIR /app**: Goro crafted a chamber where the Golden Gopher would be housed.
- **COPY . .**: He copied all of his magical scrolls into the chamber.
- **RUN go build -o golden-gopher**: This command instructed the Gopher to use its powers and create an artifact called `golden-gopher`.
- **CMD ["./golden-gopher"]**: Finally, Goro commanded the Gopher to perform its magic by running the artifact.

The next scroll Goro wrote was the heart of the spell itself, the Go code that would instruct the Gopher what to do.

---

### 3. **The Core Spell - `main.go`**

At the core of Goro’s magic lay the spell that would instruct the Golden Gopher to read the **Scroll of Insights** and reveal hidden knowledge. He crafted the spell in `main.go`:

```go
package main

import (
	"encoding/json"
	"fmt"
	"os"
)

// The Gopher's Core Spell – reading the Scroll of Insights
func main() {
	// Open the sacred scroll
	file, err := os.Open("data.json")
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	defer file.Close()

	// Unveil the hidden knowledge within the scroll
	var secrets map[string]string
	if err := json.NewDecoder(file).Decode(&secrets); err != nil {
		fmt.Println("Error decoding:", err)
		return
	}

	// Reveal the secrets
	fmt.Println("Revealing the hidden wisdom:")
	for key, value := range secrets {
		fmt.Printf("%s: %s\n", key, value)
	}
}
```

- **os.Open("data.json")**: This command summoned the Scroll of Insights, containing ancient knowledge in the form of a JSON file.
- **json.NewDecoder(file).Decode(&secrets)**: Goro instructed the Golden Gopher to decode the scroll’s contents and store it in a map of secrets.
- **fmt.Println**: The final spell, revealing the hidden wisdom that Goro sought.

But what knowledge did this Scroll of Insights hold? Goro would need to create that next…

---

### 4. **The Scroll of Insights - `data.json`**

Goro penned the **Scroll of Insights**, `data.json`, containing the ancient wisdom that the Golden Gopher would uncover:

```json
{
    "wisdom": "The early Gopher digs deep tunnels.",
    "strength": "Persistence leads to mastery."
}
```

This scroll contained cryptic wisdom about the strength and persistence of the Golden Gopher. Only through Goro’s spell could this knowledge be revealed.

---

### 5. **The Enchantment Scroll - `go.mod`**

To ensure the Golden Gopher would always be able to summon the necessary libraries and modules, Goro left behind the **Enchantment Scroll**, known as `go.mod`. This scroll specified the magical dependencies needed for the Gopher's spell.

```go
module golden-gopher

go 1.23
```

This simple scroll declared the Gopher’s realm and its reliance on the powers of Go version 1.20.

---

### 6. **Building the Container - The First Trial**

With the scrolls complete, Goro approached the ancient **Forge of Containers**. He knew the incantation that would summon the Docker container, binding the Golden Gopher inside:

```bash
docker build -t golden-gopher .
```

This command summoned the container, built from Goro’s Dockerfile, and prepared it to house the Golden Gopher.

---

### 7. **The Final Challenge - Running the Spell**

Goro’s final task was to command the Golden Gopher to perform its magic. He chanted the incantation to run the spell:

```bash
docker run --rm golden-gopher
```

The earth trembled as the Gopher sprang to life, reading from the Scroll of Insights and revealing its hidden wisdom:

```bash
Revealing the hidden wisdom:
wisdom: The early Gopher digs deep tunnels.
strength: Persistence leads to mastery.
```

The spell was a success! The Golden Gopher had performed the magic flawlessly, uncovering the ancient wisdom and executing Goro’s command.

---

### 8. **The Portable Power of the Gopher**

With his portable container, Goro had not only tamed the Golden Gopher but had created a tool that could be used by anyone in the kingdom of Gophoria. His fellow engineers could easily summon the Gopher, run the spell, and reveal the secrets of the Scroll of Insights—no matter where they were.

Goro’s spell was portable, reliable, and immune to the wilds of configuration and dependency errors.

---

## Docker Commands Summary:

- `docker build -t golden-gopher .`: Build the Docker image containing the Golden Gopher and its scrolls.
- `docker run --rm golden-gopher`: Command the Golden Gopher to run the spell and reveal the Scroll of Insights.

### Project Directory

```markdown
go-gopher-environment/
├── Dockerfile
├── main.go
├── go.mod
└── data.json
```

- **Dockerfile**: Defines the environment and the commands needed to run the code.
- **main.go**: The core instructions.
- **go.mod**: The module declaration, ensuring the correct Go version is used.
- **data.json**: A file with data that your script will read from.

---

Thus, Goro’s tale came to an end, his Golden Gopher a symbol of power and portability. The engineers of Gophoria marveled at his creation and followed his methods, ensuring that their spells and Gophers were always safe from the chaos outside the container walls.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>