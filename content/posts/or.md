+++
date = '2025-10-02T00:00:00+10:00'
draft = false
title = 'Operational Research'
tags = ['Operational Research', 'Optimization', 'OR', 'Learning Path', 'Roadmap']
+++

A comprehensive, step-by-step roadmap to mastering Operational Research (OR) and Optimization, from foundational mathematics to expert-level systems and research. This guide is designed for self-learners, students, and professionals aiming to become top 1% in the field, with a focus on practical skills, coding, and real-world applications.

---

## Plan

### Complete Optimization & OR Learning Path: Zero to Expert

#### Master Roadmap Table

| Phase | Duration | Topics Covered | Skills Gained | Daily Activity (1hr) |
|-------|----------|---------------|---------------|---------------------|
| Phase 0: Prerequisites | Week 1-2 | Linear algebra review, calculus basics, problem-solving mindset | Mathematical foundations | 30min review, 30min exercises |
| Phase 1: Foundations | Week 3-6 | Linear programming, formulation, graphical method, simplex intuition | Can formulate and solve basic LP problems | 20min concepts, 40min practice |
| Phase 2: Core Techniques | Week 7-12 | Integer programming, binary variables, network flows, dynamic programming | Solve discrete optimization problems | 15min theory, 45min coding |
| Phase 3: Practical Mastery | Week 13-20 | Constraint programming, MIP, heuristics, real-world modeling | Build production systems | 10min reading, 50min building |
| Phase 4: Advanced Methods | Week 21-32 | Stochastic optimization, non-linear, multi-objective, column generation | Handle complex uncertainty | 15min advanced concepts, 45min implementation |
| Phase 5: Specialization | Week 33-52 | Deep dive into chosen domain (logistics/finance/scheduling/ML) | Domain expert | 5min review, 55min projects |
| Phase 6: Expert Territory | Year 2-3 | Research papers, custom algorithms, large-scale systems | Thought leader | Self-directed learning |

---

### Phase 0: Prerequisites (Week 1-2)

#### Week 1: Mathematical Foundations

| Day | Concept | What You'll Learn | Practice | Output |
|-----|---------|------------------|----------|--------|
| 1 | What is optimization? | Definition, types of problems, real-world examples | Read examples, identify optimization in daily life | List 10 optimization problems you encounter |
| 2 | Linear algebra basics | Vectors, matrices, linear combinations | Khan Academy linear algebra review | Solve 5 matrix problems |
| 3 | Equations & inequalities | Linear equations, systems of equations, graphing | Graph lines, find intersections | Graph 3-4 constraint lines by hand |
| 4 | Functions | What is a function, domain/range, linear functions | Identify objective functions in problems | Write 5 objective functions |
| 5 | Feasible regions | Understanding solution spaces, vertices | Draw feasible regions for 2-variable problems | Hand-draw 3 feasible region problems |
| 6 | Optimization intuition | Max vs min, constraints, trade-offs | Toy problems with 2 variables | Solve graphically by hand |
| 7 | Review & setup | Install Python, PuLP, Jupyter | Get environment working | Run "hello world" optimization |

**Learning Resources:**
- Khan Academy: Linear Algebra (select topics)
- 3Blue1Brown: Essence of Linear Algebra (YouTube, first 3 videos)
- Any college algebra textbook (Chapter on linear equations)

---

### Phase 1: Foundations (Week 3-6)

#### Week 3: Linear Programming Basics

| Day | Concept | Theory (20min) | Practice (40min) | Deliverable |
|-----|---------|---------------|------------------|-------------|
| 1 | LP definition | Standard form, decision variables, objective, constraints | Read LP intro, identify components | List components of 3 example problems |
| 2 | Formulation Part 1 | How to translate word problems to math | Work through production planning example | Formulate 2 simple problems |
| 3 | Formulation Part 2 | More examples: diet problem, blending | Practice formulation patterns | Formulate 3 different problem types |
| 4 | PuLP introduction | Syntax, creating variables, adding constraints | Follow PuLP tutorial | Run 2 examples successfully |
| 5 | First code | Build production planning in code | Code from scratch | Working production optimizer |
| 6 | Interpretation | Reading solver output, shadow prices, sensitivity | Analyze solutions | Explain what solution means |
| 7 | Mini-project | Your own problem | Apply everything learned | Custom problem + solution |

#### Week 4: Graphical Method & Understanding

