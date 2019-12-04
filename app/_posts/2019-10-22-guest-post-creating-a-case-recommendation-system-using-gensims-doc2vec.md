---
title: "Guest Post: Creating a Case Recommendation System Using Gensim’s Doc2Vec"
guest-author: "Minna Fingerhood"
---
*This guest post is part of the CAP Research Community Series. This series highlights research, applications, and projects created with Caselaw Access Project data.*

*Minna Fingerhood graduated from the University of Pennsylvania this past May with a B.A. in Science, Technology, and Society (STSC) and Engineering Entrepreneurship. She is currently a data scientist in New York and is passionate about the intersection of technology, law, and data ethics.*

The United States Criminal Justice System is the largest in the world. With more than 2.3 million inmates, the US incarcerates more than [25% of the world’s prison population](https://www.aclu.org/issues/smart-justice/mass-incarceration), even as its general population only accounts for 5%. As a result, and perhaps unsurprisingly, the system has become increasingly congested, inefficient, and at times indifferent. 

The ramifications of an overpopulated prison system are far-reaching: from violent and unsanitary prison conditions; to [backlogged criminal courts](https://www.newyorker.com/magazine/2014/10/06/before-the-law); to overworked and often overwhelmed public defenders. These consequences are severe and, in many cases, undermine the promise of fair and equal access to justice. In an effort to help address these challenges, the government has employed various technologies that aim to increase efficiency and decrease human bias throughout many stages of the system. While these technologies and innovations may have been implemented with earnest intentions, in practice, they often serve bureaucratic imperatives and can reinforce and magnify the bias they intend to eliminate.  

Given this context, it is particularly important to emphasize technologies that serve to democratize and decentralize institutional and governmental processes, especially in connection with the Criminal Justice System as each decision carries enormous gravity. Therefore, with the help of the Caselaw Access Project (CAP), I have developed a legal case recommendation system that can be used by underserved defendants and their attorneys. 

This effort was inspired by the work of the Access to Justice Movement, which uses data to lower barriers to the legal system, as well as by the landmark Supreme Court decision [Gideon vs. Wainwright (1963)](https://www.oyez.org/cases/1962/155), which guarantees underserved defendants the right to counsel under the Sixth Amendment. As Justice Black wrote in the majority opinion for this case: “[The American Constitution is] designed to assure fair trials before impartial tribunals in which every defendant stands equal before the law. This noble ideal cannot be realized if the poor man charged with crime has to face his accusers without a lawyer to assist him.” While this case afforded poor defendants the right to free counsel, the meaning of ‘fair trial’ has become compromised in a system where a public defender can have, on average, over [200 cases](https://www.nytimes.com/interactive/2019/01/31/us/public-defender-case-loads.html).  

My case recommendation system attempts to empower defendants throughout this flawed process by finding the 15 cases most similar to their own based primarily on text. In theory, my application could be made available to individuals awaiting trial, thereby facilitating their own thoughtful contributions to the work of their public defender. These contributions could take many forms such as encouraging the use of precedent cited in previously successful cases or learning more about why judges deemed other arguments to be unconvincing. 

![My application hosted locally through Plotly Dash.](https://lil-blog-media.s3.amazonaws.com/Screen_Shot_2019-10-22_at_11.00.47_AM.png)

My project primarily relies on natural language processing as I wanted to match cases through text. For this, I chose to use the majority opinion texts for cases from 1970 to 2018. I used majority opinion text as it was available in the CAP dataset, but in the future I look forward to [expanding beyond the scope](https://case.law/about/#scope-limits) of CAP to include text from news reports, party filings, and even case transcripts. Further, while 1970 is a fairly arbitrary cut-off date, it also marks the year in which the term “War on Drugs” was coined. From this time forward, the prison system rapidly evolved into one marked by mass incarceration. I believed this would be useful for criminal court case data. Lastly, the data does not include cases subsequent to June of 2018, because the CAP dataset does not contain volumes past this date.

In creating semantic meaning from the text, I used Doc2Vec (through Python’s Gensim package), a derivative of the more well-known Word2Vec. This method of language processing relies on a shallow neural net to generate document vectors for every court case. Vectors are created by looking at word embeddings, or the location of words relative to other words, creating an understanding of language for the computer. These vector representations of case text can be compared to all other document vectors using cosine similarity to quantify likeness. 

![Example: a PCA representation of chosen words in my Gensim Doc2Vec model. Note: I adjusted my output vectors to have a length of 300.](https://lil-blog-media.s3.amazonaws.com/Screen_Shot_2019-10-22_at_10.32.50_AM.png)

In addition to text, I included the year of the majority decision as a feature for indicating similarity, but in a smaller proportion at 7% of the weight given to cosine similarity for word vectors. In a scenario where two cases were equally textually similar to a sample case, I wanted the more recent one to appear first, but did not want date to overshadow text similarity. 

I believe this project is a promising starting point for educating and empowering underserved defendants. The CAP dataset is a rich and expansive resource, and much more can be done to further develop this project. I am looking forward to including more text into the program as a means of increasing accuracy for my unsupervised model and providing the user with more informative resources. I also believe that creating additional optional parameters for recommendation, such as geography or individual judges, could substantially improve the efficacy of this search engine. Ultimately, I look forward to collaborating with others to expand this project so that individuals caught within the criminal justice system can better use technology as a tool for empowerment and transparency, thereby creating more opportunities for fairness and justice. 

In that regard, I have posted additional information regarding this project on my GitHub at [https://github.com/minnaf/Case_Recommendation_System](https://github.com/minnaf/Case_Recommendation_System). Please contact me if you are interested in collaborating or learning more at [minnaf@sas.upenn.edu](mailto:minnaf@sas.upenn.edu).