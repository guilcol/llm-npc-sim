# llm-npc-sim

A browser-based 3D sandbox where you talk to LLM-driven NPCs and ask them to do things. The LLM decides what an NPC tries. The world decides what happens.

**Status:** design stage. No code yet.

## Idea

- **Agnostic tools.** NPCs act only through generic verbs (move, grab, apply force, ingest, ...). There are no object-specific tools.
- **Agnostic prompts.** Prompts contain no game rules. The model's own common sense decides whether an NPC tries something.
- **Physics resolves outcomes.** The engine decides each outcome from parameters on the actor and the target. Failure is a valid outcome.
- **Outcomes become state.** Results change parameters and status. NPCs perceive the changes and react without scripted reactions.
- **Local perception.** An NPC knows only what it sees, hears, and remembers.
- **Event-driven.** The LLM is called on events, not every tick.

## How a request plays out

> Player: "Go to that fountain."

1. The engine resolves "that" to the fountain the player is looking at.
2. The LLM decides to comply and calls `move(fountain)`.
3. The engine finds a path and walks the NPC there. No LLM calls happen on the way.
4. Arrival is an event. The NPC wakes up and may respond.

## Platform

- Runs in the browser, 3D low-poly
- Bring your own LLM API key, stored locally. No backend.

## Docs

- [OVERVIEW.md](OVERVIEW.md): the project on one page
- [REQUIREMENTS.md](REQUIREMENTS.md): functional requirements

## License

To be decided.
