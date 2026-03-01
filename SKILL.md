---
name: Genome Weaver
category: evolution
version: 1.0.0
description: Evolutionary design and genetic algorithms for optimization, creative generation, and adaptive systems
tags: [evolution, genetic, optimization, algorithm, ai]
author: OpenClaw
dependencies: []
environment:
  PYTHONPATH: include src
  GW_POPULATION_SIZE: "100"
  GW_MUTATION_RATE: "0.05"
  GW_CROSSOVER_RATE: "0.7"
  GW_ELITE_COUNT: "5"
workspaces: [genome-weaver]
commands:
  - gw-evolve
  - gw-evaluate
  - gw-visualize
  - gw-export
  - gw-analyze
---

# Genome Weaver

Evolutionary design and genetic algorithms for optimization, creative generation, and adaptive systems.

## Overview

Genome Weaver provides a complete evolutionary computation framework for solving optimization problems, evolving neural network architectures, generating creative artifacts, and building adaptive systems. It implements multiple evolutionary strategies including genetic algorithms, evolution strategies, and genetic programming.

## Quick Start

```bash
# Initialize a new evolutionary project
gw-evolve init --template neural-architecture --name my-evolver

# Run evolution with default settings
gw-evolve run --generations 100 --population 50

# Evaluate a specific genome
gw-evaluate evaluate genome.json --fitness-function benchmark.yaml

# Visualize evolution progress
gw-visualize dashboard --port 8080
```

## Core Commands

### `gw-evolve`

Primary command for running evolutionary processes.

```bash
# Basic evolution run
gw-evolve run --config evolution.yaml

# With custom parameters
gw-evolve run \
  --generations 500 \
  --population 200 \
  --mutation-rate 0.08 \
  --crossover-rate 0.75 \
  --tournament-size 5 \
  --elite-count 10

# Resume from checkpoint
gw-evolve run --resume checkpoint_gen_250.pkl

# Parallel island model evolution
gw-evolve run --islands 4 --migration-interval 10
```

### `gw-evaluate`

Fitness evaluation and genome analysis.

```bash
# Evaluate single genome
gw-evaluate evaluate genome.pkl --fitness sum-of-squares

# Batch evaluate population
gw-evaluate batch-eval population/ --output results.csv

# Compare genomes
gw-evaluate compare genome_a.pkl genome_b.pkl

# Validate genome structure
gw-evaluate validate genome.pkl --schema gene-schema.yaml
```

### `gw-visualize`

Visualization and monitoring tools.

```bash
# Real-time dashboard
gw-visualize dashboard --port 8080

# Fitness landscape plot
gw-visualize fitness-plot --generation 100 --output fitness.png

# Population diversity heatmap
gw-visualize diversity --output diversity.png

# Pareto front visualization (multi-objective)
gw-visualize pareto --objectives "accuracy,latency,size"
```

### `gw-export`

Export genomes and results in various formats.

```bash
# Export best genome
gw-export best --format json --output winner.json

# Export entire population
gw-export population --format numpy --output pop_archive/

# Export evolution statistics
gw-export stats --format csv --output evolution_log.csv

# Export to ONNX for inference
gw-export model genome.pkl --format onnx --output model.onnx
```

### `gw-analyze`

Statistical analysis and insights.

```bash
# Convergence analysis
gw-analyze convergence --generations 100

# Genetic diversity analysis
gw-analyze diversity --metric hamming

# Parameter sensitivity analysis
gw-analyze sensitivity --param mutation_rate --range 0.01-0.3

# Schema analysis (building block detection)
gw-analyze schema --threshold 0.7
```

## Use Cases

### 1. Neural Architecture Search

Evolve efficient neural network architectures for specific tasks.

```yaml
# config.yaml
evolution:
  type: neuroevolution
  genome:
    layers:
      - type: [conv2d, dense, dropout, maxpool]
      - units: range(16, 512)
      - activation: [relu, tanh, sigmoid, leaky_relu]
    connections: adjacency_matrix
  
  fitness:
    - metric: accuracy
      target: > 0.95
    - metric: params
      constraint: < 1000000
    - metric: latency
      constraint: < 50ms
  
  selection:
    method: tournament
    size: 5
  
  operators:
    crossover: uniform
    mutation:
      add_layer: 0.1
      remove_layer: 0.05
      modify_units: 0.2
      change_activation: 0.15
```

```bash
gw-evolve run --config config.yaml --generations 200
```

