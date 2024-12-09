# Hierarchical Pathfinding

Hierarchical pathfinding is an advanced method used to optimize pathfinding in large-scale maps by abstracting the map into manageable chunks and connecting them through entrance nodes.

## Why Use Hierarchical Pathfinding?

Pathfinding algorithms like **A*** or **Flow Fields** are computationally intensive, especially when applied to large maps or numerous units. Traditional pathfinding methods calculate routes across the entire map, which significantly increases processing time and reduces efficiency.

Hierarchical pathfinding addresses this issue by:
- Dividing the map into **chunks**.
- Connecting these chunks using **entrance nodes**.
- Forming a graph of walkable paths across chunks.

This approach reduces the complexity of pathfinding computations and is especially useful for:
- Large maps with numerous obstacles.
- Scenarios involving many units needing simultaneous pathfinding.

---

## Demo

Below is a demo of a single unit using Hierarchical Pathfinding with **A*** to pathfind to random goal nodes across the map.

[Demo Video](https://github.com/user-attachments/assets/c3a58a4a-011b-4def-a2eb-db3483e7239c)

---

## Explanation

### Initial Map

The starting map consists of a grid where each **grey tile** represents a node.

![Initial Map](https://github.com/user-attachments/assets/99647fe5-de1d-4abc-8256-dc7754f47c55)

### Splitting the Map into Chunks

1. **Chunk Creation**: Randomly select a tile and initialize a `Chunk` object if one does not already exist for that area.
2. **Flood Fill**: Iterate through all tiles in the chunk and perform a Flood Fill operation. For each Flood Fill, create an `Abstraction` object. This step accounts for gaps within a chunk that might split it into disconnected regions.

The image on the left shows the map divided into chunks (white borders). The image on the right displays the **abstractions** within each chunk, represented by different colors.

<p float="left">
  <img src="https://github.com/user-attachments/assets/38a7d856-5b5f-42ec-b2b8-a86d814108c9" width="300" />
  <img src="https://github.com/user-attachments/assets/309ca988-ddbf-46dd-b608-9d2693e2b5a4" width="300" />
</p>

### Connecting Abstractions to Form Regions

1. Combine abstractions with a single connecting node to form `Region` objects.
2. Regions allow for easier debugging and help track path existence.

![Regions](https://github.com/user-attachments/assets/7d30e75a-b40d-48cf-a17b-2e25f413f134)

### Creating Inter-Chunk Connections

1. Place entrances at regular intervals. For example, place one entrance at the center of a side if its length exceeds a threshold.
2. Connect adjacent entrances to form inter-chunk connections.

<p float="left">
  <img src="https://github.com/user-attachments/assets/27f90a87-c854-4fa8-b239-90cdd70c5730" width="300" />
  <img src="https://github.com/user-attachments/assets/ce8dd803-e317-4642-b734-496c8f7714af" width="300" />
</p>

### Finalized Graph

After connecting all abstractions and inter-chunk nodes, the map forms a complete graph of walkable paths. Each abstraction within a chunk is linked to its neighbors, ensuring reachability.

![Final Graph](https://github.com/user-attachments/assets/c1ae6081-cf7c-46f5-a74b-1f99003b7981)

---

## Example Pathfinding

When pathfinding, the start and end nodes are converted into temporary graph nodes and connected to the overall structure. An algorithm such as **A*** or **Flow Field** can then determine the path. 

- **Green square**: Destination
- **Red square**: Start point
- **Green lines**: Calculated path

![Pathfinding Example](https://github.com/user-attachments/assets/75235b05-3e66-49e4-a42e-b6bcd3244c89)

---

## How to Use

1. Implement map splitting and chunking as described above.
2. Generate abstraction nodes within chunks and connect them to form a graph.
3. Use a pathfinding algorithm on the graph to compute paths.

---

## Notes

- Adjust entrance placement to balance graph complexity and computational efficiency.
- Regions are optional but helpful for debugging and visualization.
- Larger maps may benefit more from hierarchical pathfinding compared to small maps.

---
