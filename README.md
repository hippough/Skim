# Skim

As humans, we skim text to see if it's worth reading more deeply. These skills let an agent do the same.

`checkpoint` has a model read each file once and write an extremely concise summary into `.index/`: what the file is generally about, and the exceptions if there are any. `skim` has the agent read the summaries before the files, and open a file when it seems relevant. It is similar to other ideas involving progressive disclosure.

The agent is more likely to open the files it needs and less likely to open the ones it doesn't. The savings can be small, but they add up over long chats.

## See it yourself

`demo/` is two unrelated Wikipedia articles and the `.index/` checkpoint wrote for them.

1. Move `demo/.index` aside. In a fresh session, ask: what is the oldest thing described in these articles, and how old is it?
2. Say "checkpoint".
3. In a fresh session, ask it again. Skim runs on its own now that the folder has an index, and ends with what it read and what it opened.
4. Compare.

Three runs on Sonnet achieved consistent results:

| | without index | with index |
| --- | --- | --- |
| articles opened | 2 | 1 |
| tokens | 72k | 68k |

The difference is the article it didn't open, about 3,500 tokens, which a session pays again on every turn after.

## Choices

- A summary says what a file is saying and what it's not. "Generally" is what it says, at the level of its sections. "Except" is what you'd expect from the name and won't find, and what you wouldn't expect and will. I thought this was the most concise way to put the information an agent needs to make a decision.
- The index is written when you say so, not every session. Often nothing has changed.

## Install

Claude Code: `/plugin marketplace add hippough/Skim`, then `/plugin install skim@skim`. Anywhere else, copy the two folders under `skills/` to where your agent reads skills.

The demo articles are from Wikipedia, CC BY-SA 4.0.
