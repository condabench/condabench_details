### Failure Analysis

<p align="center">
    <img width="90%" src="https://raw.githubusercontent.com/condabench/condabench_details/refs/heads/main/assets/failure_analysis.png">
</p>

The figure above compares the manifestation of different types of failures for `4o` and `o1` models.

### Error Categories
Here are the major cohorts that we observed:

1. **Logical Reasoning Failures**: Flaws in logical reasoning or incomplete inferencing.
2. **Contextual Misinterpretations**: Misinterpretation or lack of fidelity to the given context.
3. **Instruction Compliance Issues**: Failure to follow user instructions.
4. **Data Processing Errors**: Mistakes in statistical computations or data interpretation.
5. **Response Generalization Issues**: Overgeneralized or ambiguous responses.
6. **Information Hallucinations**: Generation of information that is not based on the input or reality.
7. **Temporal Consistency Issues**: Difficulty in maintaining consistency over long conversations.
8. **Ambiguity Handling Failures**: Struggles to resolve ambiguities without additional context or clarification.

### Execution Error Analysis

<p align="center">
    <img width="90%" src="https://raw.githubusercontent.com/condabench/condabench_details/refs/heads/main/assets/execution_error_analysis(resolved-unresolved).png">
</p>

The graph shows the distribution of `resolved` and `unresolved` errors across different models.

#### Resolved and Unresolved Errors
Resolved errors refer to those errors that initially occurred but were subsequently corrected during the conversation between `User Proxy` and the external DA tool, leading to error free response. Unresolved errors are those that were not corrected, potentially causing failures.

The variation in errors across different models and categories can be quite significant. Generally, a substantial proportion of errors are resolved, indicating a relatively high rate of error correction and efficacy of `User Proxy`.
