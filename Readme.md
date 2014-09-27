# ![Retext logo](http://i58.tinypic.com/5xpx5z.png)

[![Build Status](https://img.shields.io/travis/wooorm/retext.svg)](https://travis-ci.org/wooorm/retext) [![Coverage Status](https://img.shields.io/coveralls/wooorm/retext.svg)](https://coveralls.io/r/wooorm/retext?branch=master) [![Code Climate](http://img.shields.io/codeclimate/github/wooorm/retext.svg)](https://codeclimate.com/github/wooorm/retext)

> Hey all! First, thanks a lot for watching, starring, and forking **retext**!
Secondly, I wanted to invite you all to leave any [feedback](mailto:tituswormer@gmail.com) or [issues](https://github.com/wooorm/retext/issues) you might have, to help me make **retext** even cooler :smile:.

---

**retext** is an extensible natural language system—by default using **[parse-latin](https://github.com/wooorm/parse-latin)** to transform natural language into a **[TextOM](https://github.com/wooorm/textom/)** object model. **Retext** provides a pluggable system for analysing and manipulating natural language in JavaScript. NodeJS and the browser. Tests provide 100% coverage.

> Rather than being a do-all library for Natural Language Processing (such as [NLTK](http://www.nltk.org) or [OpenNLP](https://opennlp.apache.org)), **retext** aims to be useful for more practical use cases (such as censoring profane words or decoding emoticons, but the possibilities are endless) instead of more academic goals (research purposes).
> **retext** is inherently modular—it uses plugins (similar to [rework](https://github.com/reworkcss/rework/) for CSS) instead of providing everything out of the box (such as [Natural](https://github.com/NaturalNode/natural)). This makes **retext** a viable tool for use on the web.

## Installation

npm:
```sh
$ npm install retext
```

Component:
```sh
$ component install wooorm/retext
```

Bower:
```sh
$ bower install retext
```

## Usage

The following example uses **[retext-emoji](https://github.com/wooorm/retext-emoji)** (to show emoji) and **[retext-smartypants](https://github.com/wooorm/retext-smartypants)** (for smart punctuation).

```js
/* Require dependencies. */
var Retext = require('retext'),
    emoji = require('retext-emoji'),
    smartypants = require('retext-smartypants'),
    input,
    retext;

/* Create an instance using retext-emoji and -smartypants. */
retext = new Retext()
  .use(emoji({
      'convert' : 'encode'
  }))
  .use(smartypants());

/* Read a document. */
retext.parse(
  'The three wise monkeys [. . .] sometimes called the ' +
  'three mystic apes--are a pictorial maxim. Together ' +
  'they embody the proverbial principle to ("see no evil, ' +
  'hear no evil, speak no evil"). The three monkeys are ' +
  'Mizaru (:see_no_evil:), covering his eyes, who sees no ' +
  'evil; Kikazaru (:hear_no_evil:), covering his ears, ' +
  'who hears no evil; and Iwazaru (:speak_no_evil:), ' +
  'covering his mouth, who speaks no evil.',
  function (err, tree) {
    /* Handle errors. */
    if (err) {
        throw err;
    }

    /* Log the text content of the tree (the transformed input). */
    console.log(tree.toString());
    /**
     * This logs the following:
     *   The three wise monkeys […] sometimes called the three
     *   mystic apes—are a pictorial maxim. Together they
     *   embody the proverbial principle to (“see no evil,
     *   hear no evil, speak no evil”). The three monkeys are
     *   Mizaru (🙈), covering his eyes, who sees no evil;
     *   Kikazaru (🙉), covering his ears, who hears no evil;
     *   and Iwazaru (🙊), covering his mouth, who speaks no evil.
     */
  }
);
```

## API

### Retext(parser?)

```js
var Retext = require('./'),
    ParseEnglish = require('parse-english'),
    retext;

retext = new Retext(new ParseEnglish());

/**
 * There, ol' chap.
 */

retext.parse(/* ...some English... */, function (err, tree) {/* ... */});
```

Return a new `Retext` instance with the given [parser](#parsers) (defaults to an instance of **parse-latin**).

### Retext.prototype.use(plugin)

Takes a plugin—a humble function. When `Retext#parse` is invoked, the plugin will be invoked with the parsed tree, and the **Retext** instance as arguments. Returns self.

### Retext.prototype.parse(value, callback)

Parses the given source and when done passes either an error (the first argument), or the (by `use`d plugins, modified) tree (the second argument) to the callback.

## Plugins

  * [retext-ast](https://github.com/wooorm/retext-ast) — Encoding and decoding between AST (JSON) and TextOM object model;
  * [retext-content](https://github.com/wooorm/retext-content) — Append, prepend, remove, and replace content into/from Retext nodes;
  * [retext-directionality](https://github.com/wooorm/retext-directionality) — (**[demo](http://wooorm.github.io/retext-directionality/)**) — Detect the direction text is written in;
  * [retext-dom](https://github.com/wooorm/retext-dom) — (**[demo](http://wooorm.github.io/retext-dom/)**) — Create a (living) DOM tree from a TextOM tree;
  * [retext-double-metaphone](https://github.com/wooorm/retext-double-metaphone) — (**[demo](http://wooorm.github.io/retext-double-metaphone/)**) — Implementation of the Double Metaphone algorithm;
  * [retext-emoji](https://github.com/wooorm/retext-emoji) — (**[demo](http://wooorm.github.io/retext-emoji/)**) — Encode or decode [Gemojis](https://github.com/github/gemoji);
  * [retext-keywords](https://github.com/wooorm/retext-keywords) — Extract keywords and keyphrases;
  * [retext-lancaster-stemmer](https://github.com/wooorm/retext-lancaster-stemmer) — Implementation of [the Lancaster (Paice/Husk) algorithm](http://www.comp.lancs.ac.uk/computing/research/stemming/index.htm);
  * [retext-language](https://github.com/wooorm/retext-language) — (**[demo](http://wooorm.github.io/retext-language/)**) — Detect the language of text;
  * [retext-link](https://github.com/wooorm/retext-link) — (**[demo](http://wooorm.github.io/retext-link/)**) — Detect links in text;
  * [retext-metaphone](https://github.com/wooorm/retext-metaphone) — (**[demo](http://wooorm.github.io/retext-metaphone/)**) — Implementation of the Metaphone algorithm;
  * [retext-porter-stemmer](https://github.com/wooorm/retext-porter-stemmer) — (**[demo](http://wooorm.github.io/retext-porter-stemmer/)**) — Implementation of [the Porter stemming algorithm](http://tartarus.org/martin/PorterStemmer/);
  * [retext-pos](https://github.com/wooorm/retext-pos) — Part-of-speech tagger;
  * [retext-range](https://github.com/wooorm/retext-range) — Sequences of content within a TextOM tree between two points;
  * [retext-search](https://github.com/wooorm/retext-search) — (**[demo](http://wooorm.github.io/retext-search/)**) — Search in a TextOM tree;
  * [retext-sentiment](https://github.com/wooorm/retext-sentiment) — (**[demo](http://wooorm.github.io/retext-sentiment/)**) — Detect sentiment in text;
  * [retext-smartypants](https://github.com/wooorm/retext-smartypants) — (**[demo](http://wooorm.github.io/retext-smartypants/)**) — Implementation of [SmartyPants](http://daringfireball.net/projects/smartypants/);
  * [retext-soundex](https://github.com/wooorm/retext-soundex) — Implementation of the Soundex algorithm;
  * [retext-syllable](https://github.com/wooorm/retext-syllable) — Syllable count;
  * [retext-visit](https://github.com/wooorm/retext-visit) — (**[demo](http://wooorm.github.io/retext-visit/)**) — Visit nodes, optionally by type;

## Desired Plugins

> Hey! Want to create one of the following, or any other plugin, for **retext** but not sure where to start? I suggest to read **retext-visit**’s source code to see how it’s build first (it’s probably the most straight forward to learn), and go from there.
> Let me know if you still have any questions, go ahead and send me [feedback](mailto:tituswormer@gmail.com) or [raise an issue](https://github.com/wooorm/retext/issues).

  * retext-date — detect time and date in text;
  * retext-live — Detect changes in a textarea (contenteditable?), sync the diffs over to a **retext** tree, let plugins modify the content, and sync the diffs back to the textarea;
  * retext-profanity — Censor profane words;
  * retext-punctuation-pair — detect which opening or initial punctuation, belongs to which closing or final punctuation mark (and vice versa);
  * retext-summary — Summarise text;
  * retraverse — like Estraverse;

## Parsers

  * [parse-latin](https://github.com/wooorm/parse-latin "Parse Latin") (**[demo](http://wooorm.github.io/parse-latin/)**) — default;
  * [parse-english](https://github.com/wooorm/parse-english "Parse English") (**[demo](http://wooorm.github.io/parse-english/)**) — Specifically for English;
  * [parse-dutch](https://github.com/wooorm/parse-dutch "Parse Dutch") (**[demo](http://wooorm.github.io/parse-dutch/)**) — Specifically for Dutch;

## Benchmark

Run the benchmark yourself:

```sh
$ npm run benchmark
```

On a MacBook Air, it parses about 2 big articles, 22 sections, or 206 paragraphs per second.

```
              retext.parse(source);
  202 op/s » A paragraph (5 sentences, 100 words)
   22 op/s » A section (10 paragraphs, 50 sentences, 1,000 words)
    2 op/s » An article (100 paragraphs, 500 sentences, 10,000 words)
```

## Related

  * [textom](https://github.com/wooorm/textom "TextOM")

## License

MIT © Titus Wormer
