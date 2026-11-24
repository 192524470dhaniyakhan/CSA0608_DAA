
# CO5 Assignment 5
# TASK B3 - Exact vs Approximate Set Cover
# Emergency Service Centre Selection

from itertools import combinations


# --------------------------------------------------
# EXACT SET COVER ALGORITHM
# --------------------------------------------------

def exact_set_cover(zones, centres):

    centre_names = list(centres.keys())

    combinations_checked = 0

    # Check combinations in increasing order of size
    for size in range(1, len(centre_names) + 1):

        for combination in combinations(centre_names, size):

            combinations_checked += 1

            covered = set()

            for centre in combination:
                covered.update(centres[centre])

            if zones.issubset(covered):

                return {
                    "solution": list(combination),
                    "solution_size": size,
                    "combinations_checked": combinations_checked
                }

    return {
        "solution": None,
        "solution_size": None,
        "combinations_checked": combinations_checked
    }


# --------------------------------------------------
# GREEDY SET COVER ALGORITHM
# --------------------------------------------------

def greedy_set_cover(zones, centres):

    uncovered = set(zones)

    selected = []

    selections = 0
    candidate_evaluations = 0

    while uncovered:

        best_centre = None
        maximum_coverage = 0

        # Examine every unselected centre
        for centre, covered_zones in centres.items():

            if centre in selected:
                continue

            candidate_evaluations += 1

            new_coverage = len(
                uncovered.intersection(covered_zones)
            )

            if new_coverage > maximum_coverage:

                maximum_coverage = new_coverage
                best_centre = centre

        # No centre can cover the remaining zones
        if best_centre is None:
            return {
                "solution": None,
                "solution_size": None,
                "selections": selections,
                "candidate_evaluations": candidate_evaluations,
                "trace": []
            }

        # Select the best centre
        selected.append(best_centre)
        selections += 1

        newly_covered = uncovered.intersection(
            centres[best_centre]
        )

        # Update uncovered zones
        uncovered.difference_update(
            centres[best_centre]
        )

        print(
            "Selected:", best_centre,
            "| Newly covered:", sorted(newly_covered),
            "| Remaining:", sorted(uncovered)
        )

    return {
        "solution": selected,
        "solution_size": len(selected),
        "selections": selections,
        "candidate_evaluations": candidate_evaluations,
        "trace": selected
    }


# --------------------------------------------------
# RUN ONE TEST INSTANCE
# --------------------------------------------------

def run_test(name, zones, centres):

    print("\n" + "=" * 65)
    print(name)
    print("=" * 65)

    print("Zones:", sorted(zones))
    print("Candidate Centres:")

    for centre, covered in centres.items():
        print(centre, ":", sorted(covered))

    print("\n--- EXACT SOLUTION ---")

    exact = exact_set_cover(zones, centres)

    print("Exact Solution:", exact["solution"])
    print("Exact Solution Size:", exact["solution_size"])
    print("Combinations Checked:",
          exact["combinations_checked"])

    print("\n--- GREEDY SOLUTION ---")

    greedy = greedy_set_cover(zones, centres)

    print("\nGreedy Solution:", greedy["solution"])
    print("Greedy Solution Size:", greedy["solution_size"])
    print("Greedy Selections:", greedy["selections"])
    print("Candidate Evaluations:",
          greedy["candidate_evaluations"])

    same = (
        exact["solution_size"] == greedy["solution_size"]
        if exact["solution_size"] is not None
        and greedy["solution_size"] is not None
        else False
    )

    print("\n--- COMPARISON ---")
    print("Both solutions have the same size:", same)

    return exact, greedy


# --------------------------------------------------
# TEST INSTANCE 1
# GREEDY COUNTEREXAMPLE
# --------------------------------------------------

zones1 = {1, 2, 3, 4, 5, 6}

centres1 = {
    "A": {1, 2, 3, 4},
    "B": {1, 2, 5},
    "C": {3, 4, 6}
}


# --------------------------------------------------
# TEST INSTANCE 2
# GREEDY MATCHES EXACT
# --------------------------------------------------

zones2 = {1, 2, 3, 4, 5}

centres2 = {
    "A": {1, 2, 3},
    "B": {4, 5},
    "C": {1, 4},
    "D": {2, 5},
    "E": {3, 4}
}


# --------------------------------------------------
# TEST INSTANCE 3
# GREEDY MATCHES EXACT
# --------------------------------------------------

zones3 = {1, 2, 3, 4, 5, 6}

centres3 = {
    "A": {1, 2, 3},
    "B": {4, 5, 6},
    "C": {1, 4},
    "D": {2, 5},
    "E": {3, 6}
}


# --------------------------------------------------
# LARGE SCALABILITY INSTANCE
# --------------------------------------------------

large_zones = set(range(1, 13))

large_centres = {
    "C1": {1, 2, 3, 4},
    "C2": {5, 6, 7, 8},
    "C3": {9, 10, 11, 12},
    "C4": {1, 5, 9},
    "C5": {2, 6, 10},
    "C6": {3, 7, 11},
    "C7": {4, 8, 12},
    "C8": {1, 6, 11}
}


# --------------------------------------------------
# MAIN EXECUTION
# --------------------------------------------------

if __name__ == "__main__":

    print("CO5 ASSIGNMENT 5")
    print("TASK B3 - EXACT VS APPROXIMATE SET COVER")

    # Three small test instances
    result1 = run_test(
        "TEST INSTANCE 1 - COUNTEREXAMPLE",
        zones1, centres1
    )

    result2 = run_test(
        "TEST INSTANCE 2",
        zones2, centres2
    )

    result3 = run_test(
        "TEST INSTANCE 3",
        zones3, centres3
    )

    # Large instance
    large_result = run_test(
        "LARGE SCALABILITY INSTANCE",
        large_zones, large_centres
    )

    # Final summary
    print("\n" + "=" * 65)
    print("FINAL EXPERIMENTAL SUMMARY")
    print("=" * 65)

    results = [
        ("Instance 1", result1),
        ("Instance 2", result2),
        ("Instance 3", result3),
        ("Large Instance", large_result)
    ]

    print(
        "{:<20} {:<15} {:<15} {:<15}".format(
            "Instance",
            "Exact Size",
            "Greedy Size",
            "Exact Checks"
        )
    )

    for name, result in results:

        exact, greedy = result

        print(
            "{:<20} {:<15} {:<15} {:<15}".format(
                name,
                str(exact["solution_size"]),
                str(greedy["solution_size"]),
                exact["combinations_checked"]
            )
        )

    print("\nEXPERIMENT COMPLETED")

