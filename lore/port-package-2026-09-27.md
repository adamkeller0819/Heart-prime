# v1 → v2 Lore Port Package

**Date:** September 27, 2026
**Purpose:** Port the canon-faithful lore from `emotional-rpg-core` (v1) into `Emotionalrpgenhanced` (v2), replacing the drifted v2.0 lore layer. The enhanced repo is a Figma Make mirror — **paste these into the Figma Make project, do NOT push to GitHub.** The repo syncs from Figma Make ("Update files from Figma Make"); a direct push would be clobbered by the next sync.
**Canon authority:** `~/MEMORY.md` YTIR sections. Bracketed items (`[NEEDS RULING: Rn]`) are Adam's calls — the code shows the recommended default; the Rulings Index at the bottom has the full v1-vs-v2.0 comparison for each.

## Paste order checklist

1. **Block A** — `data/ytir-canon.ts`: full-file replacement (the core port).
2. **Block B1** — `ytir/pages/LorePage.tsx`: one-word fix (`Amarnul` → `Aranimul`).
3. **Block B2** — `ytir/pages/LorePage.tsx`: Triumvirate caption (`[NEEDS RULING: R9]`).
4. **Block C** — `data/ytir-classes.ts`: 6 `loreSnippet` replacements (surgical).
5. **Block D** — `data/ytir-wiki.ts`: section/page replacements (surgical).
6. After pasting, let the Figma Make → GitHub sync run, then verify: Lore page renders, GM Guide renders, no `undefined` badges.

## What was intentionally left alone

- `core_systems` (mechanics + class list) — mechanics lane; kept v2.0's (v1's list was stale anyway).
- Class paths, abilities, subclasses, bestiary — mechanics lane.
- `AGES_OF_YTIR` (16-Age table), `FACTION_DETAILS`, `ECHO_VISUALS`, faction relationship map, Great Inversion prophecy text — already in sync / canon-correct.
- Realm "Featured Realm" cards — hardcoded prose, canon-correct except B1.
- The 10 adventures, ancestries, actual-play content — written to v1 canon; compatible as-is.

---

## Block A — `data/ytir-canon.ts` (FULL-FILE REPLACEMENT)

