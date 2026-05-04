# Case Study: Engineering for Low-Spec Environments
Privacy & NDA: Professional ethics first. Since my production code belongs to private partners and organizations, the repos stay private. This breakdown is about the architectural logic and how I solved technical debt in a real-world scenario.


## 🏗️ The ERP/POS Ecosystem (Resilience on Legacy Hardware)
The Goal: Build a rock-solid, high-performance system for environments where "modern" hardware is a luxury.

### 🔴 The Technical "B.O." (The Challenge)
I had to deploy a unified POS, ERP, and CRM on machines that were basically relics. We're talking about storefronts running Windows 7 on low-power processors with barely any RAM.

The Hardware Wall: I couldn't just throw resources at the problem. Every MB of RAM counted.

Bad Connections: The system had to handle network drops without losing transaction data or breaking the user's flow.

The Load: Running inventory management and CRM reporting on the same box as the checkout counter without lagging the whole OS.

### 🛠️ How I Built It (The Architecture)
Instead of following "trendy" microservices that would kill a low-spec machine, I went with an Optimized Monolith. This gave me total control over the request lifecycle:

MariaDB Tuning: I didn't just install a database; I tuned it for low-resource environments. By using composite indexing and table partitioning, I made sure a heavy CRM report wouldn't lock a sale at the register.

Lazy-Loading Everything: To keep the footprint small, I implemented a strict lazy-loading strategy at the app level. If the user isn't using a feature, the system isn't wasting memory on it.

Smart Queuing: I pushed non-essential tasks (like syncing logs) to background Queues. This keeps the main POS thread responsive so the clerk never sees a loading spinner during a sale.

Deployment Scripts: Since I couldn't rely on complex containers, I developed Shell Scripts to automate the setup. This ensured the PHP/Laravel environment was always configured for peak performance on that specific hardware.

### 💻 My Stack for the Job
Core: PHP (Laravel) using Service and Repository patterns to keep things clean and modular.

Database: MariaDB for relational integrity even when things get messy.

Infrastructure: Custom Shell Scripting for "bare metal" deployment in restricted environments.


## 🎮 Hybrid 2-in-1 Simulation Architecture (The Game as a Renderer)
The Goal: Decouple complex simulation logic from the game engine to create an unhackable, high-performance ecosystem where the web backend is the absolute authority.

### 🔴 The Technical "B.O." (The Challenge)
Standard real-time simulation servers are usually bloated with client-side scripts and insecure environment files that invite exploits. I needed to move away from this "legacy" mindset.

The Client is a Threat: I treated the game client as a hostile environment. If a simulation check or an economy calculation happens in the game thread, it can be manipulated.

Legacy Bloat: Boilerplate code from standard libraries (Ox, QBCore) was too heavy and decentralized. I had to strip them down and rebuild the foundation from scratch.

The Render vs. Logic Split: I needed a system where the game was just a visual output, while the actual "existence" of the player's data lived in a high-performance web environment.

### 🛠️ How I Built It (The Architecture)
I engineered a hybrid system where the game server and a web-based core act as a single unit. The game became a visual renderer for the logic running in a PHP/Laravel ecosystem.

Server-Side Authority (PHP/Laravel): All economy simulations, inventory checks, and business logic were moved out of the game scripts and into a Laravel backend. This ensured that no action could be taken in the game without a "Go" from the PHP core.

The Game as a Visual Layer: I restructured the Ox Library and QBCore base to act as simple messengers. The game engine was no longer responsible for "thinking"—it only rendered what the backend commanded it to show.

Modern UI/UX with React Canvas: For the web-facing parts of the ecosystem, I used React + Canvas to build a high-fidelity interface, while the in-game menus and UI were built using React to replace standard, clunky interfaces.

Admin Mastery with Filament: I implemented a centralized management hub using Laravel Filament, allowing for real-time monitoring and manipulation of the simulation without ever needing to log into the game.

Hardened API Security (Laravel Sanctum): Implemented a hardened security layer using Laravel Sanctum to bridge the gap between the visual renderer and the backend "brain." This ensured that every single request originating from the game client or the web interface was fully authenticated and traceable. It effectively neutralized attempts by players or external scripts to forge economic transactions, as no action could be executed without a valid, server-verified token.

### 💻 My Stack for the Job
The Brain (Backend): PHP (Laravel), Laravel Sanctum (Hardened API Security), Filament (Admin & Management), and MariaDB.

The Interface (Web/NUI): React with Canvas for complex rendering and Tailwind CSS for styling.

The Visuals (Game): Lua for low-level game hooks and React for the Native User Interface (NUI).

The Core: A completely gutted and restructured version of the simulation base, stripped of legacy noise.


## 🏆 Award-Winning Cross-Platform MVP (Techstars 2nd Place)

The Goal: Build, validate, and ship a high-concurrency mobile, web, and backend ecosystem within a strict 54-hour limit for a global entrepreneurship competition.



### 🔴 The Technical Challenge

In a high-pressure environment, I chose a high-performance stack to ensure the product was production-ready from the first commit. The challenge was managing real-time data and cross-platform consistency with zero room for error.



The 54-Hour Grind: I had to move from a blank screen to a functional, incubated-ready product in a single weekend. No sleep, just code and coffee.

Performance First: I needed a backend that could handle concurrent user spikes without breaking a sweat and a frontend that didn't look like a "web-wrapper."

Rapid Iteration: I had to implement complex navigation and global state management while features were still being defined by the team.

🛠️ How I Built It (The Architecture)

I skipped the "slow and easy" route and went with a high-performance backend and a unified cross-platform strategy:



High-Concurrency Backend (Go): I chose Go (Golang) for the core API. Its efficiency with goroutines allowed me to build a lightweight, lightning-fast backend that handled heavy loads with almost zero resource consumption.

Cross-Platform Mobility (React Native & Expo): To hit Android, iOS, and Web simultaneously without tripling the workload, I used React Native with Expo. This gave me a single codebase for all platforms, allowing for immediate deployment and testing with real users during the event.

Modern Routing & Navigation (React Router v6): I implemented React Router v6 logic to manage complex user flows. This ensured the navigation felt solid and predictable—making the MVP feel like a polished, long-term project rather than a weekend prototype.

The Result: This technical execution—combining the speed of Go with the reach of Expo—secured 2nd Place at the Techstars Startup Weekend (2026) and earned the project a spot in a professional business incubator.

### 💻 My Stack for the Job

Backend: Go (Golang) for high-performance API services.

Frontend: React Native & Expo (Android, iOS, and Web).

Navigation: React Router v6.

Infrastructure: Cloud-native architecture designed for rapid scaling and instant incubation.

