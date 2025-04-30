pip install flask
from flask import Flask, request, jsonify

app = Flask(__name__)

# Sample responses for common green campus queries
responses = {
    "recycle": "You can recycle paper, plastic, and glass in the blue bins located around campus.",
    "energy": "Remember to turn off lights and unplug chargers when not in use to save energy!",
    "events": "The next eco-awareness event is the 'Green Friday' on April 10th at the student center.",
    "transport": "You can rent bicycles at the campus gate or use the electric shuttle service.",
    "default": "I'm here to help with sustainability! Ask me about recycling, energy, green events, or transport."
}

@app.route("/chat", methods=["POST"])
def chat():
    user_input = request.json.get("message").lower()
    
    for keyword in responses:
        if keyword in user_input:
            return jsonify({"response": responses[keyword]})
    
    return jsonify({"response": responses["default"]})

if __name__ == "__main__":
    app.run(debug=True)
    <!DOCTYPE html>
<html>
<head>
    <title>Green Campus Chatbot</title>
</head>
<body>
    <h2>Green Campus Assistant</h2>
    <input id="message" placeholder="Ask me about recycling, events, etc.">
    <button onclick="sendMessage()">Send</button>
    <p id="response"></p>

    <script>
        function sendMessage() {
            const msg = document.getElementById("message").value;
            fetch("/chat", {
                method: "POST",
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ message: msg })
            })
            .then(res => res.json())
            .then(data => {
                document.getElementById("response").innerText = data.response;
            });
        }
    </script>
</body>
</html>
python app.py
