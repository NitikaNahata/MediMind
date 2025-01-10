# MediMind
MediMind is an automated radiology report generation system that leverages multimodal large language models (LLMs) to produce accurate and coherent summaries of chest X-rays. The project aims to address the challenges faced by radiologists in writing multiple reports daily, which can lead to fatigue and potential errors in critical health data interpretation.

# Project Overview

# Goals and Background
The primary objective of MediMind is to create a scalable, AI-powered medical assistant that generates radiology impressions similar to those produced by experienced radiologists. By utilizing pretrained LLMs and a Retrieval Augmented Generation (RAG) system, the tool delivers targeted and accurate summaries of chest X-rays, potentially reducing workload and improving diagnostic accuracy.
Research Questions and Hypotheses
How can multimodal LLMs improve the accuracy and consistency of radiology report generation?
Hypothesis: Fine-tuning on medical imaging datasets enhances the model's ability to interpret X-rays and provide precise, clinically relevant summaries.
Can a RAG system effectively retrieve and utilize relevant prior reports to improve the quality of generated summaries?
Hypothesis: Implementing RAG allows the system to leverage existing expert knowledge, leading to more accurate and contextually appropriate report generation.

# Methods and Technical Implementation

# Data Collection and Processing

# Dataset: 
IU-XRAY dataset from Indiana University Medical Department, containing chest X-ray images paired with diagnostic reports.

# Preprocessing: 
Images are encoded into vector embeddings using the PubMedCLIP model, which is trained on the ROCO dataset for medical imaging.

# Modeling
Embedding Generation: PubMedCLIP encoder is used to create image vector embeddings for both training and query images.
Vector Database: Qdrant Cloud Vector Database stores image embeddings and associated radiology summaries for efficient retrieval.
Language Model: BioMistral, a 4-bit quantized version of an LLM tailored for the biomedical domain, is used to generate radiology summaries.


# System Architecture
Indexing:
X-ray images are processed through PubMedCLIP to generate embeddings.
Embeddings and corresponding summaries are stored in Qdrant.
Inferencing:
User uploads a query X-ray image.
Image is encoded using PubMedCLIP.
QDRANT vector retriever performs similarity search to find top K similar impressions.
Retrieved impressions are used as context for the LLM.
BioMistral generates a detailed radiology summary based on the context and prompt.

![System Design](https://github.com/user-attachments/assets/8c550d4d-734a-400f-bc86-39404d206a4d)



# Results and Evaluation
Retrieval Evaluation: Achieved 100% accuracy in matching 50 test image embeddings with their corresponding reports.
Generator Evaluation: Utilized Claude Sonnet 3.5 as an LLM judge to assess completeness, coherence, relevance, and accuracy of generated responses.
Initial accuracy: 72% (36/50 correct responses)
Improved accuracy after prompt refinement: 80% (40/50 correct responses)
Overall score: 3 out of 5 for relevance, accuracy, and conciseness, compared to 1 out of 5 for standalone LLM without RAG.
These results demonstrate the effectiveness of the MediMind RAG system in generating accurate and relevant radiology reports, showing significant improvement over traditional LLM approaches1

![RAG Evaluation](https://github.com/user-attachments/assets/873bafaa-2192-4306-ae1a-dc83a958b71c)



