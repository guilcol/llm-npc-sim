# Edge Cases

> "Hey, check out that red fountain behind me. Walk towards it backwards."

- We aren't pointing at the fountain. It needs to be able to spot it even though it's behind us.
- How can it walk backwards towards something, while keeping the tools flexible and non-specific?

---

> "Follow me as we talk."

- How can it decide to walk with us, and at the same time hold a conversation?
- Does every inference cycle re-decide to follow us?
- Or does it pin us with a `follow` tool call that gets resent to the AI every inference in the form of "currently is following `<entity>`", and the AI can disengage at any point?
