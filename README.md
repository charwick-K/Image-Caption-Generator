# Image-Caption-Generator

This project is an implementation of an **image caption generator**, inspired by [Yumi’s Blog](https://fairyonice.github.io/Develop_an_image_captioning_deep_learning_model_using_Flickr_8K_data.html). The system automatically produces captions that describe the contents of an image.  

Image captioning is a fascinating challenge because it combines **computer vision** (to understand what’s in the picture) with **natural language processing** (to express that understanding in words). Beyond being an academic exercise, this technology has real-world impact in areas such as accessibility for the visually impaired, medical imaging, and geospatial analysis.

---

## 🌍 Real-World Applications
- **Accessibility:** A visually impaired person could snap a photo on their phone, and the system would generate a caption that can be read aloud, helping them understand their surroundings.  
- **Advertising:** Marketing teams could automate caption creation for product images, saving time during production and sales campaigns.  
- **Healthcare:** Doctors could leverage captioning models to highlight anomalies in medical scans, such as tumors or defects.  
- **Geospatial analysis:** Researchers could use captions to interpret satellite or terrain images more effectively.  

---

## 📂 Dataset
We use the **Flickr_8K dataset**, which contains about 1,500 images. Each image is paired with five human-written captions, giving the model multiple perspectives on how a scene can be described. The dataset is packaged as a ~1GB zip file, with images stored separately from the caption text file.

---

## 🔄 Project Workflow
1. **Clean the caption data**  
2. **Extract image features using VGG-16**  
3. **Merge captions with images**  
4. **Build and train an LSTM model**  
5. **Generate captions on test data**  
6. **Evaluate results using BLEU scores**  

---

## 🛠️ Step-by-Step Process

### 1. Cleaning Captions
Raw captions often contain punctuation, numbers, and irrelevant tokens. We preprocess them by removing noise and stopwords. After cleaning, we analyze word frequency to identify the most common and least common terms in the dataset.

### 2. Adding Start/End Tokens
Since captions vary in length, we add special **start** and **end** markers so the model knows where a caption begins and ends.

### 3. Extracting Image Features
We use the pre-trained **VGG-16 model**. Instead of classifying images, we strip off the final output layer and use the network to generate **4096-dimensional feature vectors** for images resized to (224, 224, 3). These vectors capture the essence of each image.

### 4. Clustering Similar Images
Once features are extracted, we group similar images together. This helps verify that VGG-16 is correctly capturing visual similarities.

### 5. Merging Captions with Images
Each image is paired with its caption(s). For simplicity, we use only the first caption per image during training. Captions are then tokenized so they can be fed into the model.

### 6. Splitting Data
We divide the dataset into **training, validation, and test sets**, ensuring balanced representation for evaluation.

### 7. Building the LSTM Model
We design an **LSTM-based architecture** that takes both image features and text tokens as input. LSTMs are ideal here because they remember context across sequences, which is crucial for generating coherent captions.  
We experiment with different hidden layer sizes (256, 512, 1024) and tune hyperparameters to improve performance.

### 8. Prediction & Evaluation
After training, we test the model on unseen images. Captions are generated and compared against ground-truth captions using the **BLEU score**.  
- A score closer to **1.0** means the generated caption closely matches human-written captions.  
- Some outputs are impressively accurate, while others miss the mark — highlighting the importance of further tuning.

---

## 📊 Hyperparameter Tuning
We experiment with different configurations and track performance using charts, tables, and TensorBoard visualizations. This iterative process helps identify the sweet spot for model accuracy and caption quality.

---

## ✅ Conclusion
Building an image caption generator is a **time-intensive but rewarding task**. It requires careful preprocessing, feature extraction, model design, and evaluation. While the system produces strong captions, there’s always room for improvement through better architectures, larger datasets, and more advanced training techniques.
