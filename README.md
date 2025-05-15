🛠️ Python Setup
✅ Install Python
Beginner Guide to Python

📦 Install required packages

bash
Copy code
pip install -r training/requirements.txt
pip install -r api/requirements.txt
📡 Install TensorFlow Serving
Setup instructions

⚛️ ReactJS Frontend Setup
🧱 Install Node.js & NPM

Node.js Setup

NPM Setup

📁 Install frontend dependencies

bash
Copy code
cd frontend
npm install
npm audit fix
🔐 Environment Setup

Copy .env.example → rename it to .env

Set your API URL inside .env

📱 React Native App Setup
📲 Set up environment
Follow the official React Native CLI Quickstart

🧵 Install mobile app dependencies

bash
Copy code
cd mobile-app
yarn install
🍏 (Mac-only) Install CocoaPods

bash
Copy code
cd ios && pod install && cd ../
📂 Copy .env.example → rename it to .env and set API URL

🧠 Training the Deep Learning Model
🗂️ Download dataset
Kaggle Dataset - PlantVillage

💾 Keep only potato folders

📓 Run the training notebook

bash
Copy code
jupyter notebook
Open training/potato-disease-training.ipynb, set dataset path in cell #2, and run all cells

🔁 Save the trained model in the models/ folder with a version number

🚀 Run the API Locally (FastAPI)
bash
Copy code
cd api
uvicorn main:app --reload --host 0.0.0.0
✅ API will be available at http://localhost:8000

🧪 Run with TF Serving + FastAPI
📁 Inside api/ folder, copy models.config.example → rename to models.config, update model paths

🐳 Run TensorFlow Serving with Docker (change paths accordingly)

bash
Copy code
docker run -t --rm -p 8501:8501 \
  -v C:/Code/potato-disease-classification:/potato-disease-classification \
  tensorflow/serving \
  --rest_api_port=8501 \
  --model_config_file=/potato-disease-classification/models.config
🚀 Run API with TF Serving

bash
Copy code
uvicorn main-tf-serving:app --reload --host 0.0.0.0
🌐 Run the Web Frontend
bash
Copy code
cd frontend
npm start
📍 Set REACT_APP_API_URL in .env if needed

📱 Run the Mobile App
bash
Copy code
cd mobile-app
npm run android   # or
npm run ios
📱 Mobile app connects to your FastAPI server to fetch predictions

✨ Create TF Lite Model
Launch:

bash
Copy code
jupyter notebook
Open training/tf-lite-converter.ipynb → run all cells after setting dataset path

📁 Saved models will appear inside tf-lite-models/

☁️ Deploy on Google Cloud Platform (GCP)
TF Lite Model via Google Cloud Functions (GCF)
Create a GCP account & project

Create a GCP bucket → Upload your .tflite model to models/

Install Google Cloud SDK

bash
Copy code
gcloud auth login
Deploy:

bash
Copy code
cd gcp
gcloud functions deploy predict_lite \
  --runtime python38 \
  --trigger-http \
  --memory 512 \
  --project your_project_id
✅ Use the trigger URL in Postman to test

Full TF Model (.h5) via GCF
Follow steps above, but upload .h5 model to models/ folder

Deploy using:

bash
Copy code
gcloud functions deploy predict \
  --runtime python38 \
  --trigger-http \
  --memory 512 \
  --project your_project_id
💡 Bonus Tips
🔄 Use Postman to test your API endpoints

📱 Mobile app can be packaged into a signed APK for Android deployment

🧠 Inspired by this GCP tutorial