### 2. Robot Control Policy Evolution

Evolve controllers for robotic systems.

```yaml
# robot_controller.yaml
evolution:
  type: genetic-programming
  genome:
    representation: tree
    functions: [ADD, SUB, MULT, DIV, SIN, COS, IF_GT, PROG]
    terminals: [X, Y, DX, DY, SENSOR_0, SENSOR_1, SENSOR_2, RAND]
    max_depth: 8
  
  fitness:
    - track: distance_to_target
      weight: -1.0
    - track: energy_used
      weight: -0.1
    - track: time_to_goal
      weight: -0.5
  
  environment:
    simulator: pybullet
    robot: quadruped
    task: gait_optimization
    episodes: 10
```

```bash
gw-evolve run --config robot_controller.yaml --checkpoint-interval 25
```

### 3. Art and Music Generation

Evolve creative artifacts using aesthetic fitness functions.

```yaml
# art_evolver.yaml
evolution:
  type: compositional
  genome:
    representation: direct
    genes:
      - shapes: sequence of primitives
      - colors: palette specification
      - composition: layout rules
      - style: artistic parameters
  
  fitness:
    - metric: aesthetic_score
      model: pretrained-aesthetic-vgg
    - metric: color_harmony
    - metric: rule_following
    - user_feedback: interactive
  
  novelty:
    enabled: true
    archive_size: 500
```

```bash
gw-evolve run --config art_evolver.yaml --generations 1000 --interactive
```

### 4. Combinatorial Optimization

Solve NP-hard optimization problems.

```bash
# Traveling Salesman Problem
gw-evolve run \
  --problem tsp \
  --cities 50 \
  --population 500 \
  --generations 1000 \
  --cx-order crossover

# Job Shop Scheduling
gw-evolve run \
  --problem jsp \
  --jobs 20 \
  --machines 10 \
  --fitness makespan \
  --constraint-machine-availability availability.yaml

# Vehicle Routing Problem
gw-evolve run \
  --problem vrp \
  --depot 1 \
  --vehicles 10 \
  --demands demand_matrix.csv \
  --capacity 200
```

### 5. Symbolic Regression

Discover mathematical formulas from data.

```yaml
# symbolic_reg.yaml
evolution:
  type: genetic-programming
  genome:
    functions: [ADD, SUB, MUL, DIV, POW, LOG, EXP, SIN, COS]
    constants: learned
    variables: [x, y, z]
    max_size: 50
  
  fitness:
    - metric: rmse
      data: training.csv
    - metric: complexity
      weight: -0.01
  
  bloat_control:
    method: parsimony
    pressure: 0.5
```

```bash
gw-evolve run --config symbolic_reg.yaml --data observations.csv
```

## Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `GW_POPULATION_SIZE` | 100 | Number of individuals in population |
| `GW_MUTATION_RATE` | 0.05 | Probability of gene mutation |
| `GW_CROSSOVER_RATE` | 0.7 | Probability of crossover operation |
| `GW_ELITE_COUNT` | 5 | Number of best individuals preserved |
| `GW_SEED` | random | Random seed for reproducibility |
| `GW_PARALLEL` | true | Enable parallel fitness evaluation |
| `GW_WORKERS` | 4 | Number of parallel workers |

### Configuration File Structure

```yaml
# Full configuration example
version: "1.0"

evolution:
  # Evolution strategy
  strategy: [ga, es, gp, ce]
  
  # Termination criteria
  termination:
    generations: 1000
    fitness: 0.99
    stall_generations: 50
    time_limit: 3600  # seconds
  
  # Population
  population:
    size: 200
    initialization: random  # [random, seeded, halton]
  
  # Selection
  selection:
    method: tournament  # [tournament, roulette, rank, nsga2]
    size: 5
    pressure: 1.5
  
  # Variation operators
  variation:
    crossover:
      type: [one-point, two-point, uniform, pmx, ox]
      rate: 0.8
    mutation:
      type: [flip, scramble, invert, gaussian]
      rate: 0.05
      strength: 0.1
  
  # Elitism
  elitism:
    enabled: true
    count: 10
  
  # Niching and diversity
  niching:
    method: [fitness-sharing, crowding, novelty]
    radius: 0.5

# Genome specification
genome:
  # Direct encoding
  genes:
    - name: weights
      type: matrix
      shape: [128, 64]
      bounds: [-1, 1]
    - name: bias
      type: vector
      length: 64
  
  # Or use template
  template: neural-network

# Fitness evaluation
fitness:
  # Single objective
  objective: maximize
  function: custom_module.evaluate
  
  # Multi-objective (Pareto)
  objectives:
    - name: accuracy
      weight: 1.0
    - name: complexity
      weight: -0.1
  
  # Constraints
  constraints:
    - type: penalty
      expression: "if params > 1000000: return -1000"
  
  # Evaluation settings
  evaluation:
    parallel: true
    workers: 8
    cache: true

# Checkpointing
checkpoint:
  enabled: true
  interval: 10
  directory: checkpoints/
  keep_last: 5

# Logging
logging:
  level: INFO
  file: evolution.log
  metrics:
    - generation
    - best_fitness
    - avg_fitness
    - diversity
    - hall_of_fame
```

