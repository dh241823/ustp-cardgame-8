# Planning Guide

A memory card matching game where players flip cards to find matching pairs, testing their memory and concentration skills.

**Experience Qualities**:
1. **Playful** - Bright, inviting visuals with satisfying card-flip animations that make each interaction feel rewarding
2. **Focused** - Clean, distraction-free interface that keeps attention on the game board and memory challenge
3. **Responsive** - Immediate feedback for every action with smooth transitions that feel natural and polished

**Complexity Level**: Light Application (multiple features with basic state)
  - Includes game state management, timer, move counter, and restart functionality with persistent high scores

## Essential Features

### Card Grid Display
- **Functionality**: Display a 4x4 grid of face-down cards with icons
- **Purpose**: Provides the core game board interface
- **Trigger**: Game loads or restarts
- **Progression**: App loads → Cards shuffle randomly → Grid displays face-down → Ready for interaction
- **Success criteria**: 16 cards appear in grid, all face-down, randomly shuffled each game

### Card Flipping Mechanism
- **Functionality**: Click to reveal card, compare pairs, handle matches/mismatches
- **Purpose**: Core gameplay interaction
- **Trigger**: User clicks on a face-down card
- **Progression**: Click card → Card flips with animation → Icon reveals → If second card, compare → Match: cards stay revealed → Mismatch: both flip back after delay → Continue until all matched
- **Success criteria**: Cards flip smoothly, pairs lock when matched, mismatches flip back after 1 second, maximum 2 cards flipped at once

### Game Statistics
- **Functionality**: Track moves, time elapsed, and display current/best scores
- **Purpose**: Adds challenge and replayability through performance tracking
- **Trigger**: Game starts on first card flip
- **Progression**: First flip → Timer starts → Each pair attempt increments move counter → Game completes → Compare to best score → Update if improved
- **Success criteria**: Timer counts accurately, moves increment correctly, best score persists between sessions

### Win Condition & Restart
- **Functionality**: Detect game completion, show celebration, allow restart
- **Purpose**: Provides closure and encourages replay
- **Trigger**: All 8 pairs are matched
- **Progression**: Final match → Brief celebration animation → Display final stats → Show restart button → Click restart → New game begins
- **Success criteria**: Win state triggers reliably, stats display accurately, restart shuffles new game

## Edge Case Handling
- **Rapid Clicking**: Prevent more than 2 cards from being flipped simultaneously by disabling clicks during comparison
- **Double-Click Same Card**: Ignore clicks on already-revealed or currently-flipped cards
- **Mid-Game Restart**: Allow restart button at any time to reset board, timer, and moves
- **No Best Score**: Display encouraging message on first game completion before best score is set

## Design Direction
The design should feel playful and engaging like a classic board game brought to life digitally, with satisfying tactile feedback through card-flip animations and a clean, colorful interface that feels inviting rather than competitive or intense.

## Color Selection
Triadic color scheme with vibrant, friendly colors that create visual interest without overwhelming the game board.

- **Primary Color**: Deep Purple (oklch(0.45 0.15 300)) - Main background and primary UI elements, communicates focus and sophistication
- **Secondary Colors**: 
  - Teal (oklch(0.60 0.12 200)) - Card backs and secondary buttons, provides cool contrast
  - Coral (oklch(0.70 0.15 40)) - Accent highlights and matched cards, adds warmth
- **Accent Color**: Bright Yellow (oklch(0.85 0.15 90)) - Call-to-action buttons and success states, draws attention energetically
- **Foreground/Background Pairings**:
  - Background (Deep Purple oklch(0.45 0.15 300)): White text (oklch(0.98 0 0)) - Ratio 8.2:1 ✓
  - Card (White oklch(0.98 0 0)): Dark Gray text (oklch(0.25 0 0)) - Ratio 13.1:1 ✓
  - Primary (Teal oklch(0.60 0.12 200)): White text (oklch(0.98 0 0)) - Ratio 4.8:1 ✓
  - Accent (Bright Yellow oklch(0.85 0.15 90)): Dark text (oklch(0.25 0 0)) - Ratio 11.5:1 ✓
  - Muted (Light Purple oklch(0.85 0.05 300)): Medium Gray text (oklch(0.45 0 0)) - Ratio 5.2:1 ✓

## Font Selection
Typography should feel friendly and modern with excellent readability, using a geometric sans-serif that reinforces the playful, game-like atmosphere.

- **Typographic Hierarchy**: 
  - H1 (Game Title): Poppins Bold/36px/tight letter spacing - Playful and bold
  - H2 (Stats Labels): Poppins SemiBold/18px/normal spacing - Clear hierarchy
  - Body (Stats Values): Poppins Regular/16px/relaxed spacing - Easy scanning
  - Button Text: Poppins Medium/14px/wide spacing - Strong emphasis

## Animations
Animations should feel snappy and satisfying like handling physical cards, with quick, decisive movements that provide clear feedback without slowing down gameplay pace.

- **Purposeful Meaning**: Card flips communicate discovery and memory testing, matched pairs celebrate success with a subtle scale bounce, mismatches communicate failure with a gentle shake
- **Hierarchy of Movement**: Card flips are primary (3D rotation), matches get secondary celebration (scale + fade), game start gets tertiary shuffle effect

## Component Selection
- **Components**: 
  - Card: Custom component with 3D flip animation using framer-motion
  - Button: Shadcn Button for restart/new game actions with default variant
  - Card (container): Shadcn Card for stats panel with subtle shadow
  - Badge: Shadcn Badge for displaying move count and timer
- **Customizations**: 
  - Custom MemoryCard component with flip state and 3D transform
  - Custom GameBoard grid layout with responsive sizing
  - Custom icon set (8 unique phosphor icons for card faces)
- **States**: 
  - Cards: face-down (teal back), face-up (white with icon), matched (coral highlight), disabled (reduced opacity)
  - Buttons: default (yellow accent), hover (scale 1.05), active (scale 0.95), disabled (muted)
- **Icon Selection**: 
  - Card faces: Heart, Star, Moon, Sun, Cloud, Lightning, Fire, Drop (playful, recognizable shapes)
  - UI: ArrowClockwise for restart, Trophy for best score
- **Spacing**: 
  - Grid gap: gap-4 (1rem) between cards
  - Stats panel: p-6 padding, mb-8 margin below
  - Card padding: Minimal, icons centered
- **Mobile**: 
  - Grid scales from 4x4 on desktop to 4x4 on mobile with smaller card sizes
  - Stats panel stacks vertically on mobile, horizontal on desktop
  - Touch targets minimum 44px, cards scale appropriately
  - Font sizes reduce slightly on mobile (H1: 28px, Body: 14px)