| Day | Concept | Theory (20min) | Practice (40min) | Deliverable |
|-----|---------|---------------|------------------|-------------|
| 1 | Graphical LP | 2D LP problems, feasible region, corner-point solution | Graphing by hand, finding intersections | Hand-drawn feasible region for a new problem |
| 2 | Sensitivity analysis | How changes in coefficients affect solutions | Modify examples, observe changes | Sensitivity report for a given problem |
| 3 | Duality | Primal vs dual problems, economic interpretation | Formulate duals for practice problems | Dual problem and interpretation |
| 4 | Excel Solver | Using Excel for LP problems, solver setup | Follow Excel tutorial, solve provided problems | 3 problems solved in Excel |
| 5 | Advanced Excel | Sensitivity analysis, solver reports, scenario manager | Explore Excel features with practice data | Comprehensive report on a solved problem |
| 6 | Real-world LPs | Case studies: diet, finance, operations | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem | Formulate, solve, and analyze | Custom LP problem + Excel report |

#### Week 5: Simplex Method (Conceptual)

| Day | Concept | Theory (20min) | Practice (40min) | Deliverable |
|-----|---------|---------------|------------------|-------------|
| 1 | Simplex intro | Simplex tableau, basic feasible solutions | Convert LP problems to simplex tableau | Tableau for 3 example problems |
| 2 | Pivoting | Pivot element, row operations, new tableau | Perform pivoting on given tableaux | Series of tableaux showing pivot steps |
| 3 | Optimality conditions | When is a solution optimal? | Analyze tableaux for optimality | Explanation of optimality for 3 problems |
| 4 | Dual simplex | When to use dual simplex, differences from primal | Solve problems using dual simplex | Primal and dual solutions for comparison |
| 5 | Sensitivity in simplex | How simplex handles changes in real-time | Modify tableau elements, observe changes | Sensitivity analysis via simplex |
| 6 | Simplex in Excel | Setting up and solving simplex in Excel | Follow Excel simplex tutorial | Excel file with simplex solutions |
| 7 | Mini-project | Your own problem using simplex | Apply simplex method end-to-end | Custom problem + simplex tableau |

#### Week 6: Real Applications

| Day | Concept | Theory (20min) | Practice (40min) | Deliverable |
|-----|---------|---------------|------------------|-------------|
| 1 | LP in the real world | Case studies: transportation, manufacturing | Read and analyze provided case studies | 1-page summary of insights gained |
| 2 | From LP to MIP | When and why to use mixed-integer programming | Modify LP problems to include integer constraints | MIP formulation for 3 problems |
| 3 | Solving MIPs | Branch-and-bound, cutting planes | Solve provided MIP problems | Solutions and methods used |
| 4 | Advanced MIP techniques | Heuristics, metaheuristics, approximation algorithms | Apply techniques to challenging MIPs | Report on approach and solution quality |
| 5 | Simulation & OR | Monte Carlo simulation, risk analysis | Perform simulation on a given model | Simulation report with insights |
| 6 | Optimization software | Overview of CPLEX, Gurobi, other solvers | Install and run examples on chosen software | Solver output and analysis |
| 7 | Mini-project | Your own real-world problem using MIP | Formulate, solve, and analyze | Custom MIP problem + software report |

**Phase 1 Checkpoint:** Can you formulate and solve any basic LP problem? Can you explain what the solution means?

---

### Phase 2: Core Techniques (Week 7-12)

#### Week 7: Integer Programming

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | IP vs LP | Key differences, when to use integer programming | Identify IP needs in case studies | List of potential IP problems in given cases |
| 2 | Binary variables | Special case of IP, applications | Solve problems using binary variables | Solutions and methods used |
| 3 | General integer variables | Handling integer constraints in models | Modify LP problems to include integer constraints | MIP formulation for 3 problems |
| 4 | Solving IPs | Branch-and-bound, cutting planes, heuristics | Solve provided IP problems | Solutions and methods used |
| 5 | Advanced IP techniques | Metaheuristics, approximation algorithms | Apply techniques to challenging IPs | Report on approach and solution quality |
| 6 | IP in the real world | Case studies: capital budgeting, facility location | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using IP | Formulate, solve, and analyze | Custom IP problem + report |

