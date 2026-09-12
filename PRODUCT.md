# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Secondary-school students in the same course at Colegio San Agustín de Panamá, studying the "Sistema Músculo-Esquelético" unit. They use the tool interchangeably on phone and laptop (no single preferred device) to drill practice questions and label anatomical diagrams before their exam.

## Product Purpose

An infinite-practice quiz built directly from the student's own class notes and talleres, so the drills match exactly what the teacher will ask. Two practice modes — Teoría (mixed question types: multiple choice, matching, fill-in-the-blank, ordering, self-graded open response) and Identificación (labeling numbered points on real anatomical diagrams) — plus a 20-question randomized exam mode with scoring, filters by topic/type/diagram, and per-question history navigation.

## Positioning

Unlike a generic anatomy quiz app, every question and diagram is sourced from this specific teacher's own notes and talleres, so practice matches the real exam's content and format rather than approximating the subject in general.

## Operating Context

Used standalone by the student and classmates, on their own devices, in both short bursts (between classes, commuting) and longer focused study sessions before the exam. Hosted as a static page on GitHub Pages; the author (Antonio) pushes content and feature updates via git.

## Capabilities and Constraints

- Single static `index.html` (vanilla HTML/CSS/JS), no backend, no accounts.
- All progress/stats live in-memory per browser tab; not synced across devices or shared among classmates.
- Content (questions, diagrams, topics) is expected to keep growing over time, including for future exams/subjects beyond the musculoskeletal system — the structure should stay easy to extend without breaking existing practice state or filters.
- Deployed via GitHub Pages from the `main` branch.

## Brand Commitments

- Product name: "Sistema Músculo-Esquelético — Práctica Infinita".
- No institutional branding on the page (as of 2026-09): the earlier "Colegio San Agustín de Panamá" credit (footer + hero) was removed at the user's explicit request. Do not reintroduce it without being asked.
- Visual identity (as of 2026-09): a dark "radiograph / scan room" system — near-black film-blue ground, a single cyan-phosphor accent, condensed display type, mono data labels. Replaces the earlier cream/green heraldic-seal identity at the user's explicit request; see DESIGN.md.
- A full-viewport landing "plate" opens the page (headline, real question-bank stats, CTA) and anchor-scrolls into the practice tool below; it must not gate or hide the practice content behind a load/click step — everything stays on one page (zero-friction principle still holds).
- Question wording and diagram content are transcribed from the student's real class materials; never invent or alter their substance.

## Evidence on Hand

- Real exam-style question bank already authored (selección, pareo, fill, order, desarrollo) covering multiple musculoskeletal topics.
- Real anatomical diagram images in `assets/` with numbered points already mapped to structure names.
- No analytics or user testimonials exist; none should be fabricated.

## Product Principles

1. Practice content must mirror the teacher's real material and exam format — never generic filler.
2. Equally usable on phone and laptop; no device is the "primary" target.
3. Zero friction: no login, no setup, open the page and start drilling immediately.
4. Content is living — adding new questions, diagrams, or entire topics later must not require restructuring what already works.
5. Shared with classmates, not just the original author — clarity and robustness matter beyond one person's own habits.
