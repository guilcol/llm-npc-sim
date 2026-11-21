# Overview

A browser-based 3D sandbox with LLM-driven NPCs. No plot. Both a game and a reference architecture for grounded agents.

## Core idea

**The LLM decides what to try. The world decides what happens.**

- **Agnostic tools.** Generic verbs, such as moving, grabbing, applying force, and ingesting. There are no object-specific tools. The number of tools isn't capped. A tool belongs if it makes sense on its own and works on any object.
- **Agnostic prompting.** Prompts don't list rules or forbidden actions. The model's own common sense decides whether an attempt makes sense and whether the NPC is willing.
- **Physics resolves outcomes.** Every attempt goes to the engine, which resolves it from parameters on the actor and the target. Anything can be attempted, and failure is a valid outcome.
- **Concepts are inferred, not checked.** The engine tracks only physical facts. Ideas like "hidden", "gift", or "safe" exist only in what the NPC and player make of them. A clumsy attempt with generic tools beats an engine-checked feature.
- **Outcomes become state.** Results change parameters on objects and NPCs. NPCs perceive those changes and react on their own, without scripted reactions.

## Mechanics

- **Parameters.** Objects and NPCs carry properties. Some are common (mass, hardness, temperature). Others are optional and apply only to some objects (spoilage, sharpness, flammability).
- **Resolution.** The engine simulates each attempt from actor and target parameters. It never labels the result as success or failure. The NPC works out what happened from what it perceives afterwards.
- **Status.** NPCs carry state (health, fatigue, temperature, conditions) that outcomes change. The model sees this state as perception, not as instructions.
- **Local perception.** An NPC knows only what it sees, hears, or remembers. It never sees global world state.
- **Event-driven.** NPCs are mostly reactive. The LLM is called on events (speech, plan done, notable change), not every tick. The architecture should allow scaling up to autonomous NPCs later.

## Examples

- Asked to push a boulder, the NPC pushes and the boulder doesn't move. The NPC sees that and responds.
- Asked to break a window, the NPC throws a pinecone and the glass holds. A rock breaks it.
- An NPC drinks from a stagnant pond, later gets sick, and starts avoiding the pond.

## Platform

- Browser, 3D low-poly
- Bring your own LLM API key, no backend

## First milestone

One small scene where unusual requests resolve sensibly through the rules, with no special-case code.

## Non-goals

- Scripted plot or quests
- Per-verb or per-object tools
- Rules written into prompts
- Global world state in prompts
