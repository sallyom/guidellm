# GuideLLM Example Runs

This directory contains example benchmark runs and analysis tools for GuideLLM performance testing.

## Running Benchmarks in Kubernetes

To run comprehensive GuideLLM benchmarks in Kubernetes, follow the instructions in the [k8s/README.md](../k8s/README.md). This will help you:

- Set up the necessary Kubernetes environment
- Configure benchmark parameters
- Execute the benchmarks
- Collect performance data

## Analyzing Results

### Using the Analysis Script

The [analyze_benchmarks.py](./analyze_benchmarks.py) script processes benchmark YAML output and generates visualizations and statistics. To use it:

1. Install required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

2. Copy the benchmark YAML file from the Kubernetes pod to your local environment:

   ```bash
   # From the k8s/README.md instructions
   kubectl cp <pod-name>:/path/to/benchmark.yaml ./llama32-3b.yaml
   ```

3. Run the analysis script (make sure the YAML file is in the same directory):

   ```bash
   python analyze_benchmarks.py
   ```

The script will:

- Process the benchmark YAML file
- Generate visualizations in the `benchmark_plots` directory
- Create a CSV file with processed metrics
- Print summary statistics

### Example Analysis

The [Llama-3.2-3b-Instruct](./Llama3.2-3b-Instruct) directory contains a complete example of benchmark analysis, including:

- Performance metrics across different concurrency levels
- Visualizations of key metrics
- Detailed README with insights and observations

This example was run on a MiniKube environment with 4x NVIDIA L40S GPUs (AWS instance type g6e.12xlarge).

The example demonstrates how to interpret:
- Request latency
- Time to first token
- Throughput (tokens per second)
- Inter-token latency
- System behavior under various load conditions 

#### View Analysis Locally

To view the generated Llama-3.2-3b-Instruct benchmark plots locally, run

```bash
pip install markdown
python -m markdown Llama-3.2-3b-Instruct/README.md > analysis.html && python -m http.server
```

Then open http://localhost:8000/analysis.html in your browser.
