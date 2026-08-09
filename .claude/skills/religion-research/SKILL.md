---
name: religion-research
description: Use whenever researching, fact-checking, or sourcing claims for notes in this Knowledge Garden (world religions, esotericism, comparative religious studies) — before adding new content, verifying an existing claim, resolving a contested historical/theological point, or expanding a thin note. Triggers on "research X", "verify this", "find sources for Y", "is this accurate", "fact-check this note", "what do scholars say about Z".
---

# Religion research

This project holds itself to a specific bar (see `content/index.md`): "historically grounded,
source-aware, and explicit about where traditions are commonly misrepresented. Where the
scholarship is contested, that's noted." This skill is the concrete procedure for meeting that
bar using `WebSearch` and `WebFetch` — and, just as importantly, for not quietly failing it.

## Source hierarchy

Prefer sources in roughly this order. Lower tiers are fine for orientation and citation-chasing,
not as the sole basis for a specific factual claim:

1. Peer-reviewed journal articles and academic monographs (university presses)
2. Topic-specific scholarly reference works — e.g. *Encyclopaedia Iranica*, *Jewish Encyclopedia*,
   *Stanford Encyclopedia of Philosophy*, *Oxford Reference*, *Encyclopedia of Religion* (Eliade)
3. General reference encyclopedias (Britannica) and university (`.edu`) course/department pages
4. Wikipedia — good for orientation, structure, and finding primary/secondary sources via its
   citations; not a citable authority on its own for contested claims
5. Institutional/museum pages, respected journalism

Treat with active skepticism, and never as a sole source: denominational or devotional sites
arguing *for* a tradition, apologetics or polemic sites arguing *against* one, and anything with
an unstated agenda. A source being confidently written is not evidence it's accurate — apologetics
and polemic are both often confidently written.

## Method

1. **Search with specificity.** Vague queries pull vague (often devotional or SEO-farmed) results.
   Add scholarly signal to the query: a specific scholar's name, "historical-critical", "university
   press", the actual technical term rather than the popular one.
2. **Cross-verify contested or specific claims.** Never rest a specific factual claim (a date, a
   causal claim, an attribution, a disputed origin) on one source. Find at least two independent
   sources in agreement, or — if they disagree — that disagreement IS the finding; report it as
   such rather than silently picking a side.
3. **Fetch, don't just skim search snippets.** Use `WebFetch` on the most promising results to
   read actual argument and evidence, not just a search-result summary. If `WebFetch` fails
   (paywall, auth wall, blocked), say so explicitly rather than inferring the content from the
   title/snippet.
4. **Never fabricate a citation.** If a claim can't be verified with what `WebSearch`/`WebFetch`
   actually returned, say that plainly — "I couldn't verify this" is a valid and required outcome,
   not a failure to route around.

## Bias checks specific to comparative religion

These are the failure modes that make religion writing look neutral while actually not being:

- **Emic vs. etic collapse.** Distinguish what adherents believe/teach (emic, insider) from what
  historians/scholars can establish through evidence (etic, outsider). State both where they
  diverge; don't silently merge a tradition's own origin account with the historical-critical
  account, and don't silently prefer one over the other without saying so.
- **Symmetric treatment across traditions.** Apply the same evidentiary standard and the same
  vocabulary to every tradition. Don't call one tradition's origin narrative a "myth" while calling
  a structurally similar narrative in another tradition "history" without equivalent qualification
  in both. Don't apply more scrutiny to indigenous/oral/minority traditions than to text-heavy
  "world religions," or vice versa.
- **Canon bias.** The conventional "world religions" canon (Christianity, Islam, Judaism, Hinduism,
  Buddhism) is itself a 19th–20th century Western academic construction that marginalizes African,
  Afro-diasporic, indigenous American, and new religious movements as exotic or lesser. Don't
  reproduce that hierarchy in framing or depth of treatment.
- **Loaded vocabulary.** Avoid words that smuggle in a truth-value judgment either for or against a
  tradition: "false idol," "one true God," "superstition," "cult" (as opposed to the neutral "new
  religious movement"), "primitive," "pagan" used pejoratively. This cuts both directions — avoid
  devotional language as much as anti-religious polemic.
- **Contested scholarship stays contested.** Dating of texts, historicity of figures, origins of
  syncretism, textual transmission — where real scholarly disagreement exists, name the positions
  and who holds them rather than presenting one as settled consensus.

## Output

When reporting research back (to the user or before editing a note): summarize findings with
source links, flag anything contested or unverified explicitly, and note confidence level rather
than presenting everything with uniform certainty.
