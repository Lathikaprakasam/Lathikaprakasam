from flask import Flask, request, jsonify

app = Flask(__name__)

# Sample keyword-based responses for green campus chatbot
RESPONSES = {

    "recycle": "Recycle paper, plastic, and glass in designated blue bins around campus.",
    "waste": "Please use the compost bin for food waste and the recycling bin for plastics and metals.",
    "energy": "Turn off lights and electronic devices when not in use to conserve energy.",
    "water": "Report leaks and avoid wasting water. Use campus water refill stations.",
    "events": "The next sustainability event is 'Eco Awareness Week' starting on May 5th.",
    "transport": "Use bicycles, campus electric shuttles, or walk to reduce your carbon footprint.",
    "contact": "You can contact the Green Campus Office at greenoffice@university.edu."
}

@app.route("/chat", methods=["POST"])
def chat():
    user_message = request.json.get("message", "").lower()

    for keyword, response in RESPONSES.items():
        if keyword in user_message:
            return jsonify({"response": response})

    return jsonify({"response": "I'm here to help with green campus initiatives. Ask me about recycling, events, transport, or sustainability tips!"})

if __name__ == "__main__":
    app.run(debug=True)
