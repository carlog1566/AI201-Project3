# Project 3 Planning


## Community

### r/LetsTalkMusic

I chose r/LetsTalkMusic because it is a discussion-focused music community where users post long-form opinions, critiques, questions, historical discussions, and recommendations about different artists, genres, albums, and solos. The community encourages thoughtful conversation which makes it well suited for a text classification task. The wide range of discussion quality like detailed analysis to simple personal opinions creates meaningful distinctions that the classifier can learn from.


## Labels

### Review

**Definition:** A post that evaluates or critiques a specific album, artist, or musical work using the author's opinions and observations

**Example 1: "Olivia Rodrigo's New Album"**
- The author critiques the album's concept, songwriting, lyrical maturity, and overall execution.

**Example 2: "Never Mind the Bollocks, Here's the Sex Pistols"**
- The author reviews the album while discussing its musical strengths, history, and impact.

**Uncertain Example: "What do people here think of the new BTS album Arirang?"**
- It is uncertain because although the title asks for other's opinions, the author spends most of the post explaining that they do not like the allbum and think that it is very derivative. I would still classify it as Review since the main focus is on evaluating the album.

### Discussion

**Definition:** A post where the author shares a personal opinion or starts a discussion about music-related ideas, habits, or culture without reviewing one specific work.

**Example 1: "Why Do People Act Like Their Opinion on Music Is A Fact?"**
- The author discusses subjectivity in music and encourages conversation.

**Example 2: "I do not understand wanting to hear an album again for the first time"**
- The author explains their personal listening philosophy and asks others what they think.

**Uncertain Example: "How did you "discover" your favorite bands?"**
- The title is phrased as a question, but the author mainly shares a personal story and encourages others to do the same. I would classify it as Discussion because its goal is to start a conversation rather than obtaining a specific answer.

### Question

**Definition:** A post whose primary purpose is asking the community an open-ended question or seeking information.

**Example 1: "How frequently do you listen to new albums?"**
- The author asks about other people's listening habits.

**Example 2: "Is there a sense of what "reddit music taste" entails?"**
- The author asks the community to explain an idea they are curious about.

**Uncertain Example: "Do Folks Really Have a Difficult Time with Kate Bush?"**
- The author briefly shares their own experience before asking why others struggle with Kate Bush's music. I would classify it as Question because the primary goal is hearing others' perspectives.

### Analysis

**Definition:** A post that examines music history, trends, genres, production, or artistic ideas using reasoning, evidence, or background information.

**Example 1: "Were Jimmy Cauty and Alex Paterson ambient music's great lost partnership?"**
- The author analyzes the musicians' creative partnership and influence.

**Example 2: "What happened to the relationship between pop stars and rap?"**
- The author explores changes in collaboration trends between pop and rap artists.

**Uncertain Example: "What do you think of when band members go solo? Do you think there is any way it can work out afterwards?"**
- The author asks a question, but most of the post develops a detailed analysis of why solo careers affect bands. I would classify it as Analysis because the reasoning drives the discussion.


## Hard Edge Cases

The hardest distinction is between Discussion and Question since many posts begin with a question but most of the post is written based on the author's own point of view. 

For example, "Why Do People Act Like Their Opinion on Music Is A Fact?" is written as a question, but its main purpose is to express the author's opinon and using a question to only encourage discussion. To handle these cases consistently, I will classify the posts based on their primary purpose:
- If the author mainly presents their own argument or perspective, I will label it as Discussion
- If the author mainly seeks responses or information from others, I will label it as Qeustion


## Data Collection Plain

I will collect examples from r/LetsTalkMusic using Reddit's public API and or directly scraping publicly visible posts from the subreddit feed. I will prioritzize posts with full discussion threads to ensure enough context for the labeling.

I will aim for at least 200 total posts and try to split it envenly across the 4 labels:
- Review: 50 posts
- Discussion: 50 posts
- Question: 50 posts
- Analysis: 50 posts

If a label is underrepresented, I will expand the collection window by:
- Going further back in the subreddit
- Include more shorter posts

If after reaching 200 total examples and the dataset is still imbalanced, I will:
- Keep the full dataset for training
- Use stratified sampling for evaluation splits


## Evaluation Metrics
I will use multiple metrics due to dealing with multi-class text classification:
- Accuracy: Measures overall correctness of predictions, useful as a baseline
- Precision (per class): Measures how many posts predicted as a label actually belong to that label. Important for ensuring the classifier does not over-assign common labels
- Recall (per class): Measures howmany true posts of a label are correctly identified. Important for detecting whether the model is missing any harder categories
- F1-score: Balances precisiona nd recall equally across all labels. Very important since it prevents large classes from dominating performance
- Confusion Matrix: Helps identify systematic confusion between the labels, useful visualization