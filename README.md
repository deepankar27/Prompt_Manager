# Managing Prompts with Ease: Prompt Organizer Pro

In the realm of **Prompt Engineering**, managing multiple versions of prompts can become overwhelming. Individuals and teams often face challenges in tracking and organizing different types of prompts, leading to the possibility of missing out on some of the best ones.

The lack of a structured approach to manage prompts efficiently often makes it difficult to navigate through them, causing a significant impediment in the workflow. Understanding this persistent issue, we introduce an application that serves as a beacon of relief: The **Prompt Organizer Pro**.

## Features of the Prompt Organizer Pro:
1. Task-Based Organization:
Users can organize prompts under different tasks (Summarization, Topic Discovery, Intent identification etc), allowing for a clear and categorized view of each prompt.

2. Prompt Versions Management:
Within each task, users can create and manage multiple versions of prompts, each with its unique set of parameters.

3. Difference Visualization:
Users can leverage the integrated 'Show Diff' feature to effortlessly visualize and compare differences, additions, or deletions between various prompt versions, highlighted for easy spotting.

4. Prompt Parameters Configuration:
Users can easily configure various parameters like temperature, top_p, max tokens, and threshold for each version of the prompt.

5. Status Tracking:
The app allows users to set and track the status of each prompt, aiding in prompt evaluation and optimization.

6. Commenting Feature:
Each prompt version has an associated comment box, allowing users to annotate important notes or information related to the prompt.

7. System Prompt Management:
Alongside user prompts, the app also enables the management of system prompts, each with its commenting feature.

8. Save and Download:
Users can save their progress and download the organized prompts in YAML format, facilitating easy sharing and storage.

9. YAML Integration for Developer Pipelines:
This application seamlessly facilitates developers by allowing the direct incorporation of YAML files into their development pipelines, making the development process more intuitive and less error-prone.

<p align="center">
  <img src="assets/capture_1.jpeg" width="500" height="500" alt="Prompt Organizer">
</p>

## Example how to use it

### Inside the prompt use placeholders and replace them with right contents:
I am giving you a passage which is noisy and you have to find the most important intents which are having high discussion value, important and represent the entire call conversation. All the intents must be in string format and relevancy score must be in integer format.\n\nYour response must contain outputs in dictionary format, following are some examples: [{intents: Intent Score},{}].\nDo not add any explanations.\n\nPassage:\n\n##placeholder_1##

Replace the ##placeholder_1## dynamically with the input passage.

```
Passage.replace("##placeholder_1##", passage_content)
```

## How to read prompt from yaml:
Load the yaml file using this method:
```
import yaml

def read_template():
	directory_path = "data.yaml"
	yaml_content = ''

	with open(directory_path, "r") as f:
		try:
			yaml_content = yaml.safe_load(f)
		except yaml.YAMLError as e:
			print(f"Error parsing {directory_path}: {e}")
	
	return yaml_content

```

## How to read prompts for a given task with its version from the YAML file?
```
def get_prompt(task, version):
    yaml_content = read_template()
    version = "version"+"_"+str(version)
    return yaml_content[task]['prompts']['version_1']["prompt"]
	
prompt = get_prompt("Intent",1)

```

## How to get parameters of given task with its version from the YAML file?
```
def get_parameters(task, version):

    yaml_content = read_template()
    version = "version"+"_"+str(version)
    temp = yaml_content[task]['prompts'][version]['temperature']
    top_p = yaml_content[task]['prompts'][version]['top_p']
    max_tokens = yaml_content[task]['prompts'][version]['max_tokens']
    threshold = yaml_content[task]['prompts'][version]['threshold']

    return {"temperature":temp, "top_p":top_p, "max_tokens":max_tokens, "threshold":threshold}

params = get_parameters('Intent',1)

```