#### Week 8: Network Flows

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Network flow problems | Types of problems, real-world applications | Identify network flow in case studies | List of potential network flow problems |
| 2 | Ford-Fulkerson method | Max flow problem, capacity constraints | Solve max flow problems by hand | Hand-solved max flow problem |
| 3 | Edmonds-Karp algorithm | BFS in residual graphs, finding augmenting paths | Implement Edmonds-Karp in code | Working code for max flow problem |
| 4 | Network simplex method | Specialized simplex for network problems | Solve network problems using network simplex | Solutions and methods used |
| 5 | Advanced network techniques | Multi-commodity flows, network design | Apply techniques to complex network problems | Report on approach and solution quality |
| 6 | Network flows in the real world | Case studies: transportation, telecommunications | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using network flows | Formulate, solve, and analyze | Custom network flow problem + report |

#### Week 9: Dynamic Programming

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | DP intro | Overlapping subproblems, optimal substructure | Identify DP opportunities in case studies | List of potential DP problems in given cases |
| 2 | Top-down vs bottom-up | Memoization vs tabulation, when to use each | Implement Fibonacci sequence in both ways | Working code for both DP approaches |
| 3 | Classic DP problems | Knapsack, longest common subsequence, matrix chain multiplication | Solve classic DP problems | Solutions and methods used |
| 4 | Advanced DP techniques | Bitmasking, DP with trees, DP with graphs | Apply techniques to complex DP problems | Report on approach and solution quality |
| 5 | DP in the real world | Case studies: resource allocation, scheduling | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | Heuristics and metaheuristics | Genetic algorithms, simulated annealing, tabu search | Apply heuristics to NP-hard problems | Report on approach and solution quality |
| 7 | Mini-project | Your own real-world problem using DP or heuristics | Formulate, solve, and analyze | Custom DP problem + report |

#### Week 10: Constraint Programming

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | CP intro | Constraints, variables, domains, CSPs | Identify CP opportunities in case studies | List of potential CP problems in given cases |
| 2 | Backtracking | Systematic search, pruning, constraint propagation | Implement N-Queens problem | Working code for N-Queens |
| 3 | Constraint propagation | Arc consistency, path consistency | Apply propagation techniques to CSPs | Report on consistency techniques used |
| 4 | Advanced CP techniques | Global constraints, decomposition, symmetry breaking | Apply techniques to complex CSPs | Report on approach and solution quality |
| 5 | CP in the real world | Case studies: scheduling, planning, resource allocation | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | Building a CP model | Identifying variables, constraints, and objectives | Model a real-world problem as a CSP | Complete CP model for a given problem |
| 7 | Mini-project | Your own real-world problem using CP | Formulate, solve, and analyze | Custom CP problem + report |

#### Week 11: Introduction to Stochastic Optimization

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Stochastic vs deterministic | Key differences, when to use stochastic optimization | Identify stochastic opportunities in case studies | List of potential stochastic problems |
| 2 | Basic concepts | Random variables, probability distributions, expectations | Calculate expectations for given distributions | Set of expectation calculations |
| 3 | Stochastic programming intro | Recourse problems, chance-constrained problems | Formulate simple stochastic programs | Stochastic formulation for 3 problems |
| 4 | Solving stochastic programs | Sample average approximation, stochastic gradient descent | Solve provided stochastic problems | Solutions and methods used |
| 5 | Advanced stochastic techniques | Dynamic programming for stochastic problems, Benders decomposition | Apply techniques to complex stochastic problems | Report on approach and solution quality |
| 6 | Stochastic optimization in the real world | Case studies: finance, supply chain, energy | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using stochastic optimization | Formulate, solve, and analyze | Custom stochastic problem + report |

#### Week 12: Introduction to Simulation Optimization

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Simulation vs optimization | Key differences, when to use simulation optimization | Identify simulation opportunities in case studies | List of potential simulation problems |
| 2 | Basic simulation concepts | Discrete event simulation, Monte Carlo simulation | Run basic simulations in Python | Set of Python simulation scripts |
| 3 | Coupling simulation and optimization | Simulation as a black box optimizer, optimization under uncertainty | Formulate problems that combine simulation and optimization | Coupled problem formulation for 3 cases |
| 4 | Solving simulation optimization problems | Ranking and selection, response surface methodology | Solve provided simulation optimization problems | Solutions and methods used |
| 5 | Advanced simulation techniques | Antithetic variates, control variates, importance sampling | Apply techniques to complex simulation problems | Report on approach and solution quality |
| 6 | Simulation optimization in the real world | Case studies: logistics, manufacturing, healthcare | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using simulation optimization | Formulate, solve, and analyze | Custom simulation problem + report |

