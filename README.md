[![Markov Namegen logo](https://github.com/Tw1ddle/markov-namegen-lib/blob/master/screenshots/markovnamegen_logo.png?raw=true "Markov Namegen Procedural Random Name Generator Project logo")](https://www.samcodes.co.uk/project/markov-namegen/)

[![License Badge](https://img.shields.io/:license-mit-blue.svg?style=flat-square)](https://github.com/Tw1ddle/markov-namegen-lib/blob/master/LICENSE)
[![Build Status Badge](https://ci.appveyor.com/api/projects/status/github/Tw1ddle/markov-namegen-lib)](https://ci.appveyor.com/project/Tw1ddle/markov-namegen-lib)

Markov Namegen is a Markov chain-based word generator library written in Haxe, made for procedural name generation. Run the demo [here](https://www.samcodes.co.uk/project/markov-namegen/).

[![Screenshot](https://github.com/Tw1ddle/MarkovNameGenerator/blob/master/screenshots/screenshot2.png?raw=true "Markov Namegen Procedural Random Name Generator screenshot 2")](https://www.samcodes.co.uk/project/markov-namegen/)

## Features
* Hundreds of customizable/combinable training data presets.
* Katz backoff using high order models - look up to "n" characters back.
* Sort and filter generated strings by length, start, end, content and regex matching.
* Damerau-Levenshtein distance similarity sorting option.
* Dirichlet prior parameter.

## Usage

See the [demo code](https://github.com/Tw1ddle/MarkovNameGenerator) for a complete worked example. Also see the [library documentation](https://tw1ddle.github.io/markov-namegen-lib/).

## Library Setup

Get the Markov Namegen library from [GitHub](https://github.com/Tw1ddle/markov-namegen-lib) or through [haxelib](https://lib.haxe.org/p/markov-namegen/).

Include it in your ```.hxml```
```
-lib markov-namegen
```

Or add it to your ```Project.xml```:
```
<haxelib name="markov-namegen" />
```

You can also transpile the library for use with different target languages by running the following from the root of the repository, and then checking the generated code in the bin folder:

```
haxe build.hxml
```

## How It Works

The [markov-namegen haxelib](https://lib.haxe.org/p/markov-namegen) uses [Markov chains](https://en.wikipedia.org/wiki/Markov_chain) to procedurally generate original words.

Using a set of words as [training data](https://en.wikipedia.org/wiki/Machine_learning), the library calculates the conditional probability of a letter coming up after a sequence of letters chosen so far. It looks back up to "n" characters, where "n" is the order of the model.

The generator can use several orders of models, each with memory n. Starting with the highest order models (models with bigger memories), it tries to get a new character, falling back to lower order models if necessary - an approach known as [Katz's back-off model](https://en.wikipedia.org/wiki/Katz%27s_back-off_model).

A [Dirichlet prior](https://en.wikipedia.org/wiki/Dirichlet_distribution#Special_cases) is used to add a constant probability that any letter may be picked as the next letter. This acts as an additive smoothing factor and adds a bit more "randomness" to the generated output.

Countless words are generated, and are then filtered and sorted according to several tweakable criteria like length, start and end characters, [similarity to a target word](https://en.wikipedia.org/wiki/Levenshtein_distance), and so on.

## Markov Namegen Ports

Some users have ported and extended the Markov Namegen library to different programming languages. See:

* Python - [pyMarkovNameGenerator](https://github.com/bicobus/pyMarkovNameGenerator) by [bicobus](https://github.com/bicobus).
* C# - [ProceduralNameGenerator](https://github.com/MagicMau/ProceduralNameGenerator) by [MagicMau](https://github.com/MagicMau). 

## Tips
* The generator works by using Markov chains, and requires training data to build them. A hundred or more words within your chosen category is usually sufficient for good results.
* Sort words by similarity to preferred "good words" using an edit distance metric, and pick the most similar and suitable results. There are a few edit distance measures provided in EditDistanceMetrics.hx.
* To get best results the training dataset, model order and prior will need to be tweaked for the type of words you want to generate. If possible, keep the prior parameter low or zero. Filter words to suit: look at length, beginning, end, contents, edit distance limits and regex. Some of this done for you in NameGenerator.hx. If you prefer to do it your own way, subclass the Generator class.

## Notes
* Many of the concepts used for the generator were suggested in [this article](http://www.roguebasin.com/index.php?title=Names_from_a_high_order_Markov_Process_and_a_simplified_Katz_back-off_scheme) by Jeffrey Lund.
* The haxelib is written in plain Haxe and so supports every Haxe target.
* If you have any questions or suggestions then [get in touch](https://twitter.com/Sam_Twidale) or open an issue.

## License
* Most of the training data bundled in the haxelib comes from sites like Wikipedia and census data sources over many years. CC-BY-SA 3.0 as a derivative from Wikipedia content will cover most of the content if you wish to use these for other purposes, but I provide no guarantee.
* The [haxelib](https://lib.haxe.org/p/markov-namegen/) code is provided under the MIT license.