# A Demo of Sleep-Time Compute

This repository demonstrates the "Sleep-time Compute" technique described in the paper ["Sleep-time Compute: Beyond Inference Scaling at Test-time"](https://arxiv.org/pdf/2504.13171) using open-source LLMs.

Google Colab: https://colab.research.google.com/drive/12Itg_XOCP9sRezztBIIRY97QHli0Lpg8?usp=sharing

## Overview

Sleep-time Compute is a technique that improves the efficiency and accuracy of language models by splitting computation into two phases:

1. **Sleep-time Phase**: Pre-compute useful inferences about a context when the model would otherwise be idle
2. **Test-time Phase**: Use these pre-computed inferences to answer queries more efficiently

This approach offers several benefits:
- Reduced latency during query time
- Improved accuracy through deeper context understanding
- Cost efficiency through amortization across multiple queries

## When to Use Sleep-Time Compute

Based on the research findings, Sleep-time Compute is most effective in the following scenarios:

- **Stateful Applications**: Systems where context persists across multiple interactions, such as:
  - Document question-answering
  - Coding assistants operating on shared repositories
  - Conversational agents maintaining dialogue history

- **Predictable Queries**: Contexts where potential questions follow predictable patterns
  - Research shows the performance gap widens with more predictable queries
  - Less effective when queries are difficult to predict or unrelated to the context

- **Multiple Related Queries**: When users ask several questions about the same context
  - Cost efficiency improves as the number of queries increases
  - Research demonstrates a 2.5× decrease in average cost per query with 10 queries per context

- **High-Latency Constraints**: Applications where reducing test-time compute is critical
  - Particularly valuable when test-time tokens are significantly more expensive
  - Can reduce test-time compute needed for the same accuracy by ~5×

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

