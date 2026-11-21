# Functional Requirements

Draft. Priority: **M** = first milestone, **L** = later.

## World

| ID | Requirement | P |
|---|---|---|
| W1 | The engine holds the authoritative state of every entity: position, orientation, parameters, and status. | M |
| W2 | The world runs real-time 3D physics: gravity, collisions, mass, and friction. | M |
| W3 | The world has at least one scene loaded from data, not code. | M |
| W4 | Entities can be created, destroyed, and transformed at runtime (broken, eaten, burned). | M |
| W5 | Time passes: parameters can change over time (cooling, spoiling, healing). | M |
| W6 | Environmental conditions (temperature, light, weather) are parameters that entities can read. | L |

## Parameters

| ID | Requirement | P |
|---|---|---|
| P1 | Every object has a common set of parameters (e.g. mass, size, hardness, temperature). | M |
| P2 | Objects can carry optional parameters that apply only to some objects (e.g. sharpness, flammability, spoilage). | M |
| P3 | Parameters are defined in data. Adding a parameter or object type needs no new tool. | M |
| P4 | NPCs carry physical attributes (e.g. strength, reach, speed) and status (e.g. health, fatigue, conditions). | M |
| P5 | A missing optional parameter means the property is absent, not an error. | M |

## Tools

| ID | Requirement | P |
|---|---|---|
| T1 | Tools are generic verbs that apply to any valid target. There are no object-specific tools. | M |
| T2 | The tool count isn't capped. A new tool must make sense on its own and work on any object. | M |
| T3 | A tool call is an attempt. The engine never rejects an attempt for being "unreasonable", only for being impossible to start (e.g. the target is out of reach). | M |
| T4 | A tool call returns no verdict. The action runs in the simulation until it settles or times out. Then the NPC wakes with fresh perception and works out what happened. | M |
| T4a | A call that can't start (unknown entity, malformed arguments) returns a plain error. That's an API error, not an outcome. | M |
| T5 | Long actions (walking, following) run in the engine without LLM involvement, and they can be interrupted. | M |
| T6 | NPCs can chain tool calls into a plan and cancel or replace it. | M |

## Resolution

| ID | Requirement | P |
|---|---|---|
| R1 | Outcomes come from actor and target parameters, never from the LLM. | M |
| R2 | Resolution is continuous, not pass/fail: a slight shift, a crack, a dent. | M |
| R2a | Effort is felt. Straining against something too heavy changes the actor's status (fatigue, pain), and the NPC perceives that as sensation. | M |
| R3 | Outcomes can change parameters and status on any entity involved, including the actor. | M |
| R4 | Effects can be delayed (e.g. sickness hours after ingesting something). | M |
| R5 | Resolution is deterministic given the same state and seed. | M |
| R6 | Resolution rules are data-driven and testable without an LLM. | M |
| R7 | Several actors can combine effort on one target (e.g. two NPCs lifting together). | L |

## Perception

| ID | Requirement | P |
|---|---|---|
| PE1 | Each NPC builds a local view from range, field of view, line of sight, and hearing. | M |
| PE2 | An NPC perceives only what its senses allow. Hidden parameters (e.g. internal spoilage) need a cue (smell, look) or experience. | M |
| PE3 | An NPC perceives its own status (pain, hunger, sickness) as sensation. | M |
| PE4 | The view is capped by salience so prompt size stays bounded. | M |
| PE6 | Perception reports raw state (positions, parameters), not computed deltas or interpretations. Before and after values come from the prompt history. | M |
| PE5 | Player references ("that", "him", "over there") resolve to entities using gaze, pointing, and proximity. | M |

## NPC cognition

| ID | Requirement | P |
|---|---|---|
| C1 | The LLM chooses whether and what to attempt, using its own common sense. The prompt contains no game rules. | M |
| C2 | Prompts are agnostic: identity, perception, memory, and the tool list only. | M |
| C3 | Each NPC has a persona (personality, values, relationships) that shapes willingness. | M |
| C4 | NPCs can refuse, negotiate, or partly comply. | M |
| C5 | NPCs react to outcomes and status changes without scripted reactions. | M |
| C6 | The LLM is called on events (speech, plan done or failed, notable perception change, status change), not every tick. | M |
| C7 | Idle NPCs run cheap scripted behavior with no LLM calls. | M |
| C8 | The architecture supports raising autonomy later (own goals, NPC-to-NPC talk) without a rewrite. | L |

## Memory

| ID | Requirement | P |
|---|---|---|
| ME1 | Each NPC keeps a log of what it perceived and did. | M |
| ME2 | Old events get compressed into summaries. | L |
| ME3 | NPCs keep relationships toward the player and other NPCs. | L |
| ME4 | NPCs learn from experience (e.g. avoid things that hurt them before). | L |
| ME5 | Memory persists across sessions. | L |
| ME6 | Each NPC can attach free-text notes to any entity (e.g. "a gift from the player"). Notes live in the NPC, not the object, so two NPCs can hold different notes on the same entity. | M |
| ME7 | Notes on an entity enter the prompt when the NPC perceives or holds that entity, and they persist after the entity is gone. | M |
| ME8 | The NPC writes and edits its own notes through a generic tool. | M |

## Conversation

| ID | Requirement | P |
|---|---|---|
| CV1 | The player can talk to NPCs in free text. | M |
| CV2 | Speech is spatial: only NPCs in hearing range receive it. | M |
| CV3 | NPCs answer in speech and emotes. | M |
| CV4 | Voice input and output. | L |

## Player

| ID | Requirement | P |
|---|---|---|
| PL1 | The player can point at or select entities to refer to them. | M |
| PL2 | The player uses the same tools as NPCs, resolved by the same engine. | L |

## Platform and LLM

| ID | Requirement | P |
|---|---|---|
| PF1 | Runs fully in the browser. No backend. | M |
| PF2 | The player brings their own API key. It is stored locally only. | M |
| PF3 | The LLM provider sits behind an adapter, so switching providers is a configuration change. | M |
| PF4 | The player can see and limit LLM usage and cost. | M |
| PF5 | Local model support. | L |

## Debug

| ID | Requirement | P |
|---|---|---|
| D1 | You can inspect any entity's parameters and status at runtime. | M |
| D2 | You can view each NPC's perception, prompt, tool calls, and outcomes. | M |
| D3 | World state can be saved and loaded for reproducing bugs. | L |
