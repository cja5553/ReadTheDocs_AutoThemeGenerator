## `analyze_and_synthesize_transcripts`

!!! note ""

    
    AutoThemeGenerator.**analyze_and_synthesize_transcripts**(*\*, directory_path, context, research_questions, script, api_key, save_results_path*)  



Function that analyzes transcripts, chunks them into manageable sizes, and synthesizes them into individual themes before syntheszing them into overarching study themes using an OpenAI GPT model. For more details, refer to [How does it work?](index.md#how-does-it-work) 


**Parameters:**:  

 - `directory_path` (*str*): The folder path in which the transcripts are located.  Folder should contain either `.txt`,`.docx`, or `.pdf` files. 
 - `context` (*str*): Context of the overall study
- `research_questions` (*str*): Research questions of the study   
- `script` (*str*): Script used in interviews or focus groups.  
- `api_key` (*str*): OpenAI API key. For more details, refer to [platform.openai.com/api-keys](https://platform.openai.com/api-keys)
- `save_results_path` (*str*): The path where the results will be saved, `themes_per_person.json` and `themes_overall.json`. 
- `model` (*str, optional*): The model to be used for completion. For a list of possible models, refer to [platform.openai.com/docs/models](https://platform.openai.com/docs/models). Defaults to `gpt-4`.
- `max_tokens_chunk` (*int, optional*): The maximum number of tokens in each transcript segment. Defaults to 2500.
- `overlap_tokens` (*int, optional*): The number of tokens that overlap between two consecutive transcript segments. Defaults to 100.
- `max_tokens_transcript` (*int, optional*): The maximum length of the generated text from a transcript segment. Defaults to 1000.
- `max_tokens_combine_ind_themes` (*int, optional*): Maximum token length for combining an single participant's themes. Defaults to 5000.
- `max_tokens_gen_ind_themes` (*int, optional*): Maximum tokens for generating themes from a chunk of combined themes from a single participant. Defaults to 1000
- `max_tokens_combine_all_themes` (*int, optional*): Maximum token length for combining themes from all participants. Defaults to 4000.
- `max_tokens_gen_all_themes` (*int, optional*): Maximum tokens for generating themes from all participants (each individual has a single chunck of themes). Defaults to 2000.

**Returns**  

- `initial_themes`, `individual_synthesized_themes` & `overall_synthesized_themes` each as a list of lists: A list where each sublist contains a synthesized chunk of overall study themes.  


**Example**

```python
from AutoThemeGenerator import analyze_and_synthesize_transcripts
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


## `download_example`


!!! note ""

    
    AutoThemeGenerator.**download_example**()  

Function to download example transcripts from a url. Used primarily for ease of demonstration in our [demonstrated examples](examples.md). 


**Parameters:**:  

 - `folder_name` (*str, optional*): Name of folder where the example transcripts will be contained in exisiting directory. Defaults to `example_transcripts`. 
 - `url` (*str, optional*): download url of the transcripts, should end in .zip format. Defaults to downloading an .zip transcripts from [Henderson et al's (2020)](https://jeehp.org/journal/view.php?doi=10.3352/jeehp.2020.17.22) study.  


**Example**

```python
>>> from AutoThemeGenerator import download_example
>>> download_example()
```