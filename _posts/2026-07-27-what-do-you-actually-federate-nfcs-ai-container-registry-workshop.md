---
title: "What Do You Actually Federate? Notes from the 4th NFCS AI Container Registry Workshop"
collection: posts
permalink: /year-archive/what-do-you-actually-federate-nfcs-ai-container-registry-workshop
excerpt: "Notes from the 4th NFCS AI Container Registry Workshop, on the unresolved question of what a federated AI container registry should actually distribute, and who it should serve."
date: 2026-07-27
venue: "Technical Blog"
---

# What Do You Actually Federate? Notes from the 4th NFCS AI Container Registry Workshop

Notes from the 4th NFCS AI Container Registry Workshop, which circled a deceptively simple question all day: what should a federated AI container registry actually distribute, and who should it serve? The event surfaced governance and architectural disagreements more than technical implementation detail.

## The Core Problem

Christian Kniep (QNIB Solutions) reframed container registries as no longer simple artifact stores. Via OCI/ORAS standards, a registry can now distribute almost anything — code, model weights, configurations, prompts — which makes "what to federate" a genuinely hard question. End users, resource providers, and software managers have conflicting priorities, and every choice about the unit of versioning directly expands or contracts the scope of governance.

## Human Factors Matter

Rich Gilham's framing: "HPC is the means, not the end." Containers solve real reproducibility problems, but at a real cost — teams need dedicated expertise to manage image bloat, GPU-driver coupling, and security constraints, and containerization does not automatically guarantee reproducibility no matter how convenient it feels.

## A Metadata-First Approach

Marc Dillon (AMD) offered the most concrete alternative: federate metadata and validation pipelines, not container blobs. A user asks for an application ("I need a chat model"), and an intelligent resolver selects the optimal implementation across whatever hardware and software stack is available — AMD, NVIDIA, Intel — so "the correct, optimised container appears." This moves the burden of hardware optimization off researchers and onto platform engineers.

## Governance as Foundation

Adam Huffman (Oxford/EESSI) reframed the whole effort as fundamentally a governance challenge, tracing EasyBuild's evolution from a single-maintainer project to one with formal steering committees, explicit lifecycle policies, and structured decision-making — a proven model for sustainability.

## MVP Consensus

Participants converged on a few concrete principles:

- Federate validated metadata descriptions, not multi-gigabyte container images
- Use OCI and ORAS standards rather than building new infrastructure
- Enforce profile validation and linting rather than relying on convention
- Put everything — recipes, metadata, policies — into version control and CI/CD
- Focus on small, real use cases with measurable value

## Cross-Cutting Insights

Recurring tensions ran through the day: users want applications, not infrastructure; governance and funding decisions have to precede technical ones; metadata and recipes matter more than the built artifacts themselves; and treating build/teardown as versioned, first-class operations is what actually unlocks reproducibility at scale.

## Takeaways Beyond HPC

Separate environment recipes from built images. Treat deployment as a versioned CI step. Move governance into the pull request pipeline instead of a separate process. Make vulnerability visibility explicit rather than assumed. EasyBuild's reproducibility model is worth studying even outside HPC contexts.

Read the full article on Medium:
[What Do You Actually Federate? Notes from the 4th NFCS AI Container Registry Workshop](https://medium.com/@huishi1885/what-do-you-actually-federate-notes-from-the-4th-nfcs-ai-container-registry-workshop-ce21bd215b2e)
