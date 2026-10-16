---
permalink: /
title: ""
excerpt: "Nina R Benway is a speech-language pathologist and neural network engineer developing clinical speech AI, from speech inversion and ultrasound biofeedback to clinical trials and scalable deployment."
author_profile: true
redirect_from:
  - /about/
  - /about.html
---


I am a speech-language pathologist, acoustic phonetician, and neural network engineer developing clinical speech technologies. I have built and tested clinical AI across the full pipeline: speech representations, neural network training, clinical trials, and scalable deployment. My engineering work includes model development in PyTorch, cloud deployment, and leading the software teams behind NIH-funded clinical tools.

I am a postdoctoral fellow in Electrical and Computer Engineering at the University of Maryland, College Park, working with [Carol Espy-Wilson](https://isr.umd.edu/clark/faculty/391/Carol-Espy-Wilson) in the Speech Communication Lab. My training and research are supported by an NIH NIDCD Pathway to Independence Award (K99/R00), five years of funding that began in 2026, and previously by an NIH T32.

**At a glance**

- **Funding:** Principal investigator of an NIH K99/R00 and two American Speech-Language-Hearing Foundation grants. Co-investigator on two NIH R01 clinical trials.
- **Clinical trials:** I test clinical speech technologies, including those I develop, in clinical trials. I contribute to four trials in progress, [iChain](https://clinicaltrials.gov/study/NCT05929859), [VISIT](https://clinicaltrials.gov/study/NCT06517225), [GAINS](https://clinicaltrials.gov/study/NCT06884943), and [ChainingAI](https://clinicaltrials.gov/study/NCT05988515), and am first author on ChainingAI. Completed trials include a [single-case randomization design comparing ultrasound and visual-acoustic biofeedback](https://pubmed.ncbi.nlm.nih.gov/34232693/) ([registry](https://clinicaltrials.gov/study/NCT03736213)) on which I am first author, [C-RESULTS](https://clinicaltrials.gov/study/NCT03737318) ([primary outcomes](https://pubmed.ncbi.nlm.nih.gov/40920957/), [secondary outcomes](https://pmc.ncbi.nlm.nih.gov/articles/PMC13081154/)), and an [ultrasound biofeedback trial for childhood apraxia of speech](https://clinicaltrials.gov/study/NCT03238677).
- **Translation:** Lead inventor on a U.S. patent application for clinical speech analysis (notice of allowance, 2026). Co-founder, President, and CEO of SpeechLink Incorporated.
- **Open data and tools:** The PERCEPT Corpora, the largest open-access speech corpora for childhood speech sound disorders in American English, and the VoxKit phone alignment tool.

---

## Research Themes

### Clinically Tested AI Speech Therapy

I develop neural networks for speech therapy and test them in clinical trials. I am the lead inventor on PERCEPT, a neural network that predicts clinician judgment of speech correctness during therapy. With [Jonathan Preston](https://artsandsciences.syracuse.edu/people/faculty/preston-jonathan-l/#Biography), I embedded PERCEPT in ChainingAI, a platform that delivers [Speech Motor Chaining](https://chaining.myspeechlink.com) with automated feedback for practice at home. A single-case experimental study showed improved /ɹ/ production, and a randomized controlled trial of ChainingAI is underway. I also work on responsible standards for developing and evaluating clinical AI, including an end-to-end overview of clinical speech AI.

### Extending Ultrasound and Articulography: Kinematic Speech Analysis from Audio

My postdoctoral research uses acoustic-to-articulatory speech inversion, a neural network method that estimates the movements of the tongue, lips, and jaw from audio alone. Kinematic speech production data are scarce for children because ultrasound and articulography instruments are mainly found in specialized laboratories. My work draws on data from both instruments to design speech inversion neural networks that extend the clinical reach of kinematic speech analysis to any setting with a microphone. I have shown that inferred tract variables differentiate error subtypes in children with speech sound disorders and quantify coordination differences in childhood apraxia of speech. I have also shown that clinician ratings of speech correctness predict articulatory proximity to the target sound. My K99 builds on this work to estimate child vocal tract gestures, classify gesture errors, and personalize tongue biofeedback displays for each learner.

### Ultrasound Biofeedback and Acoustic Biofeedback for Speech Therapy

Ultrasound imaging gives learners a real-time view of the tongue, which is normally hidden. My colleagues and I have shown that biofeedback, including ultrasound and acoustic biofeedback, enhances motor learning in speech therapy, particularly when delivered intensively and even for children who did not respond to traditional therapy. With [Tara McAllister](https://steinhardt.nyu.edu/people/tara-mcallister), Jonathan Preston, and [Elaine Hitchcock](https://www.montclair.edu/profilepages/view_profile.php?username=hitchcocke), I contributed to a large randomized controlled trial finding faster speech improvement with biofeedback than with motor-based treatment during acquisition. Ongoing trials test telepractice delivery and AI-mediated home practice. My K99 aims to deliver the benefit of ultrasound-style tongue displays from a microphone alone.

### Speech Profiles of Speech Sound Disorders in Children

I have investigated how speech sound disorders manifest across articulatory, perceptual, and acoustic dimensions, and how to automate measurement of each dimension. I collaborate with [Katie Hustad](https://csd.wisc.edu/staff/hustad-katie/) and [Visar Berisha](https://search.asu.edu/profile/226165) on automated measures of speech sound production that support personalized assessment and treatment.

### Child Speech Data and Research

I curated the [PERCEPT Corpora](https://phon.talkbank.org/access/Clinical/PERCEPT-R.html), the largest open-access speech corpora for speech sound disorders in American English. I am the sole US-based co-founder of the Interspeech Child Speech Science and Speech Technology special sessions, and I helped introduce child speech topic areas to the main program.

### Automated Language Sample Analysis

My ongoing postdoctoral research examines automatic speech recognition for clinical language sample analysis. Automated language sample metrics outperformed manual metrics in predicting language disorder status in children, reducing the burden of manual transcription and scoring.

---

The tools I use to address these research themes include:
Azure DevOps, Amazon AWS, Git, Google Speech API, HTCondor/Cluster Computing, Linux, MATLAB, Montreal Forced Aligner, NLTK, Phon, Praat, PyTorch/CUDA, R, REDCap API, Regex, RESTful APIs, SAS, Stanza/CoreNLP, and several custom tools I've developed in Python
