# "Good Enough RAG and Other Projects

Something that's been filling a lot of time is looking at retrieval augmented generation (RAG). Large Language Models hallucinate a lot when using general knowledge, less if you tell it to RTFM (read the fine manual) you've just given it. RAG pipelines rely on big databases and vector (similarity) search to identify relevant context to give to the LLM.

The most common suggested solutions are a bit too heavy for personal desktop use. Vector databases require chopping up your data into little pieces and indexing it with text embeddings created by a language model. This is very expensive all around. Then you have to maintain the database and feed it new information. The whole process isn't very friendly for questions like, "Can you read these TTRPG rules and figure out if it has a momentum mechanic. Then explain it to me."

Also a lot of the tools for this are very new, underdocumented, or sometimes just don't work.

Which leads me to another idea. Since I'm not dealing with a massive knowledge base (I'm not _that_ much of a file hoarder) could tools like `grep`, `ripgrep`, and `pdf2txt` provide "good enough" context? For example, use `rg` to search for "TTRPG" in all markdown files in this digital garden, add a question, and pipe that to the command-line GPT interface `sgpt`:

```
> {rg --context 5 --no-heading --type md "TTRPG" ./docs; echo "\n\nQUERY: how do ttrpgs relate to RAG" } | sgpt

TTRPGs (Table Top Roleplaying Games) do not directly relate to RAG (Retrieval Augmented Generation). TTRPGs are a form of interactive storytelling where players assume the roles of characters in a fictional setting. On the other hand, RAG is a technique that combines retrieval-based methods with language generation models to improve the quality and relevance of generated text.

However, TTRPGs can benefit from RAG techniques in terms of generating story prompts or providing context for the game. Tools like Ironsworn and Be Like a Crow mentioned in the document use oracles, which are similar to retrieval-based methods, to generate story prompts or guide the narrative. These oracles use dice or playing cards to provide random elements that players can incorporate into their storytelling.

In the context of the document, the author is exploring the use of RAG techniques to enhance their TTRPG experience. They mention the challenges of using large language models for generating relevant context and suggest using tools like `grep`, `ripgrep`, and `pdf2txt` to provide "good enough" context for their TTRPG needs.
```

Not that bad. The `rg` retrieval process grabs this file and an earlier file I had forgotten about, and summarizes both. And the context is trimmed down to about 550 words. Working with these APIs also require keeping a local memory of the chat conversation. I used rust to create one version of the client, but I'm trying to decide if I want to stick with that or work with typescript.
