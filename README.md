# ConDABench
<p align="center">
    <img width="80%" src="https://raw.githubusercontent.com/condabench/condabench_details/refs/heads/main/assets/overall.png">
</p>
ConDABench is a collection of conversational data analysis (ConDA) problems derived from diverse sources. We developed a multi-agent architecture for creating challenging data analysis benchmarks. The key feature of our approach is that the benchmarks are validated in four ways: (1) the data analysis question-answer (QA) pairs are extracted from real-world data analysis articles that are accompanied by source datasets, (2) the QA pairs are reviewed by a Reviewer agent checks the quality and correctness of the generated pairs, (3) the QA pairs are further validated by generating code that produces evidence for the answer from the source dataset, and (4) a final validation step is performed by a Reviewer agent that checks for coherence of the question-answer pair, the code, the dataset, and the execution results. We also provide a multi-agent evaluation framework that can evaluate advanced data analysis (ADA) tools on CoDABench. The framework measures the conversationality and quality of solutions, beyond just exact match. Specifically we provide a user proxy that helps evaluate multi-turn interactive data analysis tools by conversing with the external DA tool similar to a human. 
The DA tool's response is recorded and is evaluated against correctness (Correctness Score) and conversation quality (Conversation Score) for a given query and data file(s).

# Benchmark Construction

## Curation
<p align="center">
    <img width="40%" src="https://raw.githubusercontent.com/condabench/condabench_details/refs/heads/main/assets/curation.png">
</p>
The first phase involves the curation of question-answer (QA) pairs. These pairs are extracted from real-world data analysis articles, ensuring that they are derived from authentic and practical sources. The QA pairs are then reviewed by a reviewer agent to check the quality and correctness, ensuring that the benchmarks are reliable and accurate.
<br><br>

> [!NOTE]
> The prompts for both the Curator agent and the Reviewer agent are available [here](https://github.com/condabench/condabench_details/blob/main/curation/curator_reviewer.md). Both agents are powered by GPT-4o.

## Code Generation
<p align="center">
    <img width="40%" src="https://raw.githubusercontent.com/condabench/condabench_details/refs/heads/main/assets/code_generation.png">
</p>
In the second phase, code is generated to provide evidence for the answers derived from the curated QA pairs. This involves generating and reviewing scripts that can access the source dataset and produce the necessary results to support the provided answers. The generated code is then validated to ensure that it accurately performs the intended data analysis. This validation helps mitigate any potential errors in the curated QAs from the previous stage.
<br><br>

> [!NOTE]
> The prompts for both the Code Generator agent and the Reviewer agent are available [here](https://github.com/condabench/condabench_details/blob/main/code_gen/code_gen_reviewer.md). Both agents are powered by GPT-4o.

## External Tool Evaluation
<p align="center">
    <img width="40%" src="https://raw.githubusercontent.com/condabench/condabench_details/refs/heads/main/assets/evaluation_phase.png">
</p>
We employ a multi-agent workflow to evaluate Conversational DA tools and test them on the basis of answer correctness and conversational proficiency. To automate evaluation of such conversational tools, we first simulate a conversation using a user-proxy, then evaluate the responses obtained.

### Simulation
We define a user-proxy agent which simulates a conversation with an external DA tool when it tries to find a solution to the query asked.
In order to evaluate a DA tool, you should first run this workflow and then proceed towards the evaluation script.

### Evaluation
After the simulation stage, we run evaluation to get the correctness and conversation quality score.
