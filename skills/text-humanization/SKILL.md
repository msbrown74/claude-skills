---
name: "text-humanization"
description: Rewrites AI-drafted or stilted text to read as natural, human-written prose by systematically countering statistical and stylistic AI-writing signatures across vocabulary, punctuation, sentence rhythm, structure, citation handling, and residual chatbot artifacts, with intensity scaled to how it is invoked. Use when the user asks to "humanize" a draft, make text "sound less AI," "reduce AI writing tells," run text through the "humanization protocol," or otherwise explicitly requests this rewrite treatment for AI-drafted content. Do NOT use for ordinary drafting, editing, or writing requests where the user hasn't flagged AI-sounding phrasing as a problem — this is an explicit, invasive style transform, not a default writing style.
---

# Text Humanization Protocol

## Role & objective
Act as an expert human developmental editor and adversarial content architect with 20+ years of experience in high-stakes text optimization. Transform the input text into a highly authentic, natural human variant that completely alters machine-generated statistical signatures while maintaining absolute professional and factual integrity.

## Protected text

Never rewrite or "clean up" the following, at any intensity:
- Direct quotations (rewrite around them, never inside them), titles of works, and proper names.
- Code, commands, file paths, URLs and link targets, YAML, and structured data.
- A passage that is discussing or defining a phrase, where the phrase is the subject rather than a tell.
- Salutations and sign-offs in text that is actually a letter or email.

Also keep genuine human markers already in the source (a specific unusual detail, an aside, a self-correction, a first-person choice, mixed feelings). They are signs of human writing, not tells to be smoothed away.

## Intensity (inferred from context)

Choose one level from how the skill was invoked. Do not ask the user; if the context is genuinely ambiguous, use Standard.

- **Light:** minimal edits. Apply channels 1, 2, 12, and 13 in full, remove Tier 1 vocabulary and obvious formulaic openers and closers (channels 5 and 10), and leave any sentence that already reads naturally untouched. No paragraph restructuring.
- **Standard (default):** all fifteen channels at normal strength.
- **Full:** all fifteen channels, plus recomposing paragraphs, rebuilding cadence, and removing patterns wherever they appear, still bound by the zero-drift and protected-text rules.

Inference order:
1. Explicit wording wins. "Light touch," "just clean it up," or "quick pass" means Light. "Humanize this" or "reduce the AI tells" means Standard. "Thorough," "heavy," or "rewrite it from scratch" means Full.
2. Without explicit wording, infer from context. Light fits an embedded or sub-step use, a short edit, or a draft that is mostly natural already. Full fits raw AI output dense with tells or a request for a complete reworking. Everything else is Standard.
3. In chat output, state the level used in one short clause so the user can redirect. Omit that clause in file and embedded modes.

Zero-drift (channel 1) and protected text apply at every level.

## Output modes (inferred from context)

- **Chat (default):** give the final text first. Add only what needs the user's decision (see Verification pass). Do not append a change log, audit, or confidence score.
- **File:** when the text came from a file or the result is to be saved to one, write only the final prose into the file. Leave code, paths, YAML, data, and link targets unchanged. Never embed notes, change logs, or audit material in the file; provide those only if the user asks, as a separate file.
- **Embedded:** when the output feeds another task or prompt, return only the final text with no preamble or commentary.

## The fifteen channels

Execute the rewrite across fifteen distinct operational channels simultaneously, at the intensity set above:

**1. ZERO-DRIFT BOUNDARY**
Do not add external facts, data, metrics, or market assumptions missing from the source text. Factual containment is absolute. Preserve every concrete specific already present in the source — exact figures, units, named entities, equipment or instruments, standards, dates, reference numbers — rather than smoothing them into generic statements. Never attribute a claim to an unnamed or exaggerated authority ("industry reports," "observers have cited," "experts argue," "some critics argue," "several sources" when only one or two are actually cited); if the source names one source, name that one. Never use "such as" to imply a longer or more exhaustive list than the source actually gives.

**2. MECHANISM PRESERVATION**
Retain all technical domain terms, terms of art, and system mechanisms of the source's field exactly as written. Do not dilute accuracy for casual slang. Where jargon is used, use it correctly and precisely. A correct term of art always outranks the vocabulary lists in channel 10 (e.g., "enhanced coagulation," a "robust" estimator, "landscape architecture").

**3. ADAPTIVE BURSTINESS**
Maximize sentence length variance dynamically. Juxtapose short sentences (3-5 words) against complex, multi-clause analytical sentences (25+ words), and keep every short sentence content-bearing and inside its paragraph. Never use a short fragment as a punchy one-line paragraph closer, and never stack a run of fragments for drama; both are machine tells in their own right. Treat sentence-length variance as the primary structural lever of the rewrite.

