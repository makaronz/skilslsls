# Architectural Generation

Procedurally generate buildings, dungeons, and interior layouts for games and simulations.

---

## Dungeon Generation

### Binary Space Partitioning (BSP)

Classic algorithm for room-based dungeons:

**Algorithm:**
1. Start with full dungeon area as root rectangle
2. Split recursively (alternate horizontal/vertical)
3. Each leaf becomes a potential room
4. Create rooms within leaf boundaries (with padding)
5. Connect sibling rooms with corridors
6. Traverse tree to connect all regions

**Parameters:**
| Parameter | Effect | Range |
|-----------|--------|-------|
| Min room size | Smallest possible room | 5-15 tiles |
| Max depth | Number of splits | 3-6 |
| Split ratio | Where to split (random within range) | 0.3-0.7 |
| Room padding | Space between room and partition edge | 1-3 tiles |
| Corridor width | Hallway size | 1-3 tiles |

### Cellular Automata (Cave Generation)

**Algorithm:**
1. Fill grid randomly (45-55% walls)
2. For each cell, count wall neighbors in 3×3 area
3. If wall neighbors >= 5: become wall. Otherwise: become floor
4. Repeat 4-6 iterations
5. Flood fill to find connected regions
6. Connect isolated regions with tunnels or remove small ones

### Wave Function Collapse (WFC)

Constraint-based generation from example tiles:

**How It Works:**
1. Define tile set with adjacency rules (which tiles can neighbor which)
2. Initialize grid — each cell can be any tile
3. Find cell with lowest entropy (fewest possibilities)
4. Collapse that cell to one possibility (weighted random)
5. Propagate constraints to neighbors
6. Repeat until all cells collapsed or contradiction

**Best For:**
- Tile-based maps with complex patterns
- Interior layouts
- City blocks
- Puzzle rooms

---

## Building Generation

### Facade Generation

**Grammar-Based Approach:**

```
Building → Base + Body + Roof
Body → Floor × N
Floor → [Window, Wall, Window, Wall, Door?, ...]
Window → Frame + Glass + Sill + (Shutters?)
```

### Modular Building System

| Module Type | Size | Variations |
|-------------|------|-----------|
| Corner | 1×1×1 | Ground, middle, top |
| Wall | Variable×1×1 | Window, blind, door, balcony |
| Roof | Variable×variable | Flat, pitched, dome |
| Trim | Edge pieces | Cornice, molding |
| Interior | Room modules | Kitchen, bedroom, hallway |

### Generation Pipeline
1. Define building footprint (rectangle, L-shape, U-shape)
2. Determine floor count based on zoning/style
3. Generate structural grid (columns, walls)
4. Place facade modules following style rules
5. Generate interior layout (room subdivision)
6. Add details (windows, doors, decorations)
7. Apply material variation

---

## City/Settlement Layout

### Road Network Generation

| Method | Pattern | Best For |
|--------|---------|----------|
| Grid | Regular blocks | Modern cities |
| Radial | Circles from center | Historic cities |
| Organic | Terrain-following | Villages, medieval |
| L-system | Rule-based branching | Road hierarchies |
| Voronoi | Cell-based districts | Fantasy, alien |

### Lot Subdivision
1. Define city blocks from road network
2. Subdivide blocks into building lots
3. Assign lot types (residential, commercial, park)
4. Generate buildings sized to lots
5. Add street furniture, vegetation, details

---

## Interior Generation

### Room Placement

| Algorithm | Description | Control Level |
|-----------|-------------|-------------|
| Grid-based | Rooms align to grid | High, predictable |
| Treemap | Recursive subdivision | Natural, space-filling |
| Agent-based | Rooms "grow" from seeds | Organic, unpredictable |
| Template + variation | Pre-made layouts with random details | Very high |

### Furniture Placement Rules
- Beds against walls, not blocking doors
- Tables in room centers or against walls
- Chairs around tables or at desks
- Clearance for doorways and walkways (minimum 1m)
- Functional grouping (kitchen items together)
- Style consistency within room

---

## Best Practices

- Combine algorithms: WFC for details within BSP-generated rooms
- Pre-validate: Check connectivity, ensure all rooms reachable
- Seed-based: Store generation seed for reproducibility
- Progressive detail: Generate structure first, then details, then decoration
- Style parameters: Encapsulate architectural style in parameter sets
- Performance: Generate in chunks, stream distant areas at lower detail
