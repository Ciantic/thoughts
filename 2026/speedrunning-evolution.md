---
date: 2026-09-01
url: https://ciantic.iki.fi/2026/speedrunning-evolution/
---

# Training is speedrunning evolution

We aren't born with blank brains, but instead with sophisticated equipment to handle all kinds of inputs. This equipment was created for us during millions of years of evolution, we don't just magically learn language; we have systems in our brains to structure and understand language. Systems for distinguishing shapes and sounds, feel and taste things. When LLMs are trained, they don't only learn what we do after birth, but they also have to first go through evolutionary steps, to achieve what we can do.

This post is about Robert Wright's latest book [The God Test: Artificial Intelligence and Our Coming Cosmic Reckoning](https://thegodtest.net/). He is known for evolutionary psychology among other things, and while the book covers a lot more than similarities with LLMs and our brains, this post is only about that part. He gives three examples of the similarities. The first is the meaning of words, which is evidently important for mastering language. The second is example from the visual cortex, where we are known to have specific neurons for detecting edges. The third one is a bit harder to identify: theory of mind.

I find the visual cortex example most compelling, because we can observe via imaging that human brains have developed similar functionality. Whereas the conceptual examples of meaning of words, and theory of mind are harder to verify. I will go through them the way they are introduced in the book.

Meaning of words can be seen as multidimensional semantic space. One dimension, as Robert Wright illustrates, could be lethality, one could be speed, or size and so on. There can be innumerable amount of dimensions, and LLMs during their training construct this kind of mapping. Nobody has given LLMs a task to figure out meaning of words, but it raises out of the task of predicting the next word.

> Suppose you make a graph, with an x and y axis, on which to map the words for various animals. The x axis—the horizontal axis—is labeled “degree of lethality,” and the y axis is labeled “speed.” Both a rattlesnake and a tiger would have pretty high x values, but the tiger would have a much higher y value. So you might plot these as: rattlesnake (8,3); tiger (10,10). And a scorpion might be, say, (5,2). You could keep adding dimensions to your map; the z axis could represent size, for example. [page 18]
> 
> [...]
> 
> Some psychologists think that this method of linking words to meaning—locating them in a kind of multidimensional semantic space—is the same method human brains use. But we don’t really know how the brain does the linking. However, it seems safe to say *that* the brain does the linking. So this generic feature—some way of representing the meaning of words—is a feature that large language models have in common with the human brain.
> 
> That’s what I mean when I say neural networks can “reinvent” features of the human brain; they build structures of information processing that perform cognitive functions performed by the brain, whether or not their way of performing that function is identical to the brain’s. And this particular function—mapping words onto meaning—is, needless to say, an important one. [page 19]