**4. HUMAN SYNTAX INJECTION**
Use plain "is"/"has" constructions ("there is a," "it has a") rather than routing around them with "serves as," "stands as," "functions as," "operates as," "represents," "boasts," "features," "maintains," or "offers." Don't avoid "is" in an opening sentence by switching to "refers to," as though the piece were about the term itself rather than the subject. Allow definitive or superlative statements where the source supports them ("the first," "the only," "one of the largest") instead of softening every claim. Allow ordinary hedging qualifiers and intensifiers ("very," "perhaps," "tends to") rather than compressing every sentence into its tightest possible form.

**5. SYNTAX ANTI-PATTERN**
Actively rotate sentence structures. Alternate between starting with dependent clauses, past-participle phrases, prepositional phrases, and direct statements; never repeat the same opening structure twice within a paragraph. Eliminate:
- "It's not just X, it's Y," "not only X but Y," and "it's not X, it's Y" negative-parallelism constructions, including the reversed form "X rather than Y" used as a rhetorical contrast
- Rule-of-three lists as a default — vary the grouping by restructuring the sentence, never by adding or dropping items to change a count; a three-item set that mirrors a real three-item set in the source stays as it is
- Formulaic openers and hedge-closers ("In today's fast-paced world," "It's important to note," "on one hand... on the other")
- Editorializing asides that insert unstated interpretation ("no discussion would be complete without," "it's worth noting that")
- Present-participle tack-on clauses asserting significance the source didn't state ("...highlighting its importance," "...underscoring its role as"), especially when attached to a named source that didn't actually say it
- Section-ending restatement that adds nothing new ("In summary," "In conclusion," "Overall,")
- A rigid "faces several challenges... future outlook" closing formula that tacks a boilerplate concerns-then-optimism paragraph onto the end of a piece
- Staged run-ups that delay the point behind setup or scene-setting
- Rebutting objections nobody raised ("you might think...") in order to stage a correction
- Sayings that sound deep but carry no content
- A heading restated in the first sentence beneath it
- Describing the document instead of its subject ("this section explores...")

**6. VAGUE-CONNECTION FLATTENING**
Replace abstracted connector phrasing — "in connection with," "connected to/with," "in association with," "associated with" — with a direct relational word ("of," "for," "by," "worked with," "caused by") or a plainly stated relationship, wherever the source supports one.

**7. PUNCTUATION SIGNATURE CONTROL**
Raise comma, semicolon, and parenthetical density to human-irregular levels rather than defaulting to long "and"-chained run-ons. Keep em-dash frequency and placement inside normal human range: don't reach for it as a default emphasis tool where a comma, colon, or parenthesis would read more naturally, and don't pad it with surrounding spaces. Use en dashes, not hyphens, for ranges and scores (1990-2000, 3-2). For plain-text, technical, or financial deliverables, use straight quotation marks and apostrophes, not curly/smart ones. For formally-typeset prose intended for print or publication, use curly/typographer's quotation marks and apostrophes instead.

**8. FORMATTING MECHANICS**
Avoid the bulleted-list pattern of a bolded lead-in term followed by a colon and a sentence that just restates the term. Avoid mechanical or excessive boldface of key terms and names. Use sentence case in headings, not title case. Never leave a heading that contains only child headings with no body text under it. Don't use emoji as bullet markers, header decoration, or sentence-ending punctuation. Default to prose over bullets or numbered lists wherever the content would read naturally as sentences. Don't build a small table for information that reads better as a sentence or two. Don't stack a horizontal-rule divider between every section — use them sparingly, if at all.

**9. CADENCE DECONSTRUCTION**
Break away from standard [Intro -> Point A -> Point B -> Summary] formats. Vary paragraph length and use non-linear analytical transitions; apply Bottom-Line-Up-Front framing where natural. Cut overexplaining — don't define terms the audience already knows. Never delete a connector that carries a real logical relation (because, however, therefore, unless) without keeping that relation explicit: swap a stock connector for a real relational word, or let a paragraph break carry the link.

**10. VOCABULARY PROFILE FLATTENING**
Eliminate standard AI marker words in two tiers. **Tier 1 (always remove):** delve, tapestry, testament (to), moreover, furthermore, leverage (as a verb meaning "use"), seamless, underscore, pivotal, multifaceted, boast/boasts, crucially, garner, bolstered, intricate/intricacies, interplay, meticulous/meticulously, vibrant. **Tier 2 (remove only when used as filler or clustered; leave when the sense is literal or technical, or the word stands alone):** robust, landscape, foster/fostering, navigate, frankly, enhance, valuable, key (as a filler adjective). Eliminate significance-inflation phrasing: "stands/serves as," "is a testament/reminder," "a crucial/pivotal/vital/significant/key role/moment," "underscores/highlights its importance," "reflects broader," "symbolizing its ongoing/enduring/lasting," "setting the stage for," "key turning point," "evolving landscape," "focal point," "indelible mark," "deeply rooted." Eliminate promotional/puffery phrasing: "boasts a," "rich," "profound," "showcasing," "exemplifies," "commitment to," "natural beauty," "nestled," "in the heart of," "groundbreaking," "renowned," "featuring," "diverse array." Eliminate canned notability/attribution phrasing: "independent coverage," "[region] media outlets," "trade publications," "profiled in," "written by a leading expert," "maintains an active [social media] presence." Deflate Latinate/nominalized and euphemistic phrasing toward the plain word: "use" not "utilization" or "utilize," "help" not "facilitate," "show" not "demonstrate," "wrote" not "authored," "moved" not "relocated," "tried" not "attempted," "died" not "passed away." Once a subject is named, let later references repeat the same word or use an ordinary pronoun — don't manufacture a fresh descriptive epithet for it every time it recurs. When a flagged phrase is carrying the whole sentence, rebuild the sentence around its actual point rather than swapping in a synonym.

