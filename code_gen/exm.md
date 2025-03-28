Following query-answer extraction, the code generation step is designed to generate evidence code whose input is only data. This step validates the correctness of the extracted QAs by filtering out those which are irrelevant or inconsistent with the information present in the dataset. Namely, an evidence code cannot be generated for such QAs and they get filtered out. Below is an example scenario where the extracted answer to the query cannot be inferred from the data.

<p align="center">
    <img width="90%" src="https://raw.githubusercontent.com/condabench/condabench_details/refs/heads/main/assets/codegen_filtration_example_1.png">
</p>
