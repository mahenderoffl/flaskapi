# flaskapi
from flask import Flask, jsonify
from gradio_client import Client
import os

app = Flask(__name__)

@app.route('/')
def home():
    return '✅ API is running. Visit /generate for quotes.'

@app.route('/generate', methods=['GET'])
def generate_quote():
    client = Client("mahendercreates/motivational-quotes-generator")
    img, caption = client.predict(api_name="/predict")
    return jsonify({
        "image_url": img["url"],
        "caption": caption
    })

if __name__ == '__main__':
    port = int(os.environ.get("PORT", 5000))
    app.run(host="0.0.0.0", port=port)
