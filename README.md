# SPLASH: Semantic Parsing with Language Assistance from Humans
SPLASH is dataset for the task of semantic parse correction with natural language feedback in the context of text-to-SQL parsing.

![Example](example.png)

The task, dataset along with baseline results are presented in
<br/>[Speak to your Parser: Interactive Text-to-SQL with Natural Language Feedback.]


## Format
Each example contains the following fields:

`db_id`: Name of Spider database.  

`question`: Question (Utterance) as provided in Spider.

`predicted_parse`: The predicted SQL parse by the relevant model.

`predicted_parse_with_values`: The predicted SQL with the values (annonomized in `predicted_parse`) inferred by a rule-based post-processor. Note that we still use Spider's evaluation measure which ignores the values, but inferring values for the predicted parse is essential for generating meaningful explanations. 

`predicted_parse_explanation`: The generated natural language explanation of the predicted SQL.

`feedback`: Collected natural language feedback.

`gold_parse`: The gold parse of the given question as provided in Spider.

`beam`:  The top 20 predictions with corresponding scores produced by Seq2Struct beam search.

Please, refer to the paper for more details.
