# App Flow Overview

This document explains what the current application page-planning phase is trying to achieve.

## Why this phase exists

The app repo is still close to a starter shell, while the planning repo now has enough architecture and operations direction to begin specifying real screens.

The goal of this phase is to define the application one screen at a time so app development can move forward in parallel with node development.

In practice, that means each page file should answer three questions clearly:

1. What does the user see?
2. What can the user do?
3. What does the app need from the node or local database to support this screen?

## What this phase should produce

This phase should produce a documentation package that lets someone build the first real Flutter screens without waiting for the full networking stack to be complete.

That package should:

- Define the first-run experience from app open to entry into the product
- Define the main feed and its operational states
- Make architecture constraints visible to screen implementers
- Separate what can be mocked locally from what requires real node behavior

## Why onboarding comes first

The first app experience needs to do more than copy a web signup screen.

Social Production depends on local-first behavior, identity, and a node model. That means onboarding has to cover more than username and password. It has to explain enough of the system for the user to start safely and understand what the app is doing.

The onboarding pack in this folder focuses on:

- First open and orientation
- Identity and key setup
- Basic node setup
- Profile setup
- Optional feed personalization
- Sync and ready state

## Why the main feed comes next

The main feed is the first everyday working screen for most users. It is where discovery, discussion, projects, updates, and next actions meet.

The main feed pack in this folder focuses on:

- The canonical logged-in feed
- First-use feed behavior
- Personalized and local discovery variants
- Empty, syncing, offline, and recovery states
- Primary actions such as creating content, joining projects, and opening detail screens

## Parallel work rule

The page packs are written so Flutter work and node work can proceed in parallel.

Examples:

- A screen can be built with mocked local repositories before gRPC contracts exist
- Sync indicators can be implemented before final networking logic exists
- Feed cards can be built against a stable view model while backend data pipelines are still changing

## Handoff standard

Each page should be detailed enough that a developer can answer the following without guessing:

- What is the layout hierarchy?
- What are the primary and secondary actions?
- What states must exist beyond the happy path?
- What is the minimum data needed to render the screen?
- What is blocked by unresolved product decisions?

## Relationship to other planning documents

This application planning section does not replace the architecture or operations documents.

Instead, it translates them into screens.

- Architecture answers how the system behaves technically
- Operations answers how the platform behaves socially and organizationally
- Application planning answers how that behavior appears in the product