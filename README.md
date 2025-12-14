# Priority-Pathfinding-with-Static-Threat-Mapping
// Pathfinder.cs

using System.Collections.Generic;
using System.Linq;

public class Pathfinder 
{
    // A list of coordinates that should be avoided entirely.
    private static readonly List<Vector2> StaticDangerZones = new List<Vector2> 
    {
        new Vector2(10, 50), 
        new Vector2(90, 10), 
        new Vector2(50, 50) 
    };

    /**
     * Calculates a path from start to end, strictly avoiding known static danger zones.
     * @param start The starting coordinate.
     * @param end The target coordinate.
     * @returns A list of coordinates forming the safe path.
     */
    public List<Vector2> FindSafePath(Vector2 start, Vector2 end) 
    {
        // --- Dummy implementation for pathfinding ---
        List<Vector2> path = new List<Vector2> { start };
        Vector2 current = start;

        // Simple step logic (In a real game, this would be A* or Dijkstra's)
        while (current != end) 
        {
            // Simple check: If the next point is a danger zone, find an alternative.
            Vector2 nextStep = CalculateNextOptimalStep(current, end); 

            if (StaticDangerZones.Contains(nextStep)) 
            {
                // In a real scenario, this would trigger a complex bypass.
                // Here, we just return an error path to signify blockage.
                return new List<Vector2> { start, new Vector2(-1, -1) }; 
            }
            
            path.Add(nextStep);
            current = nextStep;

            // Prevents infinite loop for this simple example
            if (path.Count > 10) break;
        }

        return path;
    }

    // Placeholder for actual pathfinding step calculation
    private Vector2 CalculateNextOptimalStep(Vector2 current, Vector2 end) 
    {
        // Logic to move closer to 'end'
        if (current.X < end.X) current.X++;
        else if (current.X > end.X) current.X--;

        if (current.Y < end.Y) current.Y++;
        else if (current.Y > end.Y) current.Y--;
        
        return current;
    }
}