**Phase 2 Checkpoint:** Can you model complex discrete decisions? Can you choose the right technique for different problems?

---

### Phase 3: Practical Mastery (Week 13-20)

#### Week 13: Constraint Programming

| Day | Concept | Theory (10min) | Practice (50min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | CP intro | Constraints, variables, domains, CSPs | Identify CP opportunities in case studies | List of potential CP problems in given cases |
| 2 | Backtracking | Systematic search, pruning, constraint propagation | Implement N-Queens problem | Working code for N-Queens |
| 3 | Constraint propagation | Arc consistency, path consistency | Apply propagation techniques to CSPs | Report on consistency techniques used |
| 4 | Global constraints | Common global constraints in CP (e.g., all-different) | Implement problems using global constraints | Solutions and methods used |
| 5 | Decomposition in CP | Breaking problems into smaller sub-problems | Apply decomposition to a complex CSP | Report on decomposition approach |
| 6 | Symmetry breaking | Identifying and breaking symmetries in CSPs | Apply symmetry breaking to a CSP | Report on symmetry breaking techniques |
| 7 | Mini-project | Your own real-world problem using CP | Formulate, solve, and analyze | Custom CP problem + report |

#### Week 14: Mixed-Integer Programming

| Day | Concept | Theory (10min) | Practice (50min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | MIP intro | Key differences between LP and MIP, when to use MIP | Identify MIP opportunities in case studies | List of potential MIP problems in given cases |
| 2 | Binary and integer variables | Special cases of MIP, applications | Solve problems using binary and integer variables | Solutions and methods used |
| 3 | General MIP formulation | How to formulate a general MIP problem | Formulate MIP problems from given scenarios | MIP formulation for 3 problems |
| 4 | Solving MIPs | Branch-and-bound, cutting planes, heuristics | Solve provided MIP problems | Solutions and methods used |
| 5 | Advanced MIP techniques | Metaheuristics, approximation algorithms | Apply techniques to challenging MIPs | Report on approach and solution quality |
| 6 | MIP in the real world | Case studies: capital budgeting, facility location | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using MIP | Formulate, solve, and analyze | Custom MIP problem + report |

#### Week 15: Dynamic Programming

| Day | Concept | Theory (10min) | Practice (50min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | DP intro | Overlapping subproblems, optimal substructure | Identify DP opportunities in case studies | List of potential DP problems in given cases |
| 2 | Top-down vs bottom-up | Memoization vs tabulation, when to use each | Implement Fibonacci sequence in both ways | Working code for both DP approaches |
| 3 | Classic DP problems | Knapsack, longest common subsequence, matrix chain multiplication | Solve classic DP problems | Solutions and methods used |
| 4 | DP with trees | Representing and solving problems with trees | Solve tree-based problems using DP | Solutions and methods used |
| 5 | DP with graphs | Representing and solving problems with graphs | Solve graph-based problems using DP | Solutions and methods used |
| 6 | Advanced DP techniques | Bitmasking, DP with trees, DP with graphs | Apply techniques to complex DP problems | Report on approach and solution quality |
| 7 | Mini-project | Your own real-world problem using DP | Formulate, solve, and analyze | Custom DP problem + report |

#### Week 16: Simulation Optimization

| Day | Concept | Theory (10min) | Practice (50min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Simulation vs optimization | Key differences, when to use simulation optimization | Identify simulation opportunities in case studies | List of potential simulation problems |
| 2 | Basic simulation concepts | Discrete event simulation, Monte Carlo simulation | Run basic simulations in Python | Set of Python simulation scripts |
| 3 | Coupling simulation and optimization | Simulation as a black box optimizer, optimization under uncertainty | Formulate problems that combine simulation and optimization | Coupled problem formulation for 3 cases |
| 4 | Solving simulation optimization problems | Ranking and selection, response surface methodology | Solve provided simulation optimization problems | Solutions and methods used |
| 5 | Advanced simulation techniques | Antithetic variates, control variates, importance sampling | Apply techniques to complex simulation problems | Report on approach and solution quality |
| 6 | Simulation optimization in the real world | Case studies: logistics, manufacturing, healthcare | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using simulation optimization | Formulate, solve, and analyze | Custom simulation problem + report |

#### Week 17: Introduction to Metaheuristics

| Day | Concept | Theory (10min) | Practice (50min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Metaheuristics intro | What are metaheuristics, when to use them | Identify opportunities for metaheuristics in case studies | List of potential metaheuristic problems |
| 2 | Genetic algorithms | Basic concepts, selection, crossover, mutation | Implement a simple genetic algorithm | Working code for a genetic algorithm |
| 3 | Simulated annealing | Annealing schedule, acceptance criteria | Implement simulated annealing for a TSP problem | Working code for simulated annealing |
| 4 | Tabu search | Tabu list, aspiration criteria | Implement tabu search for a scheduling problem | Working code for tabu search |
| 5 | Advanced metaheuristics | Ant colony optimization, particle swarm optimization | Implement advanced metaheuristics for comparison | Working code for 2 advanced metaheuristics |
| 6 | Metaheuristics in the real world | Case studies: routing, scheduling, design | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using metaheuristics | Formulate, solve, and analyze | Custom metaheuristic problem + report |

#### Week 18: Introduction to Machine Learning for OR

| Day | Concept | Theory (10min) | Practice (50min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | ML intro | What is machine learning, types of ML | Identify ML opportunities in OR problems | List of potential ML problems in OR |
| 2 | Supervised learning | Regression, classification, model evaluation | Implement linear regression and logistic regression | Working code for regression problems |
| 3 | Unsupervised learning | Clustering, dimensionality reduction | Implement k-means clustering and PCA | Working code for clustering and PCA |
| 4 | Reinforcement learning | RL basics, Markov decision processes | Implement a simple RL problem | Working code for a reinforcement learning problem |
| 5 | Neural networks | Basics of neural networks, backpropagation | Implement a simple neural network from scratch | Working code for a neural network |
| 6 | ML in the real world | Case studies: predictive maintenance, demand forecasting | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using ML | Formulate, solve, and analyze | Custom ML problem + report |

#### Week 19: Advanced Topics in OR

| Day | Concept | Theory (10min) | Practice (50min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Game theory | Basics of game theory, Nash equilibrium | Identify game theory opportunities in case studies | List of potential game theory problems |
| 2 | Decision analysis | Decision trees, utility theory | Solve decision analysis problems | Solutions and methods used |
| 3 | Nonlinear programming | Basics of nonlinear programming, KKT conditions | Solve nonlinear programming problems | Solutions and methods used |
| 4 | Global optimization | Challenges in global optimization, techniques | Apply global optimization techniques to problems | Report on approach and solution quality |
| 5 | OR in healthcare | Applications of OR in healthcare, case studies | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | OR in finance | Applications of OR in finance, case studies | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using advanced OR topics | Formulate, solve, and analyze | Custom problem + report |

#### Week 20: Capstone Project

| Day | Concept | Theory (10min) | Practice (50min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Capstone intro | Choosing a capstone project, defining scope | Identify potential capstone projects | List of 3 potential capstone projects |
| 2 | Project planning | Setting milestones, deliverables, and timelines | Create a project plan for your capstone | Detailed project plan |
| 3 | Literature review | Reviewing relevant literature, identifying gaps | Conduct a literature review for your project | Literature review summary |
| 4 | Methodology | Choosing appropriate methods and techniques | Define the methodology for your project | Methodology section of your report |
| 5 | Implementation | Implementing the chosen methods and techniques | Work on the implementation of your project | Progress on project implementation |
| 6 | Testing and validation | Testing the solution, validating results | Test and validate your project solution | Testing and validation report |
| 7 | Final presentation | Preparing and delivering the final presentation | Present your capstone project | Final presentation slides and recording |

**Phase 3 Checkpoint:** Can you build production-ready optimization systems? Can you handle large, messy real problems?

---

### Phase 4: Advanced Methods (Week 21-32)

#### Week 21: Advanced Linear Programming

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Advanced LP topics | Decomposition, duality, sensitivity analysis | Review advanced LP topics | Summary of advanced LP topics |
| 2 | Large-scale LP | Challenges and techniques for large-scale LP | Solve large-scale LP problems | Solutions and methods used |
| 3 | Sparse LP | Exploiting sparsity in LP problems | Solve sparse LP problems | Solutions and methods used |
| 4 | Structured LP | Exploiting problem structure in LP | Solve structured LP problems | Solutions and methods used |
| 5 | LP in the real world | Case studies: energy, transportation, finance | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | Mini-project | Your own real-world problem using advanced LP | Formulate, solve, and analyze | Custom LP problem + report |
| 7 | Review and catch-up | Review key concepts, catch up on any missed work | Revise and consolidate your learning | Revised notes and summaries |

#### Week 22: Advanced Integer Programming

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Advanced IP topics | Cutting planes, branch-and-cut, branch-and-price | Review advanced IP topics | Summary of advanced IP topics |
| 2 | Solving large IPs | Techniques for solving large integer programming problems | Solve large IP problems | Solutions and methods used |
| 3 | Stochastic IP | Integer programming with stochastic elements | Solve stochastic IP problems | Solutions and methods used |
| 4 | Robust IP | Integer programming with robustness considerations | Solve robust IP problems | Solutions and methods used |
| 5 | IP in the real world | Case studies: logistics, finance, telecommunications | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | Mini-project | Your own real-world problem using advanced IP | Formulate, solve, and analyze | Custom IP problem + report |
| 7 | Review and catch-up | Review key concepts, catch up on any missed work | Revise and consolidate your learning | Revised notes and summaries |

#### Week 23: Advanced Network Optimization

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Advanced network topics | Multi-commodity flows, network design, stochastic networks | Review advanced network topics | Summary of advanced network topics |
| 2 | Solving large network problems | Techniques for solving large network optimization problems | Solve large network problems | Solutions and methods used |
| 3 | Dynamic network optimization | Network optimization with dynamic elements | Solve dynamic network problems | Solutions and methods used |
| 4 | Robust network optimization | Network optimization with robustness considerations | Solve robust network problems | Solutions and methods used |
| 5 | Network optimization in the real world | Case studies: transportation, telecommunications, supply chain | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | Mini-project | Your own real-world problem using advanced network optimization | Formulate, solve, and analyze | Custom network problem + report |
| 7 | Review and catch-up | Review key concepts, catch up on any missed work | Revise and consolidate your learning | Revised notes and summaries |

#### Week 24: Advanced Dynamic Programming

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Advanced DP topics | DP with trees, DP with graphs, DP with recurrences | Review advanced DP topics | Summary of advanced DP topics |
| 2 | Solving large DP problems | Techniques for solving large dynamic programming problems | Solve large DP problems | Solutions and methods used |
| 3 | Approximate DP | Approximation algorithms for dynamic programming | Solve problems using approximate DP | Solutions and methods used |
| 4 | Online DP | Dynamic programming with online algorithms | Solve online DP problems | Solutions and methods used |
| 5 | DP in the real world | Case studies: resource allocation, scheduling, finance | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | Mini-project | Your own real-world problem using advanced DP | Formulate, solve, and analyze | Custom DP problem + report |
| 7 | Review and catch-up | Review key concepts, catch up on any missed work | Revise and consolidate your learning | Revised notes and summaries |

#### Week 25: Advanced Simulation Techniques

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Advanced simulation topics | Antithetic variates, control variates, importance sampling | Review advanced simulation topics | Summary of advanced simulation topics |
| 2 | Solving large simulation problems | Techniques for solving large simulation problems | Solve large simulation problems | Solutions and methods used |
| 3 | Parallel and distributed simulation | Techniques for parallel and distributed simulation | Implement parallel simulation for a given problem | Working code for parallel simulation |
| 4 | Simulation optimization | Combining simulation and optimization techniques | Solve simulation optimization problems | Solutions and methods used |
| 5 | Simulation in the real world | Case studies: logistics, manufacturing, healthcare | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | Mini-project | Your own real-world problem using advanced simulation techniques | Formulate, solve, and analyze | Custom simulation problem + report |
| 7 | Review and catch-up | Review key concepts, catch up on any missed work | Revise and consolidate your learning | Revised notes and summaries |

#### Week 26: Introduction to Machine Learning for OR

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | ML intro | What is machine learning, types of ML | Identify ML opportunities in OR problems | List of potential ML problems in OR |
| 2 | Supervised learning | Regression, classification, model evaluation | Implement linear regression and logistic regression | Working code for regression problems |
| 3 | Unsupervised learning | Clustering, dimensionality reduction | Implement k-means clustering and PCA | Working code for clustering and PCA |
| 4 | Reinforcement learning | RL basics, Markov decision processes | Implement a simple RL problem | Working code for a reinforcement learning problem |
| 5 | Neural networks | Basics of neural networks, backpropagation | Implement a simple neural network from scratch | Working code for a neural network |
| 6 | ML in the real world | Case studies: predictive maintenance, demand forecasting | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using ML | Formulate, solve, and analyze | Custom ML problem + report |

#### Week 27: Advanced Topics in OR

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Game theory | Basics of game theory, Nash equilibrium | Identify game theory opportunities in case studies | List of potential game theory problems |
| 2 | Decision analysis | Decision trees, utility theory | Solve decision analysis problems | Solutions and methods used |
| 3 | Nonlinear programming | Basics of nonlinear programming, KKT conditions | Solve nonlinear programming problems | Solutions and methods used |
| 4 | Global optimization | Challenges in global optimization, techniques | Apply global optimization techniques to problems | Report on approach and solution quality |
| 5 | OR in healthcare | Applications of OR in healthcare, case studies | Read and analyze provided case studies | 1-page summary of insights gained |
| 6 | OR in finance | Applications of OR in finance, case studies | Read and analyze provided case studies | 1-page summary of insights gained |
| 7 | Mini-project | Your own real-world problem using advanced OR topics | Formulate, solve, and analyze | Custom problem + report |

#### Week 28: Capstone Project

| Day | Concept | Theory (15min) | Practice (45min) | Deliverable |
|-----|---------|----------------|------------------|-------------|
| 1 | Capstone intro | Choosing a capstone project, defining scope | Identify potential capstone projects | List of 3 potential capstone projects |
| 2 | Project planning | Setting milestones, deliverables, and timelines | Create a project plan for your capstone | Detailed project plan |
| 3 | Literature review | Reviewing relevant literature, identifying gaps | Conduct a literature review for your project | Literature review summary |
| 4 | Methodology | Choosing appropriate methods and techniques | Define the methodology for your project | Methodology section of your report |
| 5 | Implementation | Implementing the chosen methods and techniques | Work on the implementation of your project | Progress on project implementation |
| 6 | Testing and validation | Testing the solution, validating results | Test and validate your project solution | Testing and validation report |
| 7 | Final presentation | Preparing and delivering the final presentation | Present your capstone project | Final presentation slides and recording |

**Phase 4 Checkpoint:** Can you handle uncertainty, nonlinearity, and massive scale? Can you research and implement advanced methods?

---

### Phase 5: Specialization (Week 33-52)

Choose ONE specialization area and go deep:

#### Option A: Logistics & Transportation
- Vehicle routing variants (CVRP, VRPTW, MDVRP)
- Last-mile delivery, drones
- Warehouse optimization, picking
- Supply chain networks
- Capstone: Complete logistics platform

#### Option B: Scheduling & Workforce
- Advanced workforce scheduling
- Project scheduling, RCPSP
- Maintenance scheduling
- Exam timetabling, course scheduling
- Capstone: Universal scheduling platform

#### Option C: Finance & Portfolio Management
- Advanced portfolio optimization
- Trading optimization
- Risk management
- Asset-liability management
- Capstone: Quantitative trading system

#### Option D: Machine Learning & AI
- Hyperparameter optimization
- Neural architecture search
- Reinforcement learning optimization
- Optimization in deep learning
- Capstone: ML-assisted optimization

#### Option E: Energy & Sustainability
- Power grid optimization
- Renewable energy integration
- Electric vehicle charging
- Carbon footprint optimization
- Capstone: Smart grid system

**Phase 5 Goal:** Become top 1% in your chosen domain.

---

### Phase 6: Expert Territory (Year 2-3)

| Quarter | Activities | Outputs | Recognition |
|---------|------------|---------|-------------|
| Q5-Q6 | Read research papers, implement novel algorithms | Paper implementations, blog posts | Known in community |
| Q7-Q8 | Contribute to open-source OR projects | Significant contributions | Project maintainer |
| Q9-Q10 | Solve competition problems, publish solutions | Kaggle medals, write-ups | Top competitor |
| Q11-Q12 | Develop novel techniques, write papers | Conference submissions | Thought leader |

---

This roadmap is designed to be actionable, modular, and adaptable to your pace. Each phase builds on the previous, ensuring a strong foundation and practical expertise in Operational Research and Optimization.
