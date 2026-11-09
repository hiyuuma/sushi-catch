# お寿司キャッチ (Sushi Catch) — SPEC v1

A single-file browser game: `index.html` only (inline CSS + JS, no external assets, no build step). Japanese UI. Must work on desktop (mouse) and smartphone (touch), responsive, max-width ~480px game column centered.

## Concept
Sushi plates flow on 3 horizontal conveyor lanes. An order ticket shows what the customer wants. Tap/click ONLY the sushi on the ticket before it slides away. 60 seconds per run.

## Demand-research findings baked in (from X research, 2026-11-09)
1. Score in yen (円) like 寿司打: each sushi has a price; earnings are comparable and braggable. Show total yen prominently.
2. Every run ends on a shareable RESULT CARD: total yen, plates served, miss count, max combo, and a rank title. Include a "結果をXでポスト" button (opens https://twitter.com/intent/tweet with prefilled result text) and a "結果をコピー" button.
3. Misses are part of the story: always show miss count during play and on the result card.
4. Mistakes must be readable, never feel unfair: speed ramps gradually and visibly; a missed/wrong plate shows a clear animation (plate slides off / breaks) plus a customer reaction emoji (😱/😖) briefly.
5. Punish with the bill, not with instant death: wrong tap = lose that item's price in yen (total never below 0), combo resets, miss +1. The run always continues.
6. Funny distractors with names: items that never appear on tickets, e.g. フライドコーン, わさび山盛り, プリン — grabbing one counts as a mistake.
7. First 10 seconds are the game: one big スタート button, one-line how-to, no menus before play.
8. Two modes with separate high scores: ゆったり (normal speed) / ランチラッシュ (1.4x speed, 1.5x prices). Mode chosen on the start screen; high score stored per mode in localStorage.

## Gameplay details
- Lanes: 3, sushi move leftward (or rightward — pick one, be consistent), spawn at readable intervals.
- Ticket: shows 2–3 target items with remaining counts (e.g. まぐろ ×2, えび ×1). Completing a ticket: bonus +¥300, "注文達成!" flash, next ticket appears. Tickets get slightly harder over time (more items / rarer items).
- Items (name, emoji, price): まぐろ 🍣 ¥300, サーモン 🍣 ¥280, えび 🍤 ¥260, たまご 🍣 ¥200, いか 🦑 ¥240, うに ¥600 (rare), 大トロ ¥800 (rare), いくら ¥450. Use emoji + name label under each plate so items are distinguishable (don't rely on identical 🍣 emoji alone — vary emoji where possible: 🍣🍤🦑🥚 etc. and always show the name text).
- Distractors (never on tickets): フライドコーン 🌽, わさび山盛り 🟢, プリン 🍮, からあげ 🍗.
- Correct tap: plate pops with +¥price floating text, served count +1, combo +1 (combo multiplier: every 10 combo adds +10% to price, cap +50% — keep simple and show current multiplier).
- Combo/miss/score HUD always visible: 残り時間, 合計円, コンボ, ミス数.
- Speed: base speed ramps +~35% across the 60 s; spawn interval shrinks slightly. In ランチラッシュ multiply speed by 1.4.
- End: time up → result card overlay (per findings #2) + もう一度 button + mode high score saved (localStorage keys per mode).
- Start screen: title お寿司キャッチ, one-line rules, mode select (two buttons), high scores per mode, big スタート button.
- Visual style: warm sushi-restaurant look (dark wood/red accents or clean light theme — pick one and keep it coherent), plates as circles with colored rims, lanes as conveyor belts with subtle animation. No external images/fonts.
- Sound: optional tiny WebAudio beeps for correct/wrong/ticket-complete; must not crash if audio unavailable; add a mute toggle. (Keep very small.)
- Code quality: vanilla JS, requestAnimationFrame loop, no libraries. Handle visibility of tap targets ≥44px. Prevent double-firing on touch (use pointerdown).
- Language: all UI text in Japanese.

## Deliverable
Create ONLY `index.html` in this directory implementing everything above. Do not modify SPEC.md or recon*.md.
