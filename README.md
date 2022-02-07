# SpeechMarkdown

[Speech Markdown](https://www.speechmarkdown.org/) transpiler for Elixir.

This library converts text in the Speech Markdown format to
[SSML](https://www.w3.org/TR/speech-synthesis11/) for processing by
Text-To-Speech APIs, etc.


## Extensions

### `filter`
This element adds an audio filter to a section or modifier. The filter syntax
allows specifying a sequence of audio filter definitions separated by
semicolons, each with its own comma-separated list of name=value parameters.
Whitespace is ignored inside the filter definition.

#### Modifier example
```
(Hello)[filter:"reverse_reverb()"]
```

#### Section Example
```
#[
  filter:"
    dalek(frequency=30, distortion=4);
    xsynth_fixed(frequency=110);
    reverb;
  "
]
You would make a good Dalek.
```

#### Override Example
A filter applied in a modifier replaces any filters in surrounding modifiers
or sections. In the following example, the only filter applied to the text
will be `reverb`.

```
#[filter:"xsynth_random"]
(Poetry is an echo, asking a shadow to dance.)[filter:"reverb"]
```

### `diction`
This element adds a specific style of diction that can be simulated by
text manipulation. Examples of diction styles are a "pig Latin" effect and
a sibilant lisp. The diction syntax allows specifying a semicolon-separated
sequence of styles.
Whitespace is ignored inside the definition.

#### Modifier example
```
(Hello)[diction:"pig_latin"]
```

#### Section Example
```
#[diction:"pig_latin; lisp"]
She sells seashells down by the seashore.
```

#### Override Example
A diction style applied in a modifier replaces any dictions in surrounding modifiers
or sections. In the following example, the only diction applied to the text
will be `pig_latin`.

```
#[diction:"lisp"]
(Poetry is an echo, asking a shadow to dance.)[diction:"pig_latin"]
```

### `emotion`
This element specifies an emotion in which the associated text should be read.
Supported emotions will vary by model, but only one emotion can be listed at a time.
An optional numeric "intensity" modifier is also allowed to vary the expression of the requested emotion.

#### Modifier example
```
(Hello)[emotion:"angry";intensity:"2"]
```

#### Section Example
```
#[diction:"excited"]
She sells seashells down by the seashore.
```

#### Overrides
The `emotion` tag follows the same override rules as the other extensions.
