---
title: MLOps Resoucres
description: A note about what you should notice at a ML project 
date: 2021-11-18
tags:
  - posts
layout: layouts/post.njk
---
# MLOps Resoucres

How to maintain and start an AI project is not a simple software project.Because it contains the new part like data collection/data processing/find a good way to model the task/evaluate what we train/monitor and optimize the model online.

## Table of contains
* [Note-to-lauch-AI-project](#Note-to-lauch-AI-project)
* [Course](#Course)
* [Tools-of-MLOpes](#Tools-of-MLOpes)
* [Article](#Article)




----
### Note-to-lauch-AI-project

How to construct a Proof of Concept for an AI project ?

#### 1. Clearly define the purpose of the AI task

>It is necessary to clarify the background of the problem with the stakeholders, the operating mechanism of the original service and the goals they want to achieve. And can analyze whether there is AI in the middle that can make up the part, and what benefits and costs can be added if necessary.

- Confirm important window contacts (with relevant knowledge/can trust), and establish an instant communication channel
- Effectively record and synchronize project stakeholders' information
- Able to draw up phased goals  
- Confirm whether the data required for the question is reasonable, what is the method of collecting the data or how to build it
- Preliminarily clarify the evaluation index (metric) as the question to improve the standard


#### 2. Data collection and processing  
    
- Must have a reliable and stable way of receiving data.
- If you need to mark the data, how to integrate relevant domain knowledge, or if there is relevant information for reference.
- Check whether the collected information is normal and complete, and whether it meets the requirements of the target task

Ｏthers:
- Assess whether traditional identification methods can be used, and semi-automatic labeling is done first to reduce the cost of manual labeling.
  Ｅxample: Use template matching to assist label the object.
  

#### 3. Looking for methods related to building:

- Evaluate the appropriate method based on the current data size/type.
- Try to find existing methods from google, as a baseline reference.
- From Github to find a package open to use by others, if there is a good method and commercial authorization can be used.
- Read related papers/curriculums of major U.S. universities/public competition materials.

Resources:
  - Resource websites with AI papers and programs in various fields:https://paperswithcode.com/
  
  - Kaggle: Data analysis/modeling competition platform, sometimes there will be programs for related topics for reference.
  https://www.kaggle.com/


#### To Do:
- How to establish a data/model version control mechanism?
- How to quickly deploy the environment? Reduce the time to rebuild the environment

---

### Course

#### 1. CMU AI software engineering course resources
- Machine learning in Ai production https://ckaestne.github.io/seai/
- Software Engineering for Ai-Enabled Systems https://ckaestne.github.io/seai/S2020/#course-content

---
### Tools-of-MLOpes

#### Developing
- Reviewnb: Notebook Collaboration Tool: https://www.reviewnb.com/

#### Model
- MLflow: https://mlflow.org/
- BentoML: the open source ML model deployment platform https://www.bentoml.ai/

#### Monitoring
- Prometheus: model monitoring: https://prometheus.io/
- Grafana: Data visualization: https://grafana.com/


---
### Article
#### 1. Line publicly shares its own MLops process
link:(in traditional chinese) https://www.ithome.com.tw/news/141774?fbclid=IwAR2u39v9I5WDDlYJz89gxhgNpFUBajeJKAHtT-fni2g9qA4-blsIfsBOS-s


- A feature store for managing feature data (Feature Store) has been established so that data engineers can input the sorted data into the feature store through a unified interface, and store the feature data in a standardized way. In this way, ML Engineers and data analysts can find the required data through the same interface, eliminating the need for time-consuming data processing, thereby achieving the purpose of reusing characteristic data.

- Integration of model development, the team integrated Jupyter Notebook as a collaborative development tool, and also integrated the open source Jnotebook Reader, so that the developed Notebook can be easily shared among various teams
https://chrome.google.com/webstore/detail/jupyter-notebook-viewer/ocabfdicbcamoonfhalkdojedklfcjmf

- Integrated with Jupyter Notebook's collaborative work tool ReviewNB, making the work of viewing code smoother.
https://www.reviewnb.com/


- The team built a Pipeline Editor tool, which allows ML developers to directly link each step of the pipeline through a visual drag-and-drop setting method: https://www.jenkins.io/doc/book/blueocean/pipeline-editor/

- For model training, Line Taiwan also trains models through the NSML platform supported by hundreds of GPUs to meet a large number of computing needs, and monitor the amount of resources used through a visual method; not only that, the NSML platform also provides The AutoML function can save the time required to repeatedly adjust the hyperparameters during the ML training process, aiming at different model versions generated during continuous training
https://ai.nsml.navercorp.com/intro

- It also integrates the open source ML platform MLFlow, allowing developers to perform version control and simple analysis and verification in the subsequent model testing phase.
https://mlflow.org/

- After the model was verified, the team also used the open source ML model deployment platform BentoML to access the selected model
https://www.bentoml.ai/


- In the monitoring of the effectiveness of the model after launch, the aspects to be monitored include the health of the service itself and whether the model has declined due to changes in the environment. The former can be monitored through Prometheus with Grafana, while the latter needs to be monitored according to the business. Logic to set monitoring indicators, monitor through the BI dashboard, and trigger model retraining according to the degree of model degradation.

model monitoring: https://prometheus.io/
Data visualization: https://grafana.com/