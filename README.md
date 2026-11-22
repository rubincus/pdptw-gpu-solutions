# Solutions of the PDPTW instances of Sartori and Buriol (2020) from a GPU-parallel hierarchical search

Solutions of the 300 instances of the pickup and delivery problem with time windows (PDPTW) of Sartori and Buriol
(2020), from 100 to 5000 locations ([instance repository](https://github.com/cssartori/pdptw-instances)), obtained
with a metaheuristic that runs up to 256 cooperating search trajectories on a single GPU. The method is described in a paper
in preparation; the citation will be added here.

The objective is hierarchical: first the number of vehicles, then the total travel time.

## Contents

- `main_table/`: one solution per instance (300), from one run of the method (seed 1) at the standard time limits of
  Hiermann and Schiffer (2026): 5 minutes for 100 locations, 15 for 200 and 400, 30 for 600 and 60 from 800 on, on an
  NVIDIA GeForce RTX 5070 Ti. In total, 28 034 vehicles.
- `main_table.csv`: for every instance, the vehicles and the travel time of that solution, the time limit, the best of
  the five seeds of Hiermann and Schiffer (2026) at the standard limit, the best-known solution of the instance
  repository at commit `b2f0569` (9 October 2026), and the run, seed and hardware behind the solution.
- `best_known/`: the 38 solutions that improve the best-known solutions of the instance repository at commit `b2f0569`
  (9 October 2026): 22 with fewer vehicles and 16 with the same fleet and less travel time. The run of the main table
  alone improves 32 instances (21 with fewer vehicles). The others come from two other runs of the GPU method and
  three of a CPU version, all from scratch within the standard time limits, and from two solutions outside that
  setting: bar-n600-7, whose previous best-known solution was improved by moving zero-load blocks between routes, and
  poa-n1000-2, from a longer run. The improvements are relative to that snapshot of the repository.
- `best_known.csv`: for each of these instances, the vehicles and the travel time of the solution and of the previous
  best-known solution, and its origin (`how`: R, the run of the main table; S, another run of the GPU method from
  scratch; C, the CPU version from scratch; B, block moves; L, a longer run).

- `runs/` and `runs.csv`: the solutions of every other run reported in the paper, so that its comparisons can be
  checked with the official validator. `runs.csv` gives, for every solution, the run, the method, the seed, the
  hardware, the time limit, the vehicles and the travel time. All runs are at the standard time limits, from scratch:
  - `equal_hardware/`: seeds 2 and 3 of the proposed method on the 25 instances with 600 locations (seed 1 is in
    `main_table/`), and the public code of Hiermann and Schiffer (2026) run on the same workstation with seeds 1, 3
    and 5 and 4 threads, on those 25 instances, on 16 large instances (two per size from 800 to 5000 locations, all
    numbered 1) and on 6 small ones (two per size from 100 to 400, numbered 1);
  - `cpu_condition/`: the CPU version of the proposed method (no GPU) on 24 instances (two per size, numbered 1),
    with 4 worker processes on four performance cores and with 27 processes;
  - `ablation/`: the variants of the analysis of components (guided ejection search alone, plus the fixed-fleet tabu
    search, and the full method) with seeds 1 to 3 on 12 instances, one per size (the full method with seed 1 is in
    `main_table/`);
  - `seeds/`: seeds 2 and 3 of the proposed method on the 24 instances of the CPU condition;
  - `mechanisms/`: the analysis of the mechanisms on the 12 instances of the ablation: seeds 4, 5 and 6 of the
    proposed method (`full_seed*`); from the solution each of these runs saved when its fleet search ended, three
    branches that received the time the run had left (`branch_random`: random groups in the second stage;
    `branch_cost`: the cost phase instead of the second stage; `branch_fleet`: more fixed-fleet attempts, then the
    second stage), so that each branch solution also took the standard time limit in total; and the version with
    independent trajectories, seeds 1 to 3 (`independent_seed*`).

## Format

The format of the instance repository: a header (instance name, authors, date, reference), then one line per route
with the indices of the nodes in the order of the visits, the depot omitted. File names follow the pattern
`<instance>.<vehicles>_<travel time>.txt`.

## Validation

Every solution was checked with the official validator of the instance repository and with an independent evaluator
that also checks that the pickup and the delivery of each request are served by the same route.

## References

- Sartori, C. S., and Buriol, L. S. (2020). A study on the pickup and delivery problem with time windows: Matheuristics
  and new instances. *Computers & Operations Research*, 124, 105065.
- Hiermann, G., and Schiffer, M. (2026). A decomposition-based approach for large-scale pickup and delivery problems.
  *European Journal of Operational Research*, 333(3), 746–761.

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), the license of the instances.
