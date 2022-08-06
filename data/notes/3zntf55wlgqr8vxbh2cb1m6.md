## General Info

NLP enables you to create software that can:

- Analyze and interpret text in documents, email messages, and other sources.
- Interpret spoken language, and synthesize speech responses.
- Automatically translate spoken or written phrases between languages.
- Interpret commands and determine appropriate actions.

## Natural language processing in Microsoft Azure

<table aria-label="Natural language processing in Microsoft Azure" class="table">
<thead>
<tr>
<th>Service</th>
<th>Capabilities</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Language</strong></td>
<td>Use this service to access features for understanding and analyzing text, training language models that can understand spoken or text-based commands, and building intelligent applications.</td>
</tr>
<tr>
<td><strong>Translator</strong></td>
<td>Use this service to translate text between more than 60 languages.</td>
</tr>
<tr>
<td><strong>Speech</strong></td>
<td>Use this service to recognize and synthesize speech, and to translate spoken languages.</td>
</tr>
</tbody>
</table>

## Microsoft Luis Demo

[Microsoft Luis](https://aidemos.microsoft.com/luis/demo)

Conversational AI in Microsoft Azure

<table aria-label="Conversational AI in Microsoft Azure" class="table">
<thead>
<tr>
<th>Service</th>
<th>Capabilities</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>QnA Maker</strong></td>
<td>This cognitive service enables you to quickly build a <em>knowledge base</em> of questions and answers that can form the basis of a dialog between a human and an AI agent.</td>
</tr>
<tr>
<td><strong>Azure Bot Service</strong></td>
<td>This service provides a platform for creating, publishing, and managing bots. Developers can use the <em>Bot Framework</em> to create a bot and manage it with Azure Bot Service - integrating back-end services like QnA Maker and LUIS, and connecting to channels for web chat, email, Microsoft Teams, and others.</td>
</tr>
</tbody>
</table>

## Conversational AI

While many organizations publish support information and answers to frequently asked questions (FAQs) that can be accessed through a web browser or dedicated app. The complexity of the systems and services they offer means that answers to specific questions are hard to find. Often, these organizations find their support personnel being overloaded with requests for help through phone calls, email, text messages, social media, and other channels.

A Language Understanding application defines a model consisting of intents and entities. Utterances are used to train the model to identify the most likely intent and the entities to which it should be applied based on a given input.

### Utterances

An utterance is an example of something a user might say, and which your application must interpret. *Ex: ("Switch the fan on." or "Turn on the light.")*

### Entities

An entity is an item to which an utterance refers. *Ex: ("Switch the **fan** on." or "Turn on the **light**."*)

### Intents

An intent represents the purpose, or goal, expressed in a user's utterance. For example, for both of the previously considered utterances, the intent is to turn a device on; so in your Conversational Language Understanding application, you might define a TurnOn intent that is related to these utterances.

The intent should be a concise way of grouping the utterance tasks. Of special interest is the None intent. You should consider always using the None intent to help handle utterances that do not map any of the utterances you have entered. The None intent is considered a fallback, and is typically used to provide a generic response to users when their requests don't match any other intent.

## Text Analysis

Text analytics is a process where an artificial intelligence (AI) algorithm, running on a computer, evaluates these same attributes in text, to determine specific insights. A person will typically rely on their own experiences and knowledge to achieve the insights. A computer must be provided with similar knowledge to be able to perform the task. There are some commonly used techniques that can be used to build software to analyze text, including:

- Statistical analysis of terms used in the text. For example, removing common "stop words" (words like "the" or "a", which reveal little semantic information about the text), and performing frequency analysis of the remaining words (counting how often each word appears) can provide clues about the main subject of the text.
- Extending frequency analysis to multi-term phrases, commonly known as N-grams (a two-word phrase is a bi-gram, a three-word phrase is a tri-gram, and so on).
- Applying stemming or lemmatization algorithms to normalize words before counting them - for example, so that words like "power", "powered", and "powerful" are interpreted as being the same word.
- Applying linguistic structure rules to analyze sentences - for example, breaking down sentences into tree-like structures such as a noun phrase, which itself contains nouns, verbs, adjectives, and so on.
- Encoding words or terms as numeric features that can be used to train a machine learning model. For example, to classify a text document based on the terms it contains. This technique is often used to perform sentiment analysis, in which a document is classified as positive or negative.
- Creating vectorized models that capture semantic relationships between words by assigning them to locations in n-dimensional space. This modeling technique might, for example, assign values to the words "flower" and "plant" that locate them close to one another, while "skateboard" might be given a value that positions it much further away.
