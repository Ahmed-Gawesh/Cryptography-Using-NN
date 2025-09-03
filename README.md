# 🛡️ Neural Network Asymmetric Encryption System

# 📜 Overview
This project implements a neural network-based asymmetric encryption system inspired by adversarial learning principles. It features:

🔑 KeyGen: Generates public keys from private keys.
🧑‍💻 Alice: Encrypts plaintext using the public key.
🧑‍🔧 Bob: Decrypts ciphertext using the private key.
🕵️‍♀️ Eve: An adversarial network that attempts to recover plaintext during training (and fails, ensuring security).
🌐 API: A FastAPI server for encryption/decryption endpoints.

The system is trained to ensure Bob's accurate decryption while thwarting Eve's attempts. It processes text as binary tensors and supports batch operations via a RESTful API.

⚠️ Note: This is an experimental project for educational purposes. It is not suitable for production-grade cryptography.


# ✨ Features

🧠 Neural network models for key generation, encryption, decryption, and adversarial simulation.

📦 Batch processing for encryption/decryption via API.

🌍 CORS-enabled for seamless web integration.

🔢 Base64-encoded ciphertexts for easy data transfer.

✅ Health check endpoint for server monitoring.

📊 Visualization of training errors (Bob vs. Eve).


# 🛠️ Requirements

🐍 Python 3.10+

🔬 TensorFlow 2.19+

🧩 Keras 3.9+

🚀 FastAPI

🖥️ Uvicorn (for running the API server)

📚 Additional dependencies: NumPy, Matplotlib, TQDM, Pydantic, etc.

See requirements.txt for the complete list.

# 🚀 Installation


Install Dependencies:
bashpip install -r requirements.txt

Ensure Pre-trained Models:

Place key_gen.keras, alice.keras, bob.keras, and eve.keras in the root directory.
Alternatively, train the models using asymmetric_encryption.ipynb (see Training).

# 📡 Usage

Run the FastAPI Server:
bashuvicorn main:app --reload --port 8000.
Access the server at http://127.0.0.1:8000.

Check Server Health:
bashcurl http://127.0.0.1:8000/health
Expected response: {"status": "healthy"}

Explore the API:
Visit http://127.0.0.1:8000/docs for interactive Swagger UI documentation.


# 🐍 Example: Python Client
pythonimport requests

Encrypt
response = requests.post("http://127.0.0.1:8000/encrypt", json={"plaintext": ["Test message"]})
print(response.json())

Decrypt
cipher_data = response.json()["results"]
decrypt_response = requests.post("http://127.0.0.1:8000/decrypt", json={"ciphertexts": cipher_data})
print(decrypt_response.json())

# 🧠 Training the Models

Open asymmetric_encryption.ipynb in Jupyter Notebook or Google Colab.
Execute the cells to build, train, and evaluate the models.
Configure training parameters in the Config class:

P_LEN=32 (plaintext length)
K_LEN=32 (key length)
C_LEN=32 (ciphertext length)
EPOCHS=20, BATCH_SIZE=256, etc.


Save the trained models:
pythonencryption_system.key_gen.save('key_gen.keras')
encryption_system.alice.save('alice.keras')
encryption_system.bob.save('bob.keras')
encryption_system.eve.save('eve.keras')

Visualize training performance:
pythonencryption_system.plot_errors("eval")


The training ensures Bob's decryption error is near 0, while Eve's error remains high (~0.5, equivalent to random guessing).

# 📂 Project Structure

text├── 📄 main.py                    # FastAPI server for encryption/decryption

├── 📓 asymmetric_encryption.ipynb # Jupyter notebook for model training

├── 💾 key_gen.keras              # Pre-trained KeyGen model

├── 💾 alice.keras                # Pre-trained Alice model

├── 💾 bob.keras                  # Pre-trained Bob model

├── 💾 eve.keras                  # Pre-trained Eve model (for evaluation)

├── 📋 requirements.txt           # Dependency list

├── 📝 README.md                  # This file

└── 📜 LICENSE                    # MIT License

# 🤝 Contributing
We welcome contributions to enhance this project! 🚀

Fork the repository.
Create a feature branch:
bashgit checkout -b feature/your-new-feature

Commit your changes:
bashgit commit -m "Add your new feature"

Push to your branch:
bashgit push origin feature/your-new-feature

Open a pull request.

For major changes, please open an issue first to discuss your ideas.

# 📄 License
This project is licensed under the MIT License. See the LICENSE file for details.