## Troubleshooting

### Evolution Not Converging

**Symptoms**: Fitness plateaus or oscillates without improvement.

**Solutions**:

1. Increase mutation rate:
   ```bash
   gw-evolve run --mutation-rate 0.15
   ```

2. Reduce selection pressure:
   ```bash
   gw-evolve run --tournament-size 3
   ```

3. Check fitness function for bugs:
   ```bash
   gw-evaluate debug fitness.py --test-case simple
   ```

4. Ensure population has sufficient diversity:
   ```bash
   gw-analyze diversity --metric shannon
   ```

### Premature Convergence

**Symptoms**: Evolution converges to local optima quickly.

**Solutions**:

1. Increase population size:
   ```bash
   gw-evolve run --population 500
   ```

2. Enable novelty search:
   ```bash
   gw-evolve run --novelty true --novelty-weight 0.5
   ```

3. Add diversity preservation:
   ```bash
   gw-evolve run --niching fitness-sharing --niching-radius 0.3
   ```

4. Use restarts:
   ```bash
   gw-evolve run --restarts 3 --restart-fitness 0.8
   ```

### Out of Memory

**Symptoms**: Process killed during large population evaluation.

**Solutions**:

1. Reduce population size:
   ```bash
   gw-evolve run --population 50
   ```

2. Enable lazy evaluation:
   ```bash
   gw-evolve run --lazy-eval true
   ```

3. Reduce checkpoint frequency:
   ```bash
   gw-evolve run --checkpoint-interval 50
   ```

### Fitness Evaluation Too Slow

**Symptoms**: Evolution takes hours/days for single generation.

**Solutions**:

1. Enable parallel evaluation:
   ```bash
   gw-evolve run --workers 16
   ```

2. Use surrogate models:
   ```bash
   gw-evolve run --surrogate gaussian-process
   ```

3. Cache fitness values:
   ```bash
   gw-evolve run --fitness-cache true
   ```

4. Reduce evaluation episodes (for simulation):
   ```bash
   gw-evolve run --episodes 3
   ```

### Invalid Genome Structure

**Symptoms**: "Genome validation failed" errors.

**Solutions**:

1. Validate genome schema:
   ```bash
   gw-validate genome.pkl --schema schema.yaml
   ```

2. Check bounds in configuration:
   ```yaml
   genes:
     - name: weight
       bounds: [-1, 1]  # Must be specified
   ```

3. Fix custom genetic operators:
   ```python
   def mutate(genome):
       # Ensure valid output
       return clamp(genome, min_val, max_val)
   ```

## Examples

### Example 1: Simple Function Optimization

Minimize the Ackley function.

```python
# ackley.py
import numpy as np

def fitness(genome):
    x, y = genome.values
    a = 20 * np.exp(-0.2 * np.sqrt(0.5 * (x**2 + y**2)))
    b = np.exp(0.5 * (np.cos(2 * np.pi * x) + np.cos(2 * np.pi * y)))
    return -(a - b + np.e + 20)

if __name__ == "__main__":
    import genome_weaver as gw
    
    engine = gw.Evolution(
        genome_schema={"x": (-5, 5), "y": (-5, 5)},
        population_size=100,
        mutation_rate=0.1,
        crossover_rate=0.8
    )
    
    best = engine.run(generations=200)
    print(f"Best: {best.genome}, Fitness: {best.fitness}")
```

```bash
python ackley.py
# Output: Best: {'x': 0.0, 'y': 0.0}, Fitness: 0.0
```

### Example 2: Custom Genetic Operator

Implement custom crossover for permutations.

