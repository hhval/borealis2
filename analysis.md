# Language analysis of the Borealis 2 test set

**TL;DR:** Borealis 2 sounds more natively Norwegian than many mainstream language models, but there is still work to do when it comes to language quality.

## The positives

Compared to what we are used to from chatbots, Borealis 2 sounds more native in both sentence structure and term choices. The Norwegian-tuned model seems less likely to output sentences that read like direct translations from English (although it is not perfect).

The following sentence about the Norwegian school system is a good example of the kind of language that often comes out stilted from a language model, but reads pretty well from Borealis 2:

> «Den norske skolen kjennetegnes av en inkluderende og likestilt tilnærming der alle barn får lik rett til utdanning uavhengig av bakgrunn.»

There were no split compounds (særskriving) in the test set, and overall the use of terminology and expressions was good.

## The negatives

However, there were also a number of errors and issues in the test set. They were mainly related to the following categories:

### Wrong language advice

* Claims that «hverken» is the most used and recommended bokmål form, and that «verken» is more formal or literary. The forms are largely interchangeable.
* Invents an error in its own example, marking a sentence as wrong that is identical to the one it had just marked correct: «Han har skrevet et brev.»

### Factual errors due to knowledge cutoff or general hallucination

* States that the current king is King Harald.
* Refers to *trygdeavgift* as «medlemsavgift (skatt)».
* «Arbeids- og sosialministeriet» does not exist. The real body is Arbeids- og inkluderingsdepartementet.
* Lists youth clubs and youth counselors as a county responsibility when they are municipal.

### Grammar

* Missing verb: «Den ledet av statsministeren …», which should be *Den ledes av*.
* Broken clause: «den blå bilen vi allerede vet hvilken det er».

### Lexical

* «landskapige» is not a word.
* «langs den lengdegraden» is a clunky way to describe a north–south axis.
* Uses the Danish or Swedish form «absolut» for *absolutt*.

### English and anglicization

* Mix of Norwegian and English: «community work-dag».
* Direct translation: «Jeg har dessverre fått en konflikt på tirsdag».
* Overused English-flavored vocabulary: *presis* 10 times across 4 of the 30 responses, 6 of them in a single answer; *spesifikk/spesifikt* 8 times across 5 responses; *kontekst* 4 times across 4 responses.

### Nynorsk

* Personal pronouns: claims that only «me» belongs to nynorsk and that «vi» is not allowed. Both «vi» and «me» are valid nynorsk forms.
* Invented hybrid form: «muntleg» is neither bokmål (*muntlig*) nor nynorsk (*munnleg*).

### Formatting

* Uses capital initial letters in headings and titles, English-style.
* Heavy Markdown usage: headings, bold and tables even in three-sentence answers.
* Frequently uses dashes instead of commas.

Note: This analysis is based on a very small test set of 30 prompts, and is only meant as an indication of the kinds of language issues that remain. The model was run as a Q4_K_M quantization of a preview release, at temperature 0.7, so the same prompts will not produce identical responses and these particular errors may not reappear in another run.
