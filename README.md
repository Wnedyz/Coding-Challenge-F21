# ACM Research Coding Challenge (Fall 2021)

## [](https://github.com/ACM-Research/Coding-Challenge-F21#no-collaboration-policy)No Collaboration Policy

**You may not collaborate with anyone on this challenge.**  You  _are_  allowed to use Internet documentation. If you  _do_  use existing code (either from Github, Stack Overflow, or other sources),  **please cite your sources in the README**.

## [](https://github.com/ACM-Research/Coding-Challenge-F21#submission-procedure)Submission Procedure

Please follow the below instructions on how to submit your answers.

1.  Create a  **public**  fork of this repo and name it  `ACM-Research-Coding-Challenge-F21`. To fork this repo, click the button on the top right and click the "Fork" button.

2.  Clone the fork of the repo to your computer using  `git clone [the URL of your clone]`. You may need to install Git for this (Google it).

3.  Complete the Challenge based on the instructions below.

4.  Submit your solution by filling out this [form](https://acmutd.typeform.com/to/zF1IcBGR).

## Assessment Criteria 

Submissions will be evaluated holistically and based on a combination of effort, validity of approach, analysis, adherence to the prompt, use of outside resources (encouraged), promptness of your submission, and other factors. Your approach and explanation (detailed below) is the most weighted criteria, and partial solutions are accepted. 

## [](https://github.com/ACM-Research/Coding-Challenge-S21#question-one)Question One

[Sentiment analysis](https://en.wikipedia.org/wiki/Sentiment_analysis) is a natural language processing technique that computes a sentiment score for a body of text. This sentiment score can quantify how positive, negative, or neutral the text is. The following dataset in  `input.txt`  contains a relatively large body of text.

**Determine an overall sentiment score of the text in this file, explain what this score means, and contrast this score with what you expected.**  If your solution also provides different metrics about the text (magnitude, individual sentence score, etc.), feel free to add it to your explanation.   

**You may use any programming language you feel most comfortable. We recommend Python because it is the easiest to implement. You're allowed to use any library/API you want to implement this**, just document which ones you used in this README file. Try to complete this as soon as possible as submissions are evaluated on a rolling basis.

Regardless if you can or cannot answer the question, provide a short explanation of how you got your solution or how you think it can be solved in your README.md file. However, we highly recommend giving the challenge a try, you just might learn something new!


////Explication
The score I obtain was was a 2, meaning neutral, I was expecting more o less a score of 1 which means negative. The text had a poem like structure which makes it harder and more complex to understand with normal text databse. I found a poem database specialy made for sentiment analysis(https://huggingface.co/datasets/poem_sentiment) which was perfect fit for this overall text, sadly my laptop isn't equipped with the necessary requirments for training this databse model so I had to use a pre-trained model of sentiment anayalsis in replacement. I chose a text classification based model call bert that was trained with financial term datase(https://huggingface.co/ProsusAI/finbert). 

BERT uses Semi-supervised encoder bidirectional learning, it's able to understand language patterns of a specific task by training it with theme related databse. Containing 24 layers in the encoder stack with 1024 hidden units and 16 attention heads. BERT "masks" 15% of words in sequence in order to calculate the probability of different words with softmask in this case allowing it to detect the type of sentiment that the context of the mask word provides. After, for sentiment analysis, is similar to Next Sentence Clssification(NSP) where the input are put through Transformer model, then the CLS output becomes a 2X1 vector, that is then gone through another classification layer on top.

I first started by importing the Tokenizer and the pretrained model, I set the token at it's max length of 512. In this ocassion due to the length of the text, I had to divide them into 512 (510 cause need to leave space for CLS and SEP which indicates the start and end of paragraph). The tokenizer then convertes the words into numerical values that can then be encoded into a vector and masked for prediction. I then padded the last division since the length of the text wasn't perfectly divisible by 512. Each 512 paragraph gave three numerical values of being postive, negative, or neutral using softmax. I stack the separated paragraph chunks and put the mask chunks on top. Put the input_dict in model for output. Gathering the probability of each value, and  finally getting the max mean of both paragraphs by using softmax with -1 in dim to access the second dimension where data would be usable. For overall result, take the mean of the paragraph chunks and get overall data, and finally get the arg max of the three. 

Although I predict that if I had trained my own model with the poem sentiment analysis data, the results would have probably be negative since the text contains a lot of argument between two characters. I think this model prediction was more toward neutral because it was fine-tuned with financial terms and literacry, thus normal discussion are generally classified as neutral. 
