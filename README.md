# Knowledge Extraction with open-source LLMs

E.ON as every big organization strives for reliable Knowledge Extraction and Management from analogue and digital documents.
On the market, there are many competitors for commercial solutions.
E.ON partners with Microsoft Azure incorporating Azure OpenAI models into its platform (E.ON GPT) and a familily of custom solutions.
Additinally, E.ON consideres other commercial models from big players like Amazon and Google.

Current situation presents a set of challeges:
- commercial offerings are limited in deployable capacity, it is not always possible to get requested bandwith (tokens-per-minute) for acceptable User experience;
- evaluated solutions are expensive, and the costs rise with the number of users;
- it is difficult to adapt models, finetuning is restricted or even not possible;
- the is no way to host own specialized model based on a foreign base model.


This study evaluates BERT, RoBERTa, and ALBERT on question answering using the SQuAD 1.0 and SQuAD 2.0 datasets.

## Data Sheet

Here is the examples of data:

Valid questions SQuAD 1.0:
```json
{
  "title": "Beyoncé",
  "paragraphs": [
    {
      "qas": [
        {
          "question": "When did Beyonce start becoming popular?",
          "id": "56be85543aeaaa14008c9063",
          "answers": [
            {
              "text": "in the late 1990s",
              "answer_start": 269
            }
          ],
          "is_impossible": false
        },
        {
          "question": "What areas did Beyonce compete in when she was growing up?",
          "id": "56be85543aeaaa14008c9065",
          "answers": [
            {
              "text": "singing and dancing",
              "answer_start": 207
            }
          ],
          "is_impossible": false
        }
      ],
      "context": "Beyoncé Giselle Knowles-Carter (/biːˈjɒnseɪ/ bee-YON-say) (born September 4, 1981) is an American singer, songwriter, record producer and actress. Born and raised in Houston, Texas, she performed in various singing and dancing competitions as a child, and rose to fame in the late 1990s as lead singer of R&B girl-group Destiny's Child. Managed by her father, Mathew Knowles, the group became one of the world's best-selling girl groups of all time. Their hiatus saw the release of Beyoncé's debut album, Dangerously in Love (2003), which established her as a solo artist worldwide, earned five Grammy Awards and featured the Billboard Hot 100 number-one singles \"Crazy in Love\" and \"Baby Boy\"."
    }
  ]
}
```

Artificial questions SQuAD 2.0 :
```json
{
  "qas": [
    {
        "plausible_answers": [
            {
                "text": "November 2006",
                "answer_start": 569
            }
        ],
        "question": "When could GameCube owners purchase Australian Princess?",
        "id": "5a8d7bf7df8bba001a0f9ab4",
        "answers": [],
        "is_impossible": true
    },
    {
        "plausible_answers": [
            {
                "text": "2005",
                "answer_start": 364
            }
        ],
        "question": "What year was the Legend of Zelda: Australian Princess originally planned for release?",
        "id": "5a8d7bf7df8bba001a0f9ab5",
        "answers": [],
        "is_impossible": true
    }
],
  "context": "The Legend of Zelda: Twilight Princess (Japanese: ゼルダの伝説 トワイライトプリンセス, Hepburn: Zeruda no Densetsu: Towairaito Purinsesu?) is an action-adventure
game developed and published by Nintendo for the GameCube and Wii home video game consoles. It is the thirteenth installment in the The Legend of Zelda series. Originally planned for
 release on the GameCube in November 2005, Twilight Princess was delayed by Nintendo to allow its developers to refine the game, add more content, and port it to the Wii. The Wii ver
sion was released alongside the console in North America in November 2006, and in Japan, Europe, and Australia the following month. The GameCube version was released worldwide in Dec
ember 2006.[b]"
}
```

## Implimentations

The challenge is built around one main NLP task: Question Answering over unstructured textual Data.

Complexity levels:

- Level 0: Choose one open-source LLM, use it AS IS for Answer generation given questions from the dev part of SQuAD 1.0 and evaluate it using the provided evaluation script.ompare several (3) models in their raw performance.

  For level O implementation by using BERT, see Level0-BERT.ipynb
  For level O implementation by using albert, see Level0-albert.ipynb
  For level O implementation by using Roberta, see Level0-roberta.ipynb
  
  
- Level 1: On SQuAD 1.0 (only valid questions) use the chosen LLM and augment the retrieval by means of model finetuning and/or RAG technique, calculate F1 for comparison.

  For level 1 implementation by using BERT, see Level1_implementation_BERT.ipynb
  For level 1 implementation by using albert, see Level1_implementation_albert.ipynb
  For level 1 implementation by using Roberta, see Level1_implementation_RoBERTa.ipynb
  
- level 1+: Compute not only the F1 metric, but also BLUE and an other appropriate metric (research question), compare the results.
  see evaluation.ipynp to get blue and rouge scores


- Level 3: On SQuAD 2.0 (valid and imaginary questions) employ results of the previous level with indication to imaginary answers.
  
  For level 3 implementation by using RoBERTa BASE, see Level3_implementation_roberta_base.ipynb
  For level 3 implementation by using RoBERTa Large, see Level3_implementation_roberta_large.ipynb

- As a solution, please refer to file: Level3_implementation_roberta_large.ipynb which a basic user interface provided. 

Besides fine-tuning, RAG is a technique widely used in knowledge extraction. We combined our fine-tuned roberta large model with RAG architecture. As a proof-of-concept, see  Proof-of-Concept-Roberta-RAG-Collaboration.ipynb

Project Contributors:
Fabian Arnold
Tugce Caglayan
Seyma Cakir
Ozlem Senel 
Ozgur Kaan Varlik
