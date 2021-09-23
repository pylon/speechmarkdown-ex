# SpeechMarkdown

[Speech Markdown](https://www.speechmarkdown.org/) transpiler for Elixir.

This library converts text in the Speech Markdown format to
[SSML](https://www.w3.org/TR/speech-synthesis11/) for processing by
Text-To-Speech APIs, etc.


## Extensions

### `filter`
This element adds an audio filter to a section or modifier. The filter syntax
allows specifying a sequence of audio filter definitions seperated by
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
