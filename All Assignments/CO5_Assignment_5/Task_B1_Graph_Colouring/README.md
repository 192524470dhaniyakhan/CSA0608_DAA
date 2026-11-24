
# CO5 Assignment 5
# TASK B1 - Instrumented Graph Colouring
# Backtracking with Search Instrumentation and Ordering Comparison

class GraphColouring:

    def __init__(self, graph, k, strategy="input"):
        self.graph = graph
        self.k = k
        self.strategy = strategy

        self.vertices = list(graph.keys())
        self.colouring = {v: 0 for v in self.vertices}

        self.stats = {
            "search_nodes": 0,
            "candidate_assignments": 0,
            "rejected_branches": 0,
            "backtracks": 0,
            "max_depth": 0
        }

    # Check whether a colour can be assigned safely
    def is_safe(self, vertex, colour):

        for neighbour in self.graph[vertex]:

            if self.colouring[neighbour] == colour:
                return False

        return True

    # Select the next vertex according to the strategy
    def select_vertex(self, unassigned):

        if self.strategy == "input":
            return unassigned[0]

        elif self.strategy == "degree":
            # Select the unassigned vertex with the
            # highest total degree.
            # Ties are resolved using input order.
            return max(
                unassigned,
                key=lambda v: len(self.graph[v])
            )

        return unassigned[0]

    # Recursive backtracking algorithm
    def backtrack(self, unassigned, depth):

        self.stats["search_nodes"] += 1

        self.stats["max_depth"] = max(
            self.stats["max_depth"], depth
        )

        # All vertices are successfully coloured
        if not unassigned:
            return True

        vertex = self.select_vertex(unassigned)

        remaining = [
            v for v in unassigned if v != vertex
        ]

        # Try every available colour
        for colour in range(1, self.k + 1):

            self.stats["candidate_assignments"] += 1

            if self.is_safe(vertex, colour):

                self.colouring[vertex] = colour

                if self.backtrack(remaining, depth + 1):
                    return True

                # Undo the assignment
                self.colouring[vertex] = 0

                self.stats["backtracks"] += 1

            else:

                self.stats["rejected_branches"] += 1

        return False

    # Run the algorithm
    def solve(self):

        if self.k < 0:
            raise ValueError("Number of colours cannot be negative.")

        # Reset state and statistics
        self.colouring = {
            v: 0 for v in self.vertices
        }

        for key in self.stats:
            self.stats[key] = 0

        result = self.backtrack(
            self.vertices.copy(), 0
        )

        if not result:
            self.colouring = {
                v: 0 for v in self.vertices
            }

        return result, self.colouring, self.stats


# Display the result of one experiment
def run_experiment(name, graph, k, strategy):

    print("\n" + "=" * 60)
    print(name)
    print("Strategy:", strategy)
    print("Number of colours:", k)

    solver = GraphColouring(graph, k, strategy)

    result, colouring, stats = solver.solve()

    if result:
        print("Result: VALID COLOURING FOUND")
        print("Final Colouring:", colouring)
    else:
        print("Result: NO VALID COLOURING EXISTS")

    print("Search Nodes Visited:",
          stats["search_nodes"])

    print("Candidate Assignments:",
          stats["candidate_assignments"])

    print("Rejected Branches:",
          stats["rejected_branches"])

    print("Number of Backtracks:",
          stats["backtracks"])

    print("Maximum Search Depth:",
          stats["max_depth"])

    return result, stats


# Compare input-order and degree-based ordering
def compare_strategies(name, graph, k):

    print("\n\n######## STRATEGY COMPARISON ########")
    print("Graph:", name)

    _, input_stats = run_experiment(
        name, graph, k, "input"
    )

    _, degree_stats = run_experiment(
        name, graph, k, "degree"
    )

    print("\nPERFORMANCE COMPARISON")

    print("{:<28} {:<15} {:<15}".format(
        "Measure", "Input Order", "Degree Order"
    ))

    print("-" * 58)

    for measure in input_stats:

        print("{:<28} {:<15} {:<15}".format(
            measure,
            input_stats[measure],
            degree_stats[measure]
        ))


# --------------------------------------------------
# TEST CASE 1: Colourable Graph
# --------------------------------------------------

graph1 = {
    "A": ["B", "C"],
    "B": ["A", "C", "D"],
    "C": ["A", "B", "D"],
    "D": ["B", "C"]
}


# --------------------------------------------------
# TEST CASE 2: Not Colourable with Two Colours
# --------------------------------------------------

graph2 = {
    "A": ["B", "C"],
    "B": ["A", "C"],
    "C": ["A", "B"]
}


# --------------------------------------------------
# TEST CASE 3: Boundary Case - Single Vertex
# --------------------------------------------------

graph3 = {
    "A": []
}


# --------------------------------------------------
# EXECUTION
# --------------------------------------------------

if __name__ == "__main__":

    print("CO5 ASSIGNMENT 5 - TASK B1")
    print("INSTRUMENTED GRAPH COLOURING")

    # Validation tests using input-order strategy
    run_experiment(
        "TEST 1 - Colourable Graph",
        graph1, 3, "input"
    )

    run_experiment(
        "TEST 2 - Triangle with Two Colours",
        graph2, 2, "input"
    )

    run_experiment(
        "TEST 3 - Single Vertex Boundary Case",
        graph3, 1, "input"
    )

    # Compare both ordering strategies
    compare_strategies(
        "Colourable Graph", graph1, 3
    )

    compare_strategies(
        "Triangle Graph", graph2, 2
    )

    compare_strategies(
        "Boundary Graph", graph3, 1
    )

