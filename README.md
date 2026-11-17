# Solutions of the PDPTW instances of Sartori and Buriol (2020) from a GPU-parallel hierarchical search

Solutions of the 300 instances of the pickup and delivery problem with time windows (PDPTW) of Sartori and Buriol
(2020), from 100 to 5000 locations ([instance repository](https://github.com/cssartori/pdptw-instances)), obtained
with a metaheuristic that runs thousands of search trajectories on a single GPU. The method is described in a paper
in preparation; the citation will be added here.

The objective is hierarchical: first the number of vehicles, then the total travel time.

## Contents

- `main_table/`: one solution per instance (300), from one run of the method (seed 1) at the standard time limits of
  Hiermann and Schiffer (2026): 5 minutes for 100 locations, 15 for 200 and 400, 30 for 600 and 60 from 800 on, on an
  NVIDIA GeForce RTX 5070 Ti. In total, 28 034 vehicles.
- `main_table.csv`: for every instance, the vehicles and the travel time of that solution, the time limit, the best of
  the five seeds of Hiermann and Schiffer (2026) at the standard limit, and the best-known solution of the instance
  repository in October 2026.
- `best_known/`: the 38 solutions that improve the best-known solutions of the instance repository as of October 2026:
  22 with fewer vehicles and 16 with the same fleet and less travel time. All but two were found from scratch within the
  standard time limits (three of them by a CPU version of the method); on bar-n600-7 the travel time of the previous
  best-known solution was lowered by moving zero-load blocks between routes, and poa-n1000-2 comes from a longer run.
- `best_known.csv`: for each of these instances, the vehicles and the travel time of the solution and of the previous
  best-known solution.

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
