# Tarot Card Model

A comprehensive YAML library for modeling a tarot deck, featuring a robust type system. By default the card descriptions conform to those of the [Rider-Waite-Smith Tarot](https://en.wikipedia.org/wiki/Rider%E2%80%93Waite%E2%80%93Smith_tarot) deck, but these can be overridden.

This library is designed to be used as a git submodule in other projects, providing structured tarot card data that can be easily integrated into applications, websites, or other software projects.

## Installation and Usage

### Using as a Git Submodule

To add this repository as a git submodule to your project:

```bash
# Add the submodule to your project
git submodule add https://github.com/infomofo/tarot-model.git path/to/tarot-model

# Initialize and update the submodule
git submodule update --init --recursive

# Commit the submodule addition
git add .gitmodules path/to/tarot-model
git commit -m "Add tarot-model submodule"
```

### Updating to a Specific Version

To use a specific tagged version of this library:

```bash
# Navigate to the submodule directory
cd path/to/tarot-model

# Checkout a specific tag
git checkout v1.0.0

# Return to your project root and commit the version change
cd ../..
git add path/to/tarot-model
git commit -m "Update tarot-model to v1.0.0"
```

### Cloning a Project with Submodules

When cloning a project that uses this library as a submodule:

```bash
# Clone with submodules
git clone --recursive https://github.com/your-username/your-project.git

# Or if already cloned, initialize submodules
git submodule update --init --recursive
```

## Data Structure

This library contains the following data files:

- **`decks/rider-waite-smith/major-arcana/`** - 22 Major Arcana cards (0-21), each in its own YAML file
- **`decks/rider-waite-smith/minor-arcana/`** - 4 suit files, each containing 14 cards (Ace-King)
- **`suits/`** - Definitions for the four tarot suits (cups, pentacles, swords, wands)
- **`spreads.yml`** - Various tarot spread layouts and their meanings
- **`numerology.yml`** - Numerological associations for card numbers
- **`tags.yml`** - Comprehensive tagging system for card symbolism

### Card Structure

**Major Arcana cards** (individual files) contain:

```yaml
number: 1
name: The Magician
keywords:
  - manifestation
  - resourcefulness
meanings:
  upright: [array of meanings]
  reversed: [array of meanings]
visual_description: Objective description of the artwork
visual_description_analysis: Interpretation and symbolism
symbols: [array of symbolic elements]
```

**Minor Arcana suits** (4 files) contain an array of cards:

```yaml
cards:
  - name: Ace of Cups
    number: 1
    keywords: [array of keywords]
    meanings:
      upright: [array of meanings]
      reversed: [array of meanings]
    visual_description: Description of the artwork
    visual_description_analysis: Interpretation and symbolism
    symbols: [array of symbolic elements]
    significance: Role in the suit's journey
  # ... 13 more cards in the suit
```

### Example Usage

After adding as a submodule, you can access the data in your application:

```python
# Python example - Loading a Major Arcana card
import yaml

# Load a specific major arcana card
with open('path/to/tarot-model/decks/rider-waite-smith/major-arcana/01-the-magician.yml', 'r') as f:
    magician = yaml.safe_load(f)
    print(f"Card: {magician['name']}")
    print(f"Keywords: {', '.join(magician['keywords'])}")

# Load minor arcana cards from a suit
with open('path/to/tarot-model/decks/rider-waite-smith/minor-arcana/cups.yml', 'r') as f:
    cups_data = yaml.safe_load(f)
    for card in cups_data['cards']:
        if card['name'] == 'Ace of Cups':
            print(f"Minor Arcana: {card['name']}")
            print(f"Keywords: {', '.join(card['keywords'])}")
            break
```

```javascript
// Node.js example
const yaml = require('js-yaml');
const fs = require('fs');

// Load major arcana card
const majorCard = yaml.safeLoad(
  fs.readFileSync('path/to/tarot-model/decks/rider-waite-smith/major-arcana/01-the-magician.yml', 'utf8')
);
console.log(`Major Arcana: ${majorCard.name}`);

// Load minor arcana suit
const cupsData = yaml.safeLoad(
  fs.readFileSync('path/to/tarot-model/decks/rider-waite-smith/minor-arcana/cups.yml', 'utf8')
);
console.log(`Suit contains ${cupsData.cards.length} cards`);
```

## Versioning and Releases

This repository follows semantic versioning. To create and use versioned releases:

### For Maintainers

```bash
# Tag a new version
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# Create a GitHub release for better visibility
# (Use GitHub's web interface or gh CLI)
gh release create v1.0.0 --title "Version 1.0.0" --notes "Initial stable release"
```

### For Users

It's recommended to pin your submodule to specific tagged versions for stability:

```bash
# In your project that uses this submodule
cd path/to/tarot-model
git fetch --tags
git checkout v1.0.0
cd ../..
git add path/to/tarot-model
git commit -m "Pin tarot-model to v1.0.0"
```

## IMPORTANT DISCLAIMER

⚠️ **This library is for educational, entertainment, and software development purposes only.**

- Tarot card interpretations provided in this library are traditional meanings and should not be considered as professional advice
- Some interpretations included are the author's own and may vary from other sources or traditions  
- This software is not intended to provide medical, psychological, financial, or legal guidance
- Any decisions made based on tarot readings should not replace professional consultation
- The developers are not responsible for any decisions made using this library
- Card meanings and interpretations may vary among different traditions and practitioners
- Random number generation, even with biometric enhancement, cannot predict future events

Use responsibly and with an understanding that tarot is a tool for reflection and entertainment, not prediction or professional guidance.

## License

ISC

## Contributing

Contributions are welcome! Please feel free to submit pull requests to expand the card database, add new spread types, or improve functionality.
