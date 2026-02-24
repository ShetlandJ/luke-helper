# Stock Redistribution Planner

A tool built for Luke to plan fair redistribution of stock (Type 1, 2 & 3) across entity IDs.

## Problem

Given a spreadsheet of entity IDs with counts of Type 1, 2, and 3 stock, calculate what transfers are needed so each entity has a fair share. For example, if the average Type 1 count is 4.3, most entities should end up with 4 and some with 5.

The type columns represent physical stock. The tool calculates the specific transfers (move X units of Type N from Entity A to Entity B) required to achieve fair distribution.

Note: Details are deliberately vague due to commercial sensitivities.

## Architecture

Single-file web app (`index.html`) — no build step, no dependencies beyond SheetJS (loaded via CDN) for spreadsheet parsing.

### Key concepts

- **Entity ID**: Row identifier from the uploaded spreadsheet
- **Types 1/2/3**: Stock categories to be redistributed (column names come from the spreadsheet header)
- **Target**: The fair allocation for each entity (floor/ceil of the average)
- **Transfers**: Specific moves of stock between entities to reach targets
- **Locking**: Users can lock an entity to preserve its current stock; remaining stock is redistributed among unlocked entities

### Flow

1. User uploads CSV/XLSX with columns: Entity ID, Type 1, Type 2, Type 3
2. App calculates fair targets per type (total / entity count, distributed as floor/ceil)
3. Greedy algorithm matches surplus entities to deficit entities to produce a transfer manifest
4. Users can manually edit targets, lock entities, and export results to XLSX

## Tech

- Vanilla HTML/CSS/JS, single file
- SheetJS (`xlsx.full.min.js`) via CDN for file import/export
- Fonts: Instrument Sans (body), DM Mono (data)
- Dark theme with gold accent
