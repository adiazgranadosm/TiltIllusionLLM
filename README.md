# Identifying Tilt Illusion with Large Language Models (LLMs)

[![Python](https://img.shields.io/badge/Python-3.10+-yellow.svg)](https://www.python.org/)
[![OpenAI](https://img.shields.io/badge/OpenAI-API-412991.svg)](https://platform.openai.com/)
[![Data Science](https://img.shields.io/badge/Data%20Analysis-Pandas%20%7C%20Matplotlib-blue)](https://pandas.pydata.org/)

## Overview

This research project investigates the capacity of Large Language Models (LLMs) to detect and describe the **Tilt Illusion**—a visual phenomenon where the perceived orientation of a central stimulus is biased by surrounding patterns.

By bridging human psychophysics with computational modeling, this study evaluates whether generative AI can replicate human-like perceptual biases (repulsion/attraction effects) and how visual disparities (contrast, depth) and textual context influence these judgments.

<img width="500" height="378" alt="image" src="https://github.com/user-attachments/assets/78a622f7-18d5-4a79-b3e1-34c3f578c996" />



## Key Features

* **Synthetic Dataset Generation:** Automated pipeline to create sinusoidal grating stimuli with adjustable parameters for orientation ($ -90^\circ$ to $90^\circ$), contrast, and stereoscopic depth cues (shadows).
* **Multimodal LLM Integration:** Uses the OpenAI Vision API to process image-based inputs, evaluating the model's ability to classify orientation (Clockwise vs. Anticlockwise).
* **Perceptual Segmentation Testing:** Analysis of how visual "segmentation" cues (distractors) affect the magnitude of the illusion in AI models.
* **Contextual Priming:** Evaluates the impact of "System Prompts" explaining the illusion versus minimal-context prompting to test semantic sensitivity.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/1e714706-671d-4c00-b7d6-b0775e2f8297" />


## System Architecture

The framework is composed of three core modules:

1.  **Dataset Generation Module:**
    * Constructs center-surround sinusoidal patterns.
    * Applies **Gaussian filtering** to simulate depth (shadows) and linear scaling for contrast adjustment.
    * **Conditions:** *No-Distractor* (Baseline), *Contrast Distractor*, and *Depth Distractor*.
  
    <img width="500" alt="image" src="https://github.com/user-attachments/assets/5cd537d2-09eb-4d93-82ec-5b17d3a9bcf0" />



2.  **LLM Integration Module:**
    * Interacts with the OpenAI API using binary classification prompts.
    * **Temperature:** Set to `0.2` to minimize hallucination and ensure deterministic responses.
    * **Modes:** Minimal Context vs. Full Context (priming the model about repulsion/attraction effects).

3.  **Data Processing & Analysis:**
    * Captures response metadata in structured CSV format.
    * Generates **Cumulative Distribution Functions (CDF)** and frequency polynomial trend curves to visualize perceptual biases.

## Experimental Methodology

The study was conducted through two primary experiments:

### Experiment 1: Visual Disparities
* **Objective:** Test if visual segmentation cues (Contrast, Depth) reduce the illusion magnitude in LLMs as they do in humans.
* **Scope:** 1,140 trials across 3 image groups (114 unique images $\times$ 10 iterations).
* **Findings:** LLMs mimic human bias by misclassifying vertical stimuli as tilted but lack the robust perceptual grouping mechanisms seen in human vision.

<img width="1700" alt="image" src="https://github.com/user-attachments/assets/abec1af8-9e79-4fc9-bbc1-3067482b2425" />



### Experiment 2: Contextual Priming
* **Objective:** Assess if explaining the illusion in the prompt alters the model's perception.
* **Scope:** 380 trials comparing "Minimal Input" vs. "Contextual Explanation".
* **Findings:** Contextual prompts significantly reduced response noise and aligned the model's decisions closer to human psychophysical patterns.

<img width="1500" alt="image" src="https://github.com/user-attachments/assets/a7d68df3-3f9d-420c-8c45-bf46e1d7ece0" />



## 📊 Key Results

* **Bias Replication:** The model successfully demonstrated human-like "repulsion" effects, frequently misclassifying vertical lines ($0^\circ$) as tilted under no-distractor conditions.
* **Context Sensitivity:** While visual segmentation cues (depth/contrast) had a weak effect on the model, **textual context** strongly influenced decision-making, confirming that LLMs rely more on semantic instruction than visual perceptual grouping.
* **Uncertainty:** In the absence of context, the model exhibited high variability (noise), whereas context stabilized the probability distribution curves.

## Dependencies

* `python` (3.x)
* `openai` (API integration)
* `numpy` (Matrix operations for image generation)
* `matplotlib` / `seaborn` (Statistical plotting)
* `pandas` (Data logging and CSV manipulation)
* `Pillow` (Image processing)

## Usage

1.  **Generate Dataset:**
    ```bash
    python generate_stimuli.py --mode batch --distractors [contrast, depth]
    ```

2.  **Run Experiment:**
    ```bash
    python run_experiment.py --api_key "YOUR_KEY" --prompt_type "context"
    ```

3.  **Analyze Results:**
    ```bash
    python analyze_results.py --input "data/experiment_logs.csv" --plot cdf
    ```

## References

* **Qiu, C., et al. (2013).** Segmentation Decreases the Magnitude of the Tilt Illusion. *Journal of Vision*.
* **Qiu, C., et al. (2012).** Segmentation Effects on the Tilt Illusion: Contrast and Depth. *Journal of Vision*.
* **OpenAI.** (2025). OpenAI Platform Documentation.

## License

This project is for academic research purposes.
