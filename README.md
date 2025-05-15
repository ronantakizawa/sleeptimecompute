# A Demo of Sleep-Time Compute

This repository contains a demonstration of the "Sleep-time Compute" technique described in the paper ["Sleep-time Compute: Beyond Inference Scaling at Test-time"](https://arxiv.org/abs/2401.12200). The implementation uses Mistral-7B-Instruct-v0.1, an open-source large language model.

## Overview

Sleep-time Compute is a technique that improves the efficiency and accuracy of language models by splitting computation into two phases:

1. **Sleep-time Phase**: Pre-compute useful inferences about a context when computational demands are lower
2. **Test-time Phase**: Use these pre-computed inferences to answer queries more efficiently

This approach offers several benefits:
- Reduced latency during query time
- Improved accuracy through deeper context understanding
- Cost efficiency through amortization across multiple queries

## Implementation Details

This demo implements Sleep-time Compute using:
- **Mistral-7B-Instruct-v0.1**: A powerful open-source language model
- **Hugging Face Transformers**: For model loading and inference
- **Custom prompting strategies**: Specially designed for the Mistral instruction format

The code demonstrates:
- Setting up the model with appropriate configurations
- Implementing the sleep-time and test-time phases
- Visualizing the benefits through token usage and accuracy metrics
- Multi-query amortization to show efficiency gains

## Key Features

- **Two-Phase Approach**: Clear separation between sleep-time and test-time computation
- **Variable Verbosity**: Control the level of detail in responses
- **Performance Comparison**: Analysis of regular vs. sleep-time compute approaches
- **Visualization**: Graphs showing efficiency gains and amortization benefits

## Results

The implementation demonstrates:
1. **Test-time Efficiency**: Significant reduction in tokens needed at query time
2. **Accuracy Improvements**: More reliable answers through pre-computed inferences
3. **Cost Amortization**: Greater efficiency as the number of queries increases

## Getting Started

To run this demo:

1. Install the required dependencies:
```bash
pip install transformers torch datasets matplotlib tqdm accelerate
```

2. Run the notebook to see Sleep-time Compute in action

3. Experiment with different contexts and queries to observe the benefits

## Requirements

- Python 3.6+
- PyTorch
- Transformers
- Matplotlib
- tqdm
- Accelerate

## Acknowledgements

This implementation is based on the paper "Sleep-time Compute: Beyond Inference Scaling at Test-time". The demo uses the Mistral-7B-Instruct-v0.1 model, an open-source large language model.

## License

This project is provided as an educational demonstration. Please refer to the Mistral-7B-Instruct-v0.1 license for usage restrictions related to the underlying model.