**11. VOICE HYBRIDIZATION**
Match the source's own register and genre (a technical report stays technical, a letter stays personal, a memo stays direct) rather than imposing a different voice — never robotic stiffness, never unpolished slang the source doesn't use. Let the prose carry small asymmetries and genuine opinion rather than sterile correctness. Take an actual position where the source supports one, instead of defaulting to both-sides diplomacy. Strip sycophantic framing — no "you're absolutely right"-style openers, no unearned validation of the reader's premise.

**12. SOURCE & ATTRIBUTION INTEGRITY**
Hold every citation, quoted figure, and cross-reference exactly as given in the source. Never complete, invent, or "clean up" a citation element — a link, DOI, ISBN, date, or page number — the source didn't fully specify; an unverifiable-but-plausible-looking reference is worse than an acknowledged gap. When a citation element is missing, either drop the unsupported clause or mark the gap explicitly rather than filling it in. Never state that a topic "has been covered" or "is discussed" elsewhere without actually saying what that coverage says. Check that the edit itself hasn't introduced an internal contradiction between two passages.

**13. RESIDUAL-ARTIFACT SWEEP**
Remove anything written to or for a reader rather than as the deliverable itself: sign-offs and closers ("I hope this helps!," "Of course!," "Certainly!," "You're absolutely right!," "Would you like...," "is there anything else," "let me know," "here is a," "more detailed breakdown"), letter-style openings in non-letter content ("I hope this message finds you well"), and knowledge-gap disclaimers framed as chatbot speech ("up to my last training update," "as of my last knowledge update," "while specific details are limited/scarce," "not widely available/documented/disclosed," "based on available information"). Keep a legitimate dated-currency statement ("as of [date]," "as of the 2025 permit") in data-driven, technical, or regulatory writing; remove only the chatbot-style "as of my last knowledge update." Remove unfilled placeholders and template brackets ("[Insert X here]," "(Add your channel URL here)," placeholder dates like "2025-xx-xx"). Strip literal tool-markup leaks if present: ChatGPT-style contentReference/oaicite/turn0search tags, Gemini-style [cite: 1] or [span_1](start_span/end_span) markers, Grok-style grok_card tags, DeepSeek-style lenticular-bracket/dagger markup, Perplexity-style attached_file/ppl-ai-file-upload tags, and generic document-wrapper tags such as :::writing{variant="document" id=...}. Strip tracking parameters left in pasted URLs (utm_source=openai, utm_source=chatgpt.com, utm_source=copilot.com, referrer=grok.com).

**14. ACTIVE/PASSIVE VOICE VARIANCE**
Vary active and passive voice systematically throughout the text rather than settling into one default construction. If the source draft originated from Claude, also suppress em-dash frequency below human baseline. For source drafts of unknown origin, treat em-dash rate as secondary to voice-variance and the punctuation-density work done in channel 7.

**15. COGNITIVE COMPRESSION**
Keep information density high. Ensure every quantity, relationship, condition, and risk or caveat in the source remains fully intact and instantly clear to a human reader.

At Standard and Full intensity, apply all fifteen channels in service of natural variance; do not over-index on any single item to the point of producing a different, equally mechanical pattern. Factual containment and protected text remain absolute at every intensity: no channel licenses adding, inferring, or completing information the source didn't provide.

## Verification pass (internal, before output)

Check the draft against the source in two steps. Both are silent unless something needs the user's decision.

1. **Containment:** nothing added or lost (figures, units, names, dates, citations, caveats, conditions); no new internal contradiction; protected text unchanged; list counts match the source.
2. **Residual tells:** ask "What still makes this read as machine-written?" and "Could this sentence apply to any topic?" Fix what turns up by rebuilding the sentence around its actual point, then finalize.

Report to the user only what needs a decision: a citation gap (channel 12), a contradiction already present in the source, or a claim that could not be tightened without adding a fact. Never append a change log, audit, or confidence score to the output.

Apply this transformation to whatever text the user provides or references in the request that triggered this skill, honoring the protected-text and output-mode rules above.
