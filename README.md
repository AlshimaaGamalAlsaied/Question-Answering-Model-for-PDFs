## Question-Answering Model for PDFs

This project aims to develop an NLP model designed to extract information from various PDF files, specifically annual reports of companies. The goal is to streamline the process of gathering critical information for investors.


## Methodology

We have a set of questions for which we need numeric answers. These answers can be found within the text or within unstructured tables, making the task challenging. 

In the quest for numeric answers within tables, I explored several approaches:

1. **Regular Expressions**: Initially, I attempted to use regular expressions to extract answers ```numeric_answer = re.search(r'\d{1,3}(?:,\d{3})*(?:\.\d+)?', answer["answer"])```. However, this approach did not yield satisfactory results due to the variability in how the context was written in different PDF files.

2. **Large Language Models (LLMs)**: Recognizing the potential of LLMs to provide more accurate answers, aiming to leverage larger models. Unfortunately, resource constraints, specifically memory limitations, preventing from using these larger models effectively. As a result, it is better to resort to smaller models, which provide moderate results. However, the primary challenge remained with answers embedded in tables.

3. **Table Extraction**: To tackle answers located within tables, I explored the extraction of tables from PDF files using the Tabula library. While applying preprocessing and cleaning techniques, it shows that this approach did not yield accurate answers.

Given these challenges, it is better to consider fine-tuning the model itself to improve the accuracy of answers within tables.


### Modeling
The "bert-large-uncased-whole-word-masking-finetuned-squad" model:
* It is a substantial and effective BERT variant, part of the transformer-based family of models. 
* It is notable for its large size and its capacity to capture complex language patterns for question-answering tasks. 
* It performs well in providing accurate answers to questions based on contextual information and is widely used in natural language processing applications, Users can access and employ this model through the Hugging Face Transformers library.


### Results

| Company Name                        | Scope 1 Emissions in Tons | Scope 2 Emissions in Tons (Location based) | Scope 2 Emissions in Tons (Market based) | Scope 3 Emissions in Tons | Total amount of Waste Produced in Tons | Total amount of hazardous waste produced in Tons | Total water usage in Cubic Meter | Total number of Employees |
|------------------------------------|----------------------------|-------------------------------------------|---------------------------------------|---------------------------|-----------------------------------|--------------------------------------------------|--------------------------------|--------------------------|
| Nokia Oyj                          | 116,300                    | 380,200                                   | 263,600                               | 35,595,100                | 7,900                             | 700                                              | 1,299,000                      | 89,078                   |
| Shell PLC                          | -                          | -                                   | -                               | -                     | 2,020k                                 | 2,020K                                           | 171m                           | 554,500                  |
| Bayer AG                           | -                          | 0.11m                                    | 1.5t                                 | -                         |  -                            | 1,000                                            | 1,000                              | -                        |
| Microsoft Corporation               | -                          | 2,697,554                                 | -                                      | -                       | 60k                               | 11b                                             | 200m                              | -                        |
| SAMSUNG ELECTRONICS CO LTD         | -                          | 17,579,000                               | 17,579,000                             | -                         | -                         | 33,093k                                               | -                              | -                        |
| Philip Morris International Inc.    | -                          | -                                         | -                                      | -                         | 143,596                                | 1,423                                               | -                              | 55,393                       |


- Notes:

i. k: thousand, m: million, t: terajoules, b: billion.
<br>
ii. The empty spaces either result in a string or an illogical number when the model returns output.