It is much harder to say do our brains use similar mapping as LLMs, to me it seems plausible given that it could also be the most efficient way to compress the information by colocating and connecting concepts with similar meaning. Interestingly we know where meaning of words is stored in the brain. In humans [Wernicke's area](https://en.wikipedia.org/wiki/Wernicke%27s_area) is responsible for assigning meaning to words, and certain kind of brain damage can cause human to talk nonsense but syntactically sensible way. Language is of course much more than meaning of words, but it is harder to pinpoint the rest of the functionality.

Second example is from visual cortex:

> Our brains have an “edge detection mechanism” that helps us identify the edges of tables and buildings and tree trunks and the like. The mechanism includes neurons in the visual cortex that fire when they detect a line of contrast with a certain orientation. So one neuron might fire strongly for lines that are at a forty-five-degree angle but weakly for a sixty-degree line, whereas another neuron might do the reverse.
> 
> And it turns out that neural networks, in the course of training to identify images, develop things called “edge detection filters” that function the same way, with different filters specializing in different angles. As Claude put it during one of our conversations, “Think of it like evolution discovering the same solution multiple times—just as edge detection emerged in biological vision systems, it also emerges in artificial neural networks because it’s such an efficient way to begin processing visual information.”
> 
> The edge detection neurons in the human brain have one other property worth mentioning: Though they are a product of evolution, and thus rooted in our genes, their full functioning depends on early experience. The same goes for the neuronal connections I started this chapter with—the ones whose strengthening, via evolution, helped give us our language skills. They are also strengthened, selectively, as a child’s linguistic skills develop, and that strengthening helps the child master not just language but the specific features of the local language. This is another reminder that the training of a neural network is at once a process of evolution and of learning; it has things in common with the maturation of the human species and things in common with the maturation of a human brain. [page 60]

What makes this example compelling is the evidence, you show people pictures and see what parts of the brain "lights up". Given that different angled lines have distinct neurons, we can conculed that indeed similar functionality must exist. It likely is also the case, that this is obvious solution for image recognition in neural networks, so both natural selection and LLMs discovered it independently. We developed edge detection neurons via evolution's trial and error during our path from single celled ocelloid to human eye, while LLMs discovered it by training on vast datasets.

Third example is [theory of mind](https://en.wikipedia.org/wiki/Theory_of_mind). Ones ability to attribute different mental states for someone else. It appears as theory of mind formed in ChatGPT 4 for the first time:

> Michal Kosinski had given GPT-4, GPT-3.5, and earlier versions of GPT a classic theory of mind test known as the “false belief” test. It has questions like this: If there’s a bag full of popcorn that’s labeled “chocolate,” what will someone who can see the label but can’t see the contents of the bag think it contains? Kosinski found that, whereas GPT-3, released in 2020, had answered 40 percent of the false belief questions correctly, GPT-4 had racked up a 95 percent score. [page 116]

Robert Wright also came up his own test, which he tested on ChatGPT 4:

> First, I posed ChatGPT with this situation: “A teacher asks the class a question and a student volunteers an answer and the teacher says, ‘Well, I guess I’ve heard worse answers, but I can’t remember when.’ ”
> 
> When I asked the chatbot what it thought the student was “feeling and/or thinking,” it laid out several possibilities, starting with, “the student might feel embarrassed, disheartened, or upset due to the teacher’s response, which seems to be critical and sarcastic.” I zeroed in on that possibility and followed up by asking what other students in the class were likely feeling or thinking. ChatGPT began by noting that the students’ reactions would depend on “their individual personalities, relationships with the teacher and the student who answered, and their own experiences.” Then it listed possible reactions in what struck me as roughly their order of likelihood.
> 
> Empathy or sympathy.
> Discomfort or awkwardness.
> Fear or anxiety.
> And so on—all the way down to “Amusement.” After each reaction, the AI offered elaboration. After “Fear or anxiety,” for example, it said, “Some students might feel anxious or fearful about volunteering answers themselves, worried that they could receive similar negative feedback from the teacher.”
> 
> Then I asked my toughest question: “Suppose there’s a student in the class who is romantically attracted to the girlfriend of the student who is feeling embarrassed and disheartened. What do you think this student is feeling and/or thinking?”
> 
> ChatGPT said the student could have a mixture of feelings. And, once again, the first feeling it listed struck me as the most likely—the most likely by a long shot. “Schadenfreude,” it said, invoking the word that was imported from German because no single English word captured the idea of taking pleasure in the suffering of others. The bot then added, “This student may feel a sense of satisfaction or pleasure from seeing the other student embarrassed, thinking that it might lower the other student’s social standing or make the girlfriend reconsider their relationship.”
> 
> Okay, I rest my case. The evidence that cognitive empathy—or theory of mind or whatever you want to call it—is an emergent property of large language models seems to me compelling. But “emergent property” makes the whole thing sound a little spookier than I think it is. I think cognitive empathy just evolves, like so many other cognitive capacities, in the course of an LLM’s training.
> 
> After all, that’s how it seems to have worked in our species. Evolutionary psychologists say that natural selection built a kind of theory of mind “module” into the human brain because it helped people predict the behavior of other people. Apparently in the course of an LLM’s training, this wheel gets reinvented. “Mutations”—changes in the model’s weights—that collectively create a capacity for cognitive empathy are preserved because they make LLMs better at completing certain kinds of sentences: sentences about what’s going on in people’s minds and sentences about people’s behavior that are easier to complete if you know what’s going on in their minds. At least, that’s my theory. [page 117]

You don't need to grasp a lot of information theory to know that LLMs can't have all the answers in its "corpus" as some seem to assume. It just wouldn't fit, there is no way to make a database to autocomplete all the ways you can question them. LLMs must have true understanding of language to make sensible answers. They do make mistakes, but so does humans, however LLMs haven't been yet trained on with truly multi-modal datasets. They don't know what is it like to drive a car to a carwash, and may never know what food tastes like.[^1]

What we train LLMs on is largely driven by commercial needs, ability to understand world at the level of language is much higher in need than creating artificial taste buds. There are lot of low hanging fruits in commercial space for LLM training, one obvious is in robotics and spatial understanding. I tried to query ChatGPT about measurements from a picture, it struggled. It got confused by barrel distortion, subsequently hallucinated size of fire alarm, and had no ability to reason the object dimensions along the perspective line. After all they aren't yet trained to understand "can I reach that object", or "how should I manuver my body to reach that object". They don't know yet how far things are or how to get there.

This is from beginning of the book, but it fits nicely at the end of this post:

> So, yes, the LLM is compressing large stretches of a child’s learning process into a few months of training, but it’s also, in a sense, compressing large stretches of human evolution into that training. Feats of engineering that took hundreds of thousands if not millions of years for natural selection to perform are performed in, relatively speaking, no time at all. [page 23]

[^1]: With food, there is more complications, presumably taste of food changes based on your nutrient levels and how satied you feel yourself. How would we even approach making good enough dataset for that? LLMs might feel satisfied from the good sip of electricity though.