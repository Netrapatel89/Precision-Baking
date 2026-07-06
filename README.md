# Precision Baking 

[![Next.js Version](https://img.shields.io/badge/Next.js-15.2.4-blue?logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![Python Version](https://img.shields.io/badge/Python-3.9+-yellow?logo=python&logoColor=white)](https://python.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange?logo=tensorflow&logoColor=white)](https://tensorflow.org)
[![Gemini](https://img.shields.io/badge/Google_Gemini-2.0--flash-red?logo=googlegemini&logoColor=white)](https://deepmind.google/technologies/gemini/)
[![Database](https://img.shields.io/badge/Database-MongoDB-green?logo=mongodb&logoColor=white)](https://mongodb.com)

**Precision Baking** is a full-stack, hybrid application built to solve the biggest variable in baking: volumetric measurements. In baking, weight precision is the difference between failure and a perfect rise. By combining a modern **Next.js** frontend with a **Python-powered AI/ML and Natural Language Processing (NLP)** backend, the platform converts imprecise recipe descriptions into exact weight-based metric recipes, recognizes dishes from images, and recommends curated baking ideas.

---

## 🗺️ System Architecture

The Next.js web application coordinates with local Python micro-services and external cloud APIs



## 🌟 Core Features

### ⚖️ 1. Density-Based Measurement Converter
* **The Problem:** A cup of flour can weigh anywhere from 120g to 160g depending on how it's scooped and packed.
* **The Solution:** Paste any baking recipe, and the app uses a **spaCy NLP model** to extract ingredients and quantities. It queries an ingredient density dataset (`density_data.csv`) and automatically calculates the exact metric weight (grams) of each item based on its physical density.

### 📸 2. AI Image Dish Identifier & Recipe Generator
* Upload a photo of any baked food or pastry.
* A custom **Convolutional Neural Network (CNN)** (Keras model `model_image.keras`) classifies the image to determine the dish type.
* The application automatically triggers **Gemini 2.0 Flash** to draft a precise recipe, accompanied by matching baking tutorials retrieved via the **YouTube Data API**.

### 🔍 3. Text-Based Recipe Recommendations
* Type a search query or input ingredients you currently have in your pantry.
* The system computes a **TF-IDF representation** and uses **Cosine Similarity** to match your query against a 26MB curated dataset of recipes (`dataset.csv`), presenting you with the highest-quality matches.

### 📊 4. Authenticated Dashboard & History
* Secure JWT user authentication with encrypted passwords (bcrypt).
* Email verification service templates styled with EJS templates and sent through Nodemailer.
* Personalized user space containing saved recipes, past conversion histories, and interactive dashboard analytics rendered using **Recharts**.

---

## 🛠️ Technology Stack

| Layer | Technologies Used |
|---|---|
| **Frontend & UI** | React 19, Next.js 15 (App Router), Tailwind CSS, DaisyUI, Recharts, Tabler Icons |
| **Backend & Auth** | Node.js, Next.js API Routes, JWT, Bcrypt.js, Nodemailer, EJS |
| **Database** | MongoDB, Mongoose ODM |
| **Machine Learning** | TensorFlow / Keras (CNN Classification), scikit-learn (TF-IDF & Cosine Similarity) |
| **NLP** | spaCy (`en_core_web_sm` model) |
| **Generative AI** | Google Generative AI SDK (Gemini 2.0 Flash) |
| **External Integrations** | YouTube Data API v3 |

---

## 📂 Repository Layout

```
├── python/                     # Python scripts handling AI/ML and NLP logic
│   ├── models/                 # Neural networks, pickle files, and vectorizers
│   │   ├── model_image.keras   # Pre-trained CNN model for dish identification
│   │   ├── vectorizer.pkl      # Saved TF-IDF Vectorizer
│   │   └── ingredient_vectors.pkl
│   ├── upload/                 # Buffer directory for image processing
│   ├── convert.py              # Parsing and density calculations
│   ├── image_predict.py        # Image classification and Gemini interaction
│   ├── text_predict.py         # Content-based recommendation system
│   ├── density_data.csv        # Custom volume-to-weight conversions
│   └── dataset.csv             # Curated baking recipes database
│
├── src/                        # Next.js Application Source
│   ├── app/
│   │   ├── (Home)/             # Public authentication & presentation routes
│   │   ├── api/                # Internal API route handlers
│   │   └── user/               # Private dashboard & authenticated workspace
│   ├── components/             # Reusable UI component blocks
│   ├── helper/                 # Server template and mailing layouts
│   ├── models/                 # Mongoose schemas (User, SavedRecipe, Conversion)
│   ├── context/                # Context-level state management
│   └── types/                  # Global TypeScript type definitions
```

---

## 🚀 Setup & Installation

### Prerequisites
* **Node.js** (v18.0.0 or higher)
* **Python** (v3.9 - v3.11 recommended for TensorFlow compatibility)
* **MongoDB** (running locally or in the cloud via Atlas)

### Step 1: Clone the Repo and Install Web Dependencies
```bash
git clone https://github.com/yourusername/precision-baking.git
cd precision-baking
npm install
```

### Step 2: Establish the Python Virtual Environment
It is highly recommended to isolate Python dependencies:
```bash
# Initialize virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
.\venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install required packages
pip install tensorflow numpy spacy scikit-learn pandas requests python-dotenv google-generativeai matplotlib openpyxl

# Install English language processing pipeline
python -m spacy download en_core_web_sm
```

### Step 3: Setup Configuration (.env)
Create a `.env` file in the project's root folder using the `.env.sample` format:
```env
MONGO_URI=mongodb://localhost:27017/precision-baking
JWT_SECRET=your_custom_jwt_secret_token
GOOGLE_API_KEY=your_gemini_api_key
YOUTUBE_API_KEY=your_youtube_data_api_v3_key

# Optional (Needed for user email verification):
EMAIL_USER=your_auth_email@gmail.com
EMAIL_PASS=your_email_app_password
```

### Step 4: Run Locally
Start the Next.js local development server:
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) on your web browser to test the features!

---

## 🤝 Contributing
Contributions are what make the open source community such an amazing place to learn, inspire, and create.
1. Fork the Project.
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the Branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

---

## 📄 License
Distributed under the MIT License. See `LICENSE` for more information.
