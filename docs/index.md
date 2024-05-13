# AutoThemeGenerator  
AutoThemeGenerator is a package that allows you to perform thematic analysis in qualitative studies using OpenAI's GPT models. 

<p align="center">
  <a href="https://cja5553.github.io/ReadTheDocs_AutoThemeGenerator/">
    <img src="https://img.shields.io/badge/Documentation-v0.1.2-orange" alt="Documentation">
  </a>
  <a href="https://pypi.org/project/AutoThemeGenerator/">
    <img src="https://img.shields.io/badge/pypi_package-v0.1.2-brightgreen" alt="pypi package">
  </a>
  <a href="https://github.com/cja5553/AutoThemeGenerator">
    <img src="https://img.shields.io/badge/github_source_code-source_code?logo=github&color=green" alt="GitHub Source Code">
  </a>
  <a href="https://colab.research.google.com/drive/1BoAI-QNL-yL8j8hUJ3K8cJkbyp4spoQ3">
    <img src="https://img.shields.io/badge/-Colab_Example-grey?logo=google&logoColor=F9AB00" alt="Colab Example">
  </a>
</p>


### User input  

Users are only required to specify the folder location where their interview transcripts are stored. Accepted formats of transcripts include `PDF`, `.docx`, and `.txt` (prefered). AutoThemeGenerator` assumes that each document is a transcript of one interviewed participant. Files that are not formatted as such may lead to subpar results (refer to [How does it work?](#how-does-it-work) to understand why) 

### Output  

The package outputs a **list of relevant themes** synthesized across all interview transcripts. Themes are presented in the form of a:  
1. topic sentence,  
2. an explanation,  
3. a relevant quote  
The outputs are similar to what you would expect to see in a proper qualitative analysis study. An example of an expected output is shown below:   
```python
>>> print(overall_synthesized_themes)

# note: output truncated for display purposes
["**Theme 1: Understanding and Awareness of Physical Activity**
- Topic Sentence: Participants exhibited a range of understandings ... ... 
- Explanation: Physical activity was generally understood ... ... 
- Quote: 'Physical activity is anything that ...'
**Theme 2: Personal and Environmental Barriers to Physical Activity** 
- Topic Sentence: Participants identified multiple personal and situational obstacles ... ...
- Explnanation: These barriers stem from personal issues like inconvenience ... ...
- Quote: 'I think that a lot of people don’t want to put in the effort'... ... 
... ...
... ...
... ..."]
```

The package is also structured to analyze and view themes for each individual transcript. 

```Python
>>> from pprint import pprint
>>> for i in range(len(individual_synthesized_themes)):
>>>      print(f"\n\nThe themes from interviewee {i+1} is:\n")
>>>      pprint(individual_synthesized_themes[i])
The themes from interviewee 1 is:
["Theme 1:
- Topic Sentence: ... ...,
- Explaination: ... ...,
- Quote: ... ...]

The themes from interviewee 2 is:
["Theme 1: ... ...
- Topic Sentence: ... ...,
- Explaination: ... ...,
- Quote: ... ...]
```

For more details refer to [documention](documention.md). 

## Requirements
### Required packages
To use `AutoThemeGenerator`, you are required to have the following packages installed:  
- `openai`  
- `docx`    
- `tqdm`    
- `nltk`    
- `nltk.tokenize` (submodule of `nltk`)   
- `python-docx`  
- `textract`  
- `requests`  
- `zipfile` (Python standard library)   
- `shutil`  (Python standard library)  
- `json`  (Python standard library)  

If you do not have this packages installed in python, you can do the following:
```bash
pip install openai==1.12.0 python-docx docx tqdm nltk textract requests
```
### OpenAI API key
You also need an OpenAI key to be able to use this package. If you do not have one, you can apply for an OpenAI API key at [platform.openai.com/api-keys](https://platform.openai.com/api-keys). 


## Installation
To install in python, simply do the following: 

```bash
pip install AutoThemeGenerator
```

## Quick Start
Here we provide a quick example on how you can execute GPT4QualitativeAnalysis to conveniently perform qualitative analysis from your transcript. For details towards each of the package's functions and parameters, refer to the [documention](documention.md). 

```python
from AutoThemeGenerator import *

# specify the context of your study
context = (
    "Physical inactivity is a major risk factor for developing several chronic illness. "
    "However, university students and staff in the UK are found to be more physically inactive "
    "compared the general UK population. "
    )
# specify your research questions
research_questions = (
    "This study seeks to understand the barriers and enablers "
    "of physical activity (PA) among university staff and students in "
    "the UK under the university setting, using the Theoretical "
    "Domain Framework (TDF) to guide the investigation. "
    )
# specify your survey script
survey_script = (
    "Knowledge\n "
    "What do you know about physical activity? How might you define physical activity? "
    "... ..." # note: truncated to save space
    "... ..." 
    )



# Specify the folders containing your transcript
directory_path = "my_transcript_folder"
# specify your OpenAI API key
api_key = "<insert your API key>"
# specify the folder you wish to save your themes. 
save_results_path = "folder_of_my_saved_results"


# Analyze and synthesize transcripts
initial_themes, individual_synthesized_themes, overall_synthesized_themes = \
analyze_and_synthesize_transcripts(
    directory_path = directory_path, context = context,
    research_questions = research_questions, script = survey_script,
    api_key = api_key, save_results_path = save_results_path)

# display your study-level themes
print(overall_synthesized_themes)
```

You can now view the themes in the form of a topic sentence, a detailed explaination and a relevant quote



## How does it work?
![alt text](Figure 1.jpg)
##### 1. Chunking 
Transcripts are chunked into sizeable bits to fit into GPT-4's context window
##### 2. Extracting relevant themes 
Background information is provided to the GPT model. These include the context, research question and survey script. Themes are then identified at a chunk-level. 
##### 3. Synthesizing themes at a participant level
Chunk level themes are then synthesized at a participant-level. 
##### 4. Synthesizing themes to a study-level
Participant-level themes are then synthesized at a study-level. For each study, the package returns a topic sentence of the theme, an explaination of the theme, and a supporting relevant quote from the transcript. 

## Citation  
Y Yang, C Alba, W Xi, M Li, C Wang, A Jami, R An. "GPT Models Can Perform Thematic Analysis in Public Health Studies, Akin to Qualitative Researchers" Working paper.


## Questions?
Contact me at [alba@wustl.edu](mailto:alba@wustl.edu)