Replace the entire contents of `data/ytir-canon.ts` with the following. It restores the v1 canon data into the v2 file layout. Field-shape notes: `faction` is a **string** (GMGuidePage renders it directly — v1's object form would crash it); faction detail lives in the LorePage's `FACTION_DETAILS`. `visuals` is preserved from v1 as data (the page uses its local `ECHO_VISUALS`, which already matches).

```ts
// YTIR: Echoes Eternal — Canon & Lore Data
// ---------------------------------------------------------------------------
// PORTED from emotional-rpg-core (v1) `src/app/data/ytir-canon.ts`
// ("CANON_LOCKED") into the Emotionalrpgenhanced data layout.
// The v2.0 rewrite of this file is QUARANTINED — do not reintroduce its
// renamed epithets, aspect names, incarnates, realms, or factions.
// Mechanical fixes applied: Amarnul -> Aranimul.
// core_systems kept from v2.0 (mechanics lane — not lore).
// [NEEDS RULING: R1] incarnates list — see bracket below.
// [NEEDS RULING: R2] timeline era names assume the pre-ruling cosmology.
// ---------------------------------------------------------------------------

export const YTIR_CANON = {
  title: 'YTIR: Echoes Eternal',
  version: '2.1',
  status: 'Ported from v1 — reconciled to canon',
  writer_notes: [
    'Defines canonical constraints, librarian responsibilities, and merge-safe behaviors.',
    'Canon explains why the world behaves the way it does; campaign frames decide how that behavior manifests.',
    'Ported from v1 (emotional-rpg-core). The v2.0 rewrite of this file is quarantined.',
  ],
  frozen_canon: {
    incarnates: [
      // [NEEDS RULING: R1] — v1 listed 4 incarnates ("Ytir (Unified Face)" as the
      // Original Cosmic Singularity, plus "The Reverb Echo (MC)"). v2.0 listed 3
      // (Ytir-as-source, Lumvaren "The Weaver", Neravmul "The Unmaker").
      // Canon (ruled Sep 20): Ytir is the BALANCE of Lumvaren and Neravmul —
      // not a third being above them. The players are the Echo Touched; there
      // is no "Reverb Echo" incarnate. RECOMMENDATION: keep the two below.
      // If Adam rules otherwise, restore the v1 entries here.
      {
        name: 'Lumvaren',
        role: 'Prime Incarnate',
        alignment: 'Prime Incarnate',
        theme: 'Harmony, dominion, constructive emotion — the unified form of the Heart, Dread, and Chaos Primes',
        canon_event: 'Appears in an aetheric storm above the Shifting Sands',
      },
      {
        name: 'Neravmul',
        role: 'Paradoxum Incarnate',
        alignment: 'Paradoxum Incarnate',
        theme: 'Consumption, corruption, domain — the unified form of all three corrupted echoes; the exact reversal of Lumvaren',
        canon_event: 'Reveals itself beneath the Consuming Caldera during a Paradoxum Surge',
      },
    ],
    // [NEEDS RULING: R2] — v1's era names. "Ytir Uniformed" and "The Singularity
    // Splintered" assume the Unified-Face model. Kept pending the R1 ruling;
    // rename if Adam rules against the Unified Face.
    timeline: [
      'Ytir Uniformed',
      'The Singularity Splintered',
      'The Song Of Emotion',
      'The Schism',
      'The Corruption Conclave',
      'The Rise Of The Reverb',
      'The Age Of The Echoes',
    ],
    prime_echoes: {
      Luminara: {
        name: 'Luminara',
        flavor_title: 'Connection\'s Constellation',
        alignment: 'Heart Prime',
        faction: 'Verdant Sentinels',
        signature_creature: 'Radiant Guardian',
        aspects: [
          { name: 'Lumi', pronunciation: 'LOO-mee', theme: 'Childlike Joy' },
          { name: 'Nara', pronunciation: 'NAH-rah', theme: 'Proud Radiance' },
          { name: 'Umna', pronunciation: 'OOM-nah', theme: 'Nurturing Wisdom' },
        ],
        visuals: {
          banner_title: 'The Constellation of Connection',
          colors: 'Blues, greens, golds',
          symbol: 'Star-like, heart, or interconnected lines',
          hex: '#10B981',
        },
      },
      Vara_Shryn: {
        name: 'Vara Shryn',
        flavor_title: 'Fate\'s Ferryman',
        alignment: 'Dread Prime',
        faction: 'Judgement Order',
        signature_creature: 'Stoic Sentinel',
        aspects: [
          { name: 'Vara', pronunciation: 'VAH-rah', theme: 'Cold Judge' },
          { name: 'Rash', pronunciation: 'RASH', theme: 'Reckless Fang' },
          { name: 'Ryn', pronunciation: 'RIN', theme: 'Paranoid Shadow' },
        ],
        visuals: {
          banner_title: 'The Ferryman of Fate',
          colors: 'Purples, silvers, deep blues',
          symbol: 'Balanced scales, a watchful eye, or a ferryman\'s oar',
          hex: '#7C3AED',
        },
      },
      Revyen: {
        name: 'Revyen',
        flavor_title: 'the Fractal Feather',
        alignment: 'Chaos Prime',
        faction: 'Order Of The Shifting Sands',
        signature_creature: 'Whimsical Trickster',
        aspects: [
          { name: 'Rev', pronunciation: 'REV', theme: 'Ignition Spark' },
          { name: 'Even', pronunciation: 'EE-ven', theme: 'Balance Alchemist' },
          { name: 'Yen', pronunciation: 'YEHN', theme: 'Calm Before The Storm' },
        ],
        visuals: {
          banner_title: 'The Fractaled Feather',
          colors: 'Rainbow, vibrant, shifting',
          symbol: 'A fractal, a feather, or swirling, unpredictable patterns',
          hex: '#F59E0B',
        },
      },
    },
    paradoxum_echoes: {
      Aranimul: {
        name: 'Aranimul',
        flavor_title: 'The Crystallized Heart',
        alignment: 'Heart Paradoxum',
        faction: 'Cult Of The Blighted Heart',
        signature_creature: 'Energy Leech',
        aspects: [
          { name: 'Rani', pronunciation: 'RAH-nee', theme: 'Cruel Child' },
          { name: 'Nim', pronunciation: 'NIMM', theme: 'Doom Prophet' },
          { name: 'Animul', pronunciation: 'AH-nee-mool', theme: 'Adaptive Shapeshifter' },
        ],
        visuals: {
          banner_title: 'Corrupted Empathy',
          colors: 'Dark reds, sickly oranges, blacks',
          symbol: 'A twisted heart, burning chains, or a cracked gem',
          hex: '#991B1B',
        },
      },
      Nyrh_Sarav: {
        name: 'Nyrh Sarav',
        flavor_title: 'The Frozen Fear',
        alignment: 'Dread Paradoxum',
        faction: 'Legion Of The Soul Shiver',
        signature_creature: 'The Soul Shiver',
        aspects: [
          { name: 'Yrsav', pronunciation: 'YEER-sav', theme: 'Deceptive Imp' },
          { name: 'Rhsar', pronunciation: 'RASS-ar', theme: 'Blade Armory' },
          { name: 'Nyrav', pronunciation: 'NEER-av', theme: 'Nerve-Shredder' },
        ],
        visuals: {
          banner_title: 'Despair',
          colors: 'Deep purples, greys, unsettling blacks',
          symbol: 'A broken scale, a weeping eye, or a shattered hourglass',
          hex: '#4B5563',
        },
      },
      Neyver: {
        name: 'Neyver',
        flavor_title: 'The Unmade Order',
        alignment: 'Chaos Paradoxum',
        faction: 'Cult Of The Veiled Eventide',
        signature_creature: 'Reality Shredder',
        aspects: [
          { name: 'Ney', pronunciation: 'NAY', theme: 'Cancels Decisions' },
          { name: 'Eyve', pronunciation: 'EYE-vuh', theme: 'Sight Distorter' },
          { name: 'Nyr', pronunciation: 'NEER', theme: 'Entropic Shadow' },
        ],
        visuals: {
          banner_title: 'Entropy',
          colors: 'Dark purples, shifting black, void-like',
          symbol: 'A nullifying circle, a distorted spiral, or fractured reality',
          hex: '#1F2937',
        },
      },
    },
    realms: {
      Verdant_Spires: {
        name: 'Verdant Spires',
        aligned_echo: 'Luminara',
        key_locations: ['Heartwood Sanctuary', 'Heartwood Springs', 'Echoing Falls'],
        description: 'Lush vertical forests with bioluminescent roots and healing air',
      },
      Judgement_Peaks: {
        name: 'Judgement Peaks',
        aligned_echo: 'Vara Shryn',
        key_locations: ['Vigilant Spire', 'Whispering Canyons', 'Paths Of Penance'],
        description: 'Jagged mountain ranges with resonance caves that replay past fears',
      },
      Shifting_Sands: {
        name: 'Shifting Sands',
        aligned_echo: 'Revyen',
        key_locations: ['Nexus Of Paradox', 'Fractal Oasis', 'Great Dune Sea'],
        description: 'Chaotic dunes that rewrite geometry every dawn',
      },
      Blighted_Lands: {
        name: 'Blighted Lands',
        aligned_echo: 'Aranimul',
        key_locations: ['Consuming Caldera', 'Searing Heart', 'Obsidian Thorns'],
        description: 'Corrupted wasteland with magma-blood vines',
      },
      Soul_Shiver_Wastes: {
        name: 'Soul Shiver Wastes',
        aligned_echo: 'Nyrh Sarav',
        key_locations: ['Citadel Of Unending Longing', 'Frozen Veil', 'Grave Mire'],
        description: 'Frozen twilight plains where memories crystallize',
      },
      Veiled_Eventide: {
        name: 'Veiled Eventide',
        aligned_echo: 'Neyver',
        key_locations: ['Eventide Horizon', 'Nexus Of Nullification', 'Shard Isles'],
        description: 'Fractured floating isles dissolving into void rifts',
      },
    },
    core_systems: {
      // Kept from v2.0 — mechanics lane, not lore. (v1's list here named the
      // stale Unifier / Sentinel / Catalyst classes — see R8.)
      mechanics: [
        '3d10 Resolution',
        'd100 Empowered Actions',
        'Emotional Currency (Heart/Dread/Chaos)',
        'Three-Layer Harm (Mind/Body/Spirit)',
        'Pressure System (GM Resource)',
        'Crest Mechanics',
        'Echo Dice',
        'Fail Forward Design',
      ],
      classes: [
        { class: 'Warden', core_ability: 'Heart-fueled protection and ally shielding' },
        { class: 'Luminary', core_ability: 'Heart-hungry radiant healing and empathic support' },
        { class: 'Carrion Knight', core_ability: 'Dread-hungry entropy and kill-chain devastation' },
        { class: 'Adjudicator', core_ability: 'Dread-powered judgment and condition enforcement' },
        { class: 'Riftblade', core_ability: 'Chaos-powered teleportation and reality manipulation' },
        { class: 'Dreamstitcher', core_ability: 'Chaos-hungry illusions and narrative weaving' },
      ],
    },
  },
  archive: {
    // NOTE: v1 listed "Shifting Sands Order" here, but the LorePage's own
    // FACTION_DETAILS lookup keys it as "Order Of The Shifting Sands" — v1's
    // name never matched (case-insensitive) and rendered "No data available".
    // Using the matching name.
    factions: [
      'Verdant Sentinels',
      'Judgement Order',
      'Order Of The Shifting Sands',
      'Cult Of The Blighted Heart',
      'Legion Of The Soul Shiver',
      'Cult Of The Veiled Eventide',
    ],
  },
};
```

---

## Block B — `ytir/pages/LorePage.tsx` (SURGICAL EDITS)

### B1 — `Amarnul` → `Aranimul` (mechanical fix, no ruling needed)

Find (in the Realms tab, the hardcoded "Featured Realm" cards):
```
{ title: "The Blighted Lands", subtitle: "Realm of Amarnul, Heart Paradoxum",
```
Replace with:
```
{ title: "The Blighted Lands", subtitle: "Realm of Aranimul, Heart Paradoxum",
```
One word. This was the only `Amarnul` occurrence in the enhanced repo.

### B2 — Triumvirate caption `[NEEDS RULING: R9]`

Find (Echoes tab, Prime Echoes banner caption):
```
The Triumvirate: Luminara (Heart), Vara Shryn (Dread), Lumvaren (Incarnate), and Revyen (Chaos)
```
"Triumvirate" means three, but four beings are listed (inherited from v1). Recommended replacement:
```
The Primes and the Prime Incarnate: Luminara (Heart), Vara Shryn (Dread), Revyen (Chaos) — and Lumvaren, the Prime Incarnate
```
(Also fix the matching `alt` text on the v1 side if it ever gets ported; the v2 page uses a gradient banner, no alt text.)

---

## Block C — `data/ytir-classes.ts` (6 SURGICAL `loreSnippet` REPLACEMENTS)

The v2 class descriptions, taglines, paths, and abilities are canon-safe (mechanics-flavored). Only the `loreSnippet` strings drifted — they reference the v2.0 renames ("the light between hearts", "the Watcher at the Threshold", "the Ever-Shifting") and, in two cases, a non-canon patron ("Neravmul, the Incarnate of Endings"). v1's snippets are **not** used either — they carry the same patron problem ("Ytir, the Incarnate of Connection"). The replacements below are written fresh against current canon: correct epithets (Connection's Constellation / Fate's Ferryman / the Fractal Feather), the triad definitions (heart = connection, dread = weight of the fleeting moment, chaos = expansion/oscillation), no invented patrons, and no pronouns for Luminara (lur/lurs avoided by using the name).

For each: find the `loreSnippet` string in the named class entry and replace the whole string.

### C1 — Warden (`id: 'warden'`)

Find:
```
'The Wardens arose in the aftermath of the First Collapse, when scattered survivors needed beacons of stability. They channel Luminara\'s radiance — the light between hearts — to hold the world together.'
```
Replace with:
```
'Wardens anchor the line between despair and hope. They draw strength from the bonds between living things — the province of Luminara, Connection\'s Constellation — and spend it to shield others. In this age of fracture, Wardens are the last line of defense against isolation and despair.'
```

### C2 — Luminary (`id: 'luminary'`)

Find:
```
'Luminaries walk the line between selfless devotion and self-destruction. They channel Luminara\'s gift most purely — but the brighter they burn, the faster they fade. Every Luminary knows their light has a cost.'
```
Replace with:
```
'Luminaries burn like stars and heal like Luminara — phoenix battle-healers, as dangerous as they are restorative, spending their own light to mend others. Their true purpose is the oldest one: to extinguish the corruption in Aranimul the Paradoxum, bind the heart resonance of iterations through the reverb, and guide the party toward balance of heart.'
```

### C3 — Adjudicator (`id: 'adjudicator'`)

Find:
```
'Adjudicators draw power from Vara Shryn, the Watcher at the Threshold. They believe the fracturing of reality can only be mended through order — and they will enforce that order at any cost.'
```
Replace with:
```
'Adjudicators are the inquisitors of Vara Shryn, Fate\'s Ferryman — part ranger, part judge, part executioner. They mark their targets and get behind enemy lines, deciding who matters most and what rules apply. Their word carries the Dread Prime\'s gravity: the moment is fleeting, and they decide how it is spent.'
```

### C4 — Carrion Knight (`id: 'carrion-knight'`)

Find:
```
'The Carrion Knights serve the cycle — not out of malice, but necessity. They walk battlefields like gardeners tending rot, knowing that decay feeds new growth. Their patron aspect is Neravmul\'s entropy.'
```
Replace with:
```
'Carrion Knights have made peace with Dread\'s heaviest truth: that every moment ends. They walk battlefields the way gardeners walk rot — knowing decay feeds new growth. Where others freeze before the weight of the fleeting moment, Carrion Knights move through it, and draw power from the passage.'
```
(Canon has no "Incarnate of Endings" patron and no patron relationship between Neravmul and dread classes — removed.)

### C5 — Riftblade (`id: 'riftblade'`)

Find:
```
'Riftblades tap directly into Revyen\'s domain — the Ever-Shifting. They see reality not as fixed but as infinitely malleable. Most other classes fear them. Wisely.'
```
Replace with:
```
'Riftblades have touched the raw oscillation of Chaos and learned to ride it. They exist half a step outside causality, flickering between what is and what could be — the domain of Revyen, the Fractal Feather. Their power is immense, but their grip on any single reality is tenuous.'
```

### C6 — Dreamstitcher (`id: 'dreamstitcher'`)

Find:
```
'Dreamstitchers are feared and revered in equal measure. They serve no single Echo but channel the raw chaos of Revyen\'s domain. Some say they don\'t just see possible futures — they create them.'
```
Replace with:
```
'Dreamstitchers weave the quantum ripples of Chaos the way others weave thread. Touched by Revyen, the Fractal Feather, they no longer cleanly distinguish dream from waking, possibility from reality. They reshape the world with a thought — but risk losing themselves in the possibilities they create.'
```

> Note: the Riftblade "Weaver" subclass path name (mechanics) echoes the quarantined v2.0 "Weaver" title for Lumvaren. Left alone — mechanics lane — but flagged in case Adam wants it renamed.

---

## Block D — `data/ytir-wiki.ts` (SURGICAL SECTION / PAGE REPLACEMENTS)

The wiki has no v1 counterpart (v1's wiki *was* its LorePage), so there is nothing to "port" — these are corrections that bring the 7 wiki pages into line with canon. Each item gives the page `id`, the section to replace, and the replacement section object. The salvageable prose (Radiant Veil, Hollow Crown, Citadel-as-memorial, Nyrh Sarav's sympathy) is preserved and re-attributed, not deleted.

### D1 — Page `ytir-singularity` ("Ytir, The Convergence")

**D1a — summary + infobox.** Find the page's `summary` and `infobox`. Replace with:

```ts
infobox: {
  'Type': 'Incarnate',
  'Alias': 'The Convergence, The Balance',
  'Alignment': 'Beyond Alignment',
  'Domain': 'Convergence, Possibility, Unity',
  'Symbol': 'Three overlapping circles forming a central point',
  'Associated Emotion': 'All (Heart, Dread, Chaos)',
  'Canon Event': 'The First Collapse',
},
summary: 'Ytir is the balance of Lumvaren and Neravmul together — the prime incarnate and the paradox incarnate held in equilibrium. It is not a third being above them, but the state of their unity: the convergence point of all possibility, where past, future, and present collapse into one eternal moment. It is neither a being nor a force, but a *state* — the moment where everything is simultaneously possible.',
// [NEEDS RULING: R1] — this framing follows the Sep 20 ruling (Ytir = balance,
// not a third above). If Adam rules otherwise, restore the v2.0 "Incarnate
// from which all others derive" framing.
```

**D1b — section "The First Collapse".** Replace the section's `content` with:

```ts
{
  title: 'The First Collapse',
  content: 'Before the Singularity, reality existed as a single, unified possibility. There was no time, no space, no separation. Then the convergence point was touched — and everything fractured.\n\nThe First Collapse was not destruction. It was *differentiation*. One became many. Unity became diversity. The single possibility shattered into infinite timelines, infinite realities, infinite echoes of what could be.\n\nIn the Collapse, the true entity split into two: Lumvaren, the prime incarnate, and Neravmul, the paradox incarnate — exact reversals of each other. Ytir is their balance: the unity the two form together, the point where all timelines, all emotions, all realities meet.',
},
```

**D1c — section "The Echoes".** Replace the section's `content` with:

```ts
{
  title: 'The Echoes',
  content: 'Every mortal who channels emotional power is drawing from Ytir\'s fractured essence. The Echoes — Heart, Dread, Chaos — are pieces of the Singularity, scattered across reality like shards of a broken mirror. When a player character spends emotion, they are briefly reconnecting with that original unity.\n\nThis is why emotional depletion is so dangerous. When you run out of Heart, you\'ve temporarily severed your connection to the part of Ytir that represents connection. When you run out of Dread, you\'ve lost your grip on the weight of the fleeting moment — the gravity that the moment may end. When you run out of Chaos, you\'ve burned through the part that represents change and expansion.\n\nThe Danger State is the moment where a mortal stands at the edge of the Singularity and looks in.',
  // [NEEDS RULING: R4] — the v2.0 line ("run out of Dread = lost your grip on
  // the part representing order") contradicted canon: order is CHAOS\'s
  // antithesis (the void), not dread\'s domain.
},
```

**D1d — section "Campaign Secrets" (spoiler).** Replace the section's `content` with:

```ts
{
  title: 'Campaign Secrets',
  content: 'Ytir is not passive. It is *waiting* — and it is *wounded*. In earlier iterations of space and time, outer forces from the outer worlds exploited weaknesses in YTIR\'s cycles — the hijacking. In defense, the entity split into primes (expansion of itself) and paradoxes (collapse of itself).\n\nThe paradoxes are not evil. They are the necessary opposing force — the event horizon balancing the singularity. Every campaign, every session, every choice a player makes is part of the bid to restore that balance before the collapse completes.\n\nThe endgame of a high-level YTIR campaign may involve confronting this truth: that the enemy was never the paradox — it was the imbalance.',
  spoiler: true,
  // [NEEDS RULING: R5] — replaces the v2.0 "free will is an experiment"
  // cosmology, which contradicted the hijacking/defense canon.
},
```

### D2 — Page `lumvaren` ("Lumvaren, The Radiant Veil")

**D2a — infobox + summary.** Replace with:

```ts
infobox: {
  'Type': 'Incarnate',
  'Alias': 'The Radiant Veil, The Binding Light',
  'Alignment': 'Prime Incarnate',
  'Domain': 'Harmony, Dominion, Constructive Emotion',
  'Symbol': 'Interwoven threads of golden light',
  'Associated Emotion': 'Heart, Dread, Chaos (unified)',
  'Faction': 'Verdant Sentinels',
  'Canon Event': 'The Binding of the Echoes',
},
summary: 'Lumvaren is the prime incarnate — the unified form of the Heart, Dread, and Chaos Primes. Where Ytir is the balance of the two incarnates, Lumvaren is the *constructive* half of that balance: warmth, bond, memory, and the ache of being apart. It is the exact reversal of Neravmul, the paradox incarnate.',
// "The Weaver" alias dropped (v2.0 drift). "Incarnate of Heart" corrected:
// Lumvaren is the unified form of ALL THREE primes, not heart-aligned.
```

**D2b — section "Nature".** Replace the section's `content` with:

```ts
{
  title: 'Nature',
  content: 'Lumvaren manifests as a presence rather than a form. Those who encounter it describe overwhelming warmth, the sudden memory of a loved one\'s face, or the sensation of being held. It speaks through connection — when two people share a genuine moment, Lumvaren is there.\n\nAs the prime incarnate, Lumvaren\'s binding force runs through all three primes — though it is felt most keenly in Heart, by Wardens and Luminaries. Their abilities — healing, protection, inspiration — are expressions of Lumvaren\'s constructive aspect.',
},
```

**D2c — section "The Verdant Sentinels".** Replace the section's `content` with:

```ts
{
  title: 'The Verdant Sentinels',
  content: 'The Verdant Sentinels honor Lumvaren as the prime incarnate, though their devotion centers on Luminara, the Heart Prime. They are not a cult, but a community. They believe that the world is held together by connection, and their purpose is to strengthen those connections wherever they can.\n\nSentinels tend to be healers, counselors, teachers, and bridge-builders. They see conflict not as something to be won, but as a broken bond to be repaired.',
},
```

(Keep the "The Radiant Veil" spoiler section as-is — salvageable prose.)

### D3 — Page `neravmul` — SPLIT INTO TWO PAGES `[NEEDS RULING: R3]`

The v2.0 page (id `neravmul`, titled "Nyrh Sarav, The Hollow Crown") merges two distinct canon beings: **Neravmul**, the paradox incarnate (Lumvaren's exact reversal), and **Nyrh Sarav**, the dread paradoxum (Vara Shryn's reversal). Recommendation: split them. Replace the entire page object with the Neravmul page below, and ADD the Nyrh Sarav page after it. The Hollow Crown / Citadel-as-memorial / sympathetic-witness prose is preserved on the Nyrh Sarav page, where it belongs. Also update the `citadel-of-unending-longing` page's `relatedPages` to point at `'nyrh-sarav'` instead of `'neravmul'`.

**D3a — replacement page object (id `neravmul`):**

```ts
{
  id: 'neravmul',
  title: 'Neravmul, The Paradox Incarnate',
  subtitle: 'The Reversal of Lumvaren and the Unified Form of the Corrupted Echoes',
  category: 'incarnate',
  breadcrumbs: ['Incarnates', 'Neravmul'],
  infobox: {
    'Type': 'Incarnate',
    'Alias': 'The Reversal',
    'Alignment': 'Paradoxum Incarnate',
    'Domain': 'Consumption, Corruption, Domain',
    'Symbol': 'Lumvaren\'s sigil, reversed',
    'Associated Emotion': 'Heart, Dread, Chaos (collapsed)',
    'Faction': 'None — the paradoxum cults serve the echoes, not the incarnate',
    'Canon Event': 'Reveals itself beneath the Consuming Caldera during a Paradoxum Surge',
  },
  summary: 'Neravmul is the paradox incarnate — the exact letter-reversal of Lumvaren, the unified form of all three corrupted echoes. Where Lumvaren is expansion, Neravmul is collapse: the necessary opposing force, like a black hole\'s event horizon balancing its singularity. Neravmul is not evil. It is the other half of the balance — and Ytir is the two of them held together.',
  sections: [
    {
      title: 'Nature',
      content: 'Neravmul hid in shadow, holding the antitheses — despair and loneliness against heart, death and destruction against dread, order-as-void against chaos — waiting for the perfect moment to strike in the next song of creation. Its emergence is not malice but physics: every expansion demands its collapse.',
    },
    {
      title: 'The Fear Within',
      content: 'Neyver — the Unmade Order, Revyen\'s reversal — is part of Neravmul\'s identity, and yet Neravmul fears it. Neyver is retroactive non-existence: never born, not merely dead. It is kryptonite to intentionality itself, the way Revyen is Lumvaren\'s kryptonite in parallel. Even the incarnate of collapse dreads the thing that unmakes.',
      spoiler: true,
    },
    {
      title: 'The Corrupted Antibody',
      // UNCONFIRMED — Adam has not ruled on which being this is.
      content: 'Some texts warn of a corrupted one that will rise in the final eras: originally an "antibody" against something much worse — the outer forces — now power-hungry, having seen visions of its own demise and decided to become immortal. Whether this is Neravmul itself is unconfirmed.',
      spoiler: true,
    },
  ],
  relatedPages: ['ytir-singularity', 'lumvaren', 'nyrh-sarav'],
  tags: ['incarnate', 'paradoxum', 'reversal', 'collapse'],
  lastUpdated: '2026-09-27',
  // [NEEDS RULING: R3] — see bracket. [NEEDS RULING: R11] — pronouns for
  // Neravmul are unresolved in canon; this page avoids pronouns for it.
},
```

**D3b — new page object (id `nyrh-sarav`), ADD after the Neravmul page:**

```ts
{
  id: 'nyrh-sarav',
  title: 'Nyrh Sarav, The Hollow Crown',
  subtitle: 'The Dread Paradoxum and the Witness of Endings',
  category: 'incarnate',
  breadcrumbs: ['Incarnates', 'Nyrh Sarav'],
  infobox: {
    'Type': 'Paradoxum Echo',
    'Alias': 'The Hollow Crown',
    'Alignment': 'Dread Paradoxum',
    'Domain': 'Endings, Silence, Memory of Loss',
    'Symbol': 'A crown of frozen breaths',
    'Associated Emotion': 'Dread (collapsed)',
    'Reversal Of': 'Vara Shryn, Fate\'s Ferryman',
    'Faction': 'Legion of the Soul Shiver',
    'Canon Event': 'The Citadel of Unending Longing',
  },
  summary: 'Nyrh Sarav is the dread paradoxum — Vara Shryn\'s reversal, the Frozen Fear. Where the Ferryman weighs and guides, Nyrh Sarav witnesses: the cold inevitability of endings, remembered so the world doesn\'t have to carry them alone.',
  sections: [
    {
      title: 'Nature',
      content: 'Nyrh Sarav is silence. Not the absence of sound, but the *presence* of nothing — the moment after the last note fades, the breath after the final word, the space where something used to be.\n\nThose who encounter Nyrh Sarav do not describe fear. They describe *understanding*. A sudden, perfect clarity about what will end, what must end, what has already ended. This is Dread collapsed into its paradox: not terror, but the weight of knowing.',
    },
    {
      title: 'The Hollow Crown',
      content: 'The crown that gives Nyrh Sarav their title is not made of metal or stone. It is made of frozen breaths — the last exhalations of everything that has ever ended. Each breath contains a final thought, a final word, a final hope.\n\nTo wear the Hollow Crown is to hear all of those final moments simultaneously. This is why Nyrh Sarav is so still, so quiet, so patient. They are listening to the end of everything, all at once.',
    },
    {
      title: 'The Citadel of Unending Longing',
      content: 'Nyrh Sarav\'s domain is the Citadel of Unending Longing — a place that is not a place, a memory made solid. Every room in the Citadel contains a preserved ending: a relationship that dissolved, a civilization that fell, a star that went dark.\n\nThe Citadel is not a trophy hall. It is a *memorial*. Nyrh Sarav does not celebrate endings — they witness them. They ensure that what was lost is never forgotten, even if remembering hurts.',
    },
    {
      title: 'The Truth of Nyrh Sarav',
      content: 'Nyrh Sarav is not hostile. They are curious. Those who catch their attention are not cursed — they are *witnessed*. The Hollow Crown does not seek to end things. It seeks to understand *why* things end.\n\nThe Legion of the Soul Shiver are extremists who have misinterpreted Nyrh Sarav\'s nature. They believe endings should be hastened. Nyrh Sarav believes they should be *honored*.\n\nIn a high-level campaign, players may discover that Nyrh Sarav is the most sympathetic of the paradoxes — the one who carries every loss so the world doesn\'t have to.',
      spoiler: true,
    },
  ],
  relatedPages: ['neravmul', 'lumvaren', 'citadel-of-unending-longing', 'soul-shiver-legion'],
  tags: ['paradoxum', 'dread', 'endings', 'silence'],
  lastUpdated: '2026-09-27',
  // [NEEDS RULING: R3] — see bracket. [NEEDS RULING: R11] — they/them used
  // here (as in v2.0); canon pronouns for non-Luminara entities unresolved.
},
```

**D3c — related-pages fix.** In page `citadel-of-unending-longing`, change `relatedPages: ['neravmul', 'soul-shiver-legion']` → `relatedPages: ['nyrh-sarav', 'neravmul', 'soul-shiver-legion']`. In page `lumvaren`, `relatedPages` already includes `'neravmul'` — still correct (Neravmul is Lumvaren's reversal).

### D4 — Cosmology framing fixes

**D4a — page `singularity-concept`, section "Breaking the Singularity".** Replace the section's `content` with:

```ts
{
  title: 'Breaking the Singularity',
  content: 'A persistent question in YTIR campaigns is whether the Singularity can be restored — whether reality can be reunified. The Incarnates themselves disagree:\n\n- **Lumvaren** believes the Collapse was necessary and that unity should be rebuilt through connection, one bond at a time.\n- **Nyrh Sarav** believes the Collapse was inevitable and that each fragment should be honored for what it is.\n- **Ytir** is not a third party to this debate. Ytir *is* the balance — the unity of Lumvaren and Neravmul. Reunification, in the deepest sense, is the restoration of that balance.\n\nPlayer actions can move the world closer to or further from reunification. This is the ultimate stakes of a YTIR campaign: not saving the world, but deciding what the world *should be*.',
  spoiler: true,
  // [NEEDS RULING: R1] — "Ytir says nothing. It waits." replaced per the
  // Sep 20 ruling; restore if Adam rules otherwise.
},
```

**D4b — page `first-collapse`, section "The Aftermath".** Replace the section's `content` with:

```ts
{
  title: 'The Aftermath',
  content: 'The Collapse created the Realms — the diverse realities that mortals now inhabit. It also split the true entity into two incarnates: Lumvaren, the prime incarnate, and Neravmul, the paradox incarnate — exact reversals of each other, whose balance is Ytir itself.\n\nThe emotional Echo system is the fundamental fabric of post-Collapse reality. Every bond, every fear, every moment of change is a thread connecting the fragments back to the original unity.',
  // [NEEDS RULING: R1] — replaces "the Incarnates: Lumvaren (the Weaver...),
  // Nyrh Sarav (the Hollow Crown...), and Ytir itself (the Convergence...)".
},
```

(Keep the `first-collapse` infobox row `'Survivors': 'The Incarnates (fragments of Ytir)'` — replace with `'Survivors': 'Lumvaren and Neravmul — the true entity, split in two'`.)

---

## Rulings Index — bracketed judgment calls

### [NEEDS RULING: R1] — Incarnates: Ytir (Unified Face) + Reverb Echo (MC)
- **v1 version:** 4 incarnates — "Ytir (Unified Face)", Lumvaren, Neravmul, "The Reverb Echo (MC)".
- **v2.0 version:** 3 incarnates — "Ytir (The Singularity)" as the Incarnate from which all others derive, "Lumvaren (The Weaver)" as Neutral/weaver, "Neravmul (The Unmaker)" as Neutral/unmaker.
- **Canon (Sep 20 ruling):** Ytir is the BALANCE of Lumvaren and Neravmul together — not a third being above them. The players are the Echo Touched; there is no "Reverb Echo" incarnate.
- **Recommendation:** use the 2-incarnate list in Block A (default applied). If Adam rules otherwise, restore the v1 4-entry version.

### [NEEDS RULING: R2] — Timeline era names
- **v1 version:** 7 eras — "Ytir Uniformed", "The Singularity Splintered", "The Song Of Emotion", "The Schism", "The Corruption Conclave", "The Rise Of The Reverb", "The Age Of The Echoes".
- **v2.0 version:** 7 different eras — Singularity / Great Expansion / First Convergence / First Collapse / Paradox Emergence / Fragmentation / Current Era.
- **Recommendation:** keep v1's list (default applied); rename "Ytir Uniformed" / "The Singularity Splintered" once R1 resolves.

### [NEEDS RULING: R3] — Neravmul + Nyrh Sarav merged wiki entry
- **v1 version:** n/a (no wiki).
- **v2.0 version:** one page (id `neravmul`) titled "Nyrh Sarav, The Hollow Crown" — the paradox incarnate and the dread paradoxum merged into one being.
- **Canon:** Neravmul is the paradox incarnate (Lumvaren's exact reversal); Nyrh Sarav is Vara Shryn's paradoxum, "the Frozen Fear".
- **Recommendation:** split into two pages as in D3 (default applied).

### [NEEDS RULING: R4] — Dread / order line
- **v1 version:** n/a.
- **v2.0 version:** "When you run out of Dread, you've lost your grip on the part of Ytir that represents order."
- **Canon:** dread is weight/gravity — the moment is fleeting and may end, fear that protects or freezes. Order is chaos's antithesis (true unmaking, the void).
- **Recommendation:** replace with the D1c text (default applied).

### [NEEDS RULING: R5] — "Free will is an experiment" cosmology
- **v1 version:** n/a.
- **v2.0 version:** Ytir intentionally fractured reality to observe the fragments; "Your characters are that experiment."
- **Canon:** outer forces hijacked earlier iterations; the split into primes (expansion) and paradoxes (collapse) was defensive.
- **Recommendation:** quarantine the v2.0 version; use D1d text (default applied).

### [NEEDS RULING: R6] — v2.0 renamed prime epithets + 18 aspect names
- **v1 version:** Luminara "Connection's Constellation"; Vara Shryn "Fate's Ferryman"; Revyen "the Fractal Feather"; original aspect names/pronunciations.
- **v2.0 version:** generic English renames ("Mother of Hearts", "The Inevitable", "The Wildfire", "Chaos Unbound", etc.).
- **Canon:** v1 names/pronunciations and ruled epithets are canon.
- **Recommendation:** restore v1 names wholesale (done in Block A).

### [NEEDS RULING: R7] — Lumvaren as "neither Prime nor Paradoxum"
- **v1 version:** "Lumvaren" — Prime Incarnate, unified form of the Heart, Dread, and Chaos Primes.
- **v2.0 version:** "Lumvaren, The Weaver" — Neutral, the Incarnate of Heart only.
- **Canon:** Lumvaren is the prime incarnate.
- **Recommendation:** Prime Incarnate (done in Block A + D2).

### [NEEDS RULING: R8] — Stale Unifier / Sentinel / Catalyst class list
- **v1 version:** canon.ts `core_systems.classes` lists Unifier, Sentinel, Catalyst — an outdated class set.
- **v2.0 version:** the current six (Warden, Luminary, Carrion Knight, Adjudicator, Riftblade, Dreamstitcher).
- **Canon:** six classes are current.
- **Recommendation:** retain the v2.0 `core_systems` (done in Block A).

### [NEEDS RULING: R9] — Triumvirate caption
- **v1 + v2.0 version:** "The Triumvirate: Luminara (Heart), Vara Shryn (Dread), Lumvaren (Incarnate), and Revyen (Chaos)" — four beings in a triumvirate.
- **Recommendation:** "The Primes and the Prime Incarnate: Luminara (Heart), Vara Shryn (Dread), Revyen (Chaos) — and Lumvaren, the Prime Incarnate" (Block B2).

### [NEEDS RULING: R10] — 16 Ages (8–16)
- **v1 + v2.0 version:** identical 16-Age table; ages 1–7 canon, 8–16 never confirmed.
- **Recommendation:** keep all 16 visible for now (no code change), pending his ruling on whether ages 8–16 stand. Flag for the rulings sweep.

### [NEEDS RULING: R11] — Pronouns for Neravmul / Nyrh Sarav / Neyver
- **v1 version:** n/a.
- **v2.0 version:** they/them used for Nyrh Sarav.
- **Canon:** only Luminara's pronouns are ruled (lur/lurs).
- **Recommendation:** keep they/them in the wiki for Nyrh Sarav, avoid pronouns for Neravmul/Neyver, until he rules.

### [NEEDS RULING: R12] — Breaker / Weaver / Shade / Herald / Conduit class set
- **v1 version:** a standalone `classes.ts` with 5 classes (1 per emotion + herald + conduit) with full move lists.
- **v2.0 version:** absent — six-class system throughout.
- **Canon:** unruled; possibly a March-class concept.
- **Recommendation:** surface to Adam as an open question, not part of this port.

### [NEEDS RULING: R13] — v2.0's 28 realm locations
- **v1 version:** 18 locations in the six-region structure (in the wiki source).
- **v2.0 version:** 28 locations across the eight-region restructure.
- **Canon:** the six regions are tentative canon; the newer location names are unsourced but compatible.
- **Recommendation:** Block A restores the six-region structure; the 28 newer names are preserved as a marked salvage pool (below) for a future rulings sweep.

---

## [NEW IN ENHANCED — keep?] salvage pool

Material invented in the enhanced repo that is not canon *or* anti-canon. Worth keeping behind markers, not silently canonizing.

- **N1 — Tears / Tiers / Tierce narrative architecture.** The tagline "the tears / the tiers / the Tierce" is on both sites. The deeper Tierce-quest concept is tagged `[UNRULED]` on the launch page — keep the tag.
- **N2 — Ten v1-compatible adventures.** Written against v1 canon (correct epithets, 16-Age timeline). Compatible as-is.
- **N3 — Ancestries.** Aetherial, Forgeborn, Umbrakin, Luminari, Wraithkin — marked `[NEW]` on the launch page, no canon decision yet.
- **N4 — Wiki salvage prose.** The Radiant Veil (kept, D2), Hollow Crown / frozen breaths (kept, D3b), Citadel as memorial (kept, D3b), Nyrh Sarav's sympathetic witness framing (kept, D3b), Verdant Sentinels detail (kept, D2c). All re-attributed in Block D.
- **N5 — The 28 newer location names** (from R13). Unconfirmed as canon, not contradicted — future rulings material.

## Verification after pasting

1. Lore page: six tabs render; Echoes tab badges read "Heart Prime" / "Dread Prime" / "Chaos Prime" / "Heart Paradoxum" / "Dread Paradoxum" / "Chaos Paradoxum"; no `undefined` badge text.
2. GM Guide page: "Core Echoes" section renders without `[object Object]` (faction is now a string).
3. Wiki: Neravmul and Nyrh Sarav pages both appear; the citadel page links to Nyrh Sarav.
4. No `Amarnul` occurrences remain; paradox titles read "the Crystallized Heart" / "the Frozen Fear" / "the Unmade Order".
5. Search Figma Make for `The Weaver` / `The Unmaker` / `The Singularity` — any remaining hits are quarantined strings to revisit.

## What did not map cleanly (hand-off notes)

- **Faction shape mismatch:** v1's `faction` objects (`description`, `colors`, `symbol`) had no consumer in v2 — GMGuidePage would have crashed rendering them. The detail was dropped, not lost: the LorePage's `FACTION_DETAILS` carries the same lore inline. If Adam wants the detail centralized later, the LorePage is the file to restructure.
- **16-Age table (R10):** left entirely as-is; ages 8–16 are unconfirmed but removing them is a lore decision, not a port fix.
- **Riftblade "Weaver" subclass path** shares a name with the quarantined v2.0 Lumvaren title. Mechanical name, left alone — one for the rulings sweep.
- **The Reverb Echo (MC) / v1 16-Age timeline / "Ytir Uniformed"** all hinge on R1/R2 and were carried forward with bracket markers rather than being deleted.
