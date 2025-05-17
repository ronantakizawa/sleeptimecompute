# A Demo of Sleep-Time Compute to Reduce LLM Latency
<img width="942" alt="Screenshot 2025-05-17 at 10 56 31 AM" src="https://github.com/user-attachments/assets/54f2d597-d15e-4c29-ad44-eb61a9375516" />

This repository demonstrates the "Sleep-time Compute" technique described in the paper ["Sleep-time Compute: Beyond Inference Scaling at Test-time"](https://arxiv.org/pdf/2504.13171) using open-source LLMs.

Google Colab: [https://colab.research.google.com/drive/12Itg_XOCP9sRezztBIIRY97QHli0Lpg8?usp=sharing](https://colab.research.google.com/drive/12MFTFs9YMoOL-znKgYBY5heoEl9qm8AZ?usp=sharing)

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

## When Not to Use Sleep-Time Compute

Sleep-time Compute may not be beneficial in these scenarios:

- **Unpredictable Queries**: When questions are difficult to anticipate from the context
  - The research shows diminishing returns for less predictable queries
  - Standard test-time compute may be more effective in these cases

- **Single Query Scenarios**: With only one question per context
  - The overhead of sleep-time compute isn't amortized
  - Cost efficiency significantly drops without multiple related queries

- **High Test-Time Budget Settings**: In applications where extensive test-time compute is already allocated
  - Research shows standard test-time compute can sometimes outperform sleep-time compute when sufficient test-time resources are available

- **Non-Stateful Applications**: Systems where context doesn't persist between interactions
  - Without a persistent context to analyze during idle time, the core benefit is lost

- **Rapidly Changing Contexts**: Environments where the context is frequently updated
  - Pre-computed inferences may quickly become outdated

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

<img width="541" alt="Screenshot 2025-05-17 at 10 57 27 AM" src="https://github.com/user-attachments/assets/6b7e1093-8afb-4d4f-830f-7d774a0c3ee0" />


<img width="529" alt="Screenshot 2025-05-17 at 10 57 48 AM" src="https://github.com/user-attachments/assets/c4e0255e-6537-449f-8942-570268dea723" />
