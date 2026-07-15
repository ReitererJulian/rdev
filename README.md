
# rdev

## Description
**rdev** is my personal developer knowledge base — part learning wiki, part system documentation. It's split into two purposes: explaining concepts and tools I'm learning (Python, Java, Spring Boot, Docker, etc.), and documenting the real systems I run (Raspberry Pi Stack, home setup, e3ds).

[![Markdown](https://img.shields.io/badge/Format-Markdown-000000.svg)](https://www.markdownguide.org/)
[![Status](https://img.shields.io/badge/Status-Work%20in%20Progress-yellow.svg)]()

## Key Features
* **Learning Wiki:** Concept and tool notes, organized by topic (languages, frameworks, tools, concepts) — independent of any specific project.
* **System Documentation:** Real, running setups (Pi Stack, home network, e3ds hardware/software) documented separately, linking back to the wiki for underlying concepts.
* **Consistent Structure:** Clear separation between "what I'm learning" and "what I actually run", so notes don't get duplicated across projects.
* **Growing Over Time:** Continuously updated as I learn new tools and expand my home infrastructure.

## Structure Philosophy
* `wiki/` → **concepts & tools**, e.g. "how does Docker work", "what is a DTO" — written once, referenced everywhere.
* `systems/` → **concrete setups**, e.g. "how the Pi Stack is configured" — short, practical, links to `wiki/` for background instead of re-explaining concepts.

---

## Table of Contents
- [Structure](#structure)
- [Usage](#usage)
- [Contents Overview](#contents-overview)
- [Credits](#credits)

## Structure
```
rdev/
|
│   README.md
│
├───systems
│   │   README.md
│   │
│   ├───e3ds
│   │      README.md
|   |      sensor-setup.md
│   │      sensor.md
│   │
│   │
│   ├───home-setup
│   │       desk.md
│   │       README.md
│   │
│   └───pi-stack
│       │   README.md
│       │   setup.md
│       │
│       └───scripts
│               stats.md
│               stress.md
│
└───wiki
    │   README.md
    │
    ├───concepts
    │       dto.md
    │       README.md
    │       rest-api.md
    │
    ├───frameworks
    │       fast-api.md
    │       flutter.md
    │       README.md
    │       spring-boot.md
    │
    ├───languages
    │   │   README.md
    │   │
    │   ├───dart
    │   │       dart-basics.md
    │   │
    │   ├───java
    │   │       cmd-assert.md
    │   │       collections.md
    │   │       design-patterns-behavioral.md
    │   │       design-patterns-creational.md
    │   │       design-patterns-structural.md
    │   │       equals-hashcode-tostring.md
    │   │       iteration-interfaces.md
    │   │       maven.md
    │   │       oop-basics.md
    │   │       year-3.md
    │   │
    │   └───python
    │           async-vs-sync.md
    │           python-basics.md
    │
    ├───linux
    │       arch.md
    │       hyprland.md
    │       README.md
    │
    └───tools
            docker.md
            git.md
            kubernetes.md
            postgreSQL.md
            README.md
            uvicorn.md
```

## Usage
This repo isn't a runnable project — it's a documentation/notes repository. Browse `wiki/` for concept explanations, or `systems/` for how my actual infrastructure (Pi Stack, home network) is set up and configured.

## Contents Overview

**Wiki**
- **Languages** – Python, Java fundamentals and patterns
- **Frameworks** – FastAPI, Flutter, Spring Boot
- **Tools** – Docker, Kubernetes, Git, PostgreSQL, Uvicorn
- **Concepts** – REST APIs, DTOs

**Systems**
- **Pi Stack** – Raspberry Pi server setup, monitoring scripts, infrastructure notes
- **Home Setup** – Desk, room, and network layout
- **e3ds** – Hardware and sensor documentation

## Credits

**Author:**
- [Reiterer Julian](https://github.com/ReitererJulian)