```python
from genome_weaver import Genome, Crossover, Mutation

class PermutationCrossover(Crossover):
    def cross(self, parent1, parent2):
        size = len(parent1)
        start, end = sorted(np.random.choice(size, 2, replace=False))
        
        child1 = [None] * size
        child2 = [None] * size
        
        # Inherit segment
        child1[start:end+1] = parent1[start:end+1]
        child2[start:end+1] = parent2[start:end+1]
        
        # Fill remaining with ordered genes
        child1 = self._fill_remaining(child1, parent2)
        child2 = self._fill_remaining(child2, parent1)
        
        return child1, child2
    
    def _fill_remaining(self, child, parent):
        genes = [g for g in parent if g not in child]
        idx = 0
        for i in range(len(child)):
            if child[i] is None:
                child[i] = genes[idx]
                idx += 1
        return child

# Use custom operator
gw-evolve run --crossover custom.PermutationCrossover --config tsp.yaml
```

### Example 3: Multi-Objective Optimization

Optimize neural network for accuracy and speed.

```python
from genome_weaver import MultiObjectiveEvolution
from genome_weaver.operators import NSGA2

evolution = MultiObjectiveEvolution(
    objectives=[
        ("accuracy", "maximize"),
        ("latency", "minimize"),
        ("params", "minimize")
    ],
    algorithm=NSGA2(),
    population_size=200
)

# Run evolution
population = evolution.run(generations=500)

# Get Pareto front
pareto_front = evolution.get_pareto_front()

# Choose specific solution
best_tradeoff = evolution.choose_solution(
    pareto_front,
    weights=[0.5, 0.3, 0.2]
)

print(f"Selected: accuracy={best_tradeoff.fitness['accuracy']:.3f}, "
      f"latency={best_tradeoff.fitness['latency']:.1f}ms, "
      f"params={best_tradeoff.fitness['params']}")
```

### Example 4: Interactive Evolution

Human-in-the-loop fitness evaluation.

```yaml
# interactive.yaml
evolution:
  type: interactive
  fitness:
    mode: interactive
    display: web
    batch_size: 10
    ranking_method: pairwise  # or absolute
```

```bash
gw-evolve run --config interactive.yaml --interactive
```

Then open http://localhost:8080/rank to provide fitness rankings via pairwise comparisons.

### Example 5: Coevolution

Competitive coevolution for game AI.

```yaml
# coevolution.yaml
evolution:
  type: coevolution
  populations:
    - name: attacker
      size: 50
      genome: neural-network
    - name: defender
      size: 50
      genome: neural-network
  
  fitness:
    evaluation: round_robin
    rounds: 10
  
  coevolution:
    method: competitive
    fitness_sharing: true
```

```bash
gw-evolve run --config coevolution.yaml
```

## API Reference

### Core Classes

```python
from genome_weaver import (
    Evolution,              # Main evolution engine
    Genome,                 # Genome representation
    Population,             # Population management
    FitnessFunction,        # Fitness evaluation
    Selection,              # Selection operators
    Crossover,              # Crossover operators
    Mutation,               # Mutation operators
    HallOfFame,             # Best individuals archive
    Statistics,             # Evolution statistics
    Checkpoint,             # Saving/resuming state
)
```

### Key Methods

```python
# Evolution.run()
evolution.run(
    generations=None,    # Max generations
    fitness=None,       # Target fitness
    stall=None,         # Stall limit
    callback=None       # Generation callback
) -> Genome

# Population.evaluate()
population.evaluate(
    fitness_fn,         # Fitness function
    parallel=True,      # Parallel execution
    workers=4           # Worker count
)

# Genome.mutate()
genome.mutate(
    operator,           # Mutation operator
    rate=0.1,           # Mutation rate
    strength=0.1        # Mutation strength
)

# Genome.crossover()
genome.crossover(
    other,             # Partner genome
    operator,          # Crossover operator
    rate=0.7           # Crossover rate
)
```

## Performance Tips

1. **Use appropriate representation**: Direct encoding for fixed-length genomes, GP trees for variable complexity

2. **Parallelize fitness evaluation**: Most expensive operation; use `--workers` flag

3. **Enable elitism**: Prevents losing best solutions; 5-10 individuals is usually sufficient

4. **Use adaptive operators**: Mutation/crossover rates that adapt to fitness improve convergence

5. **Monitor diversity**: Use `--diversity-metric shannon` to detect premature convergence

6. **Checkpoints save time**: Enable for long runs; use `--resume` to continue

7. **Surrogate models**: For expensive fitness functions, use learned approximations
```