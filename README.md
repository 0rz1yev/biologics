from flask import Flask, render_template

app = Flask(__name__)

# Define some example biological topics and their descriptions
biological_topics = {
    "Topic 1": {
        "image": "topic1.jpg",  # File path to the image for DNA
        "information_url": "/topic/topic1/information",
        "locations_url": "/topic/topic1/locations"
    },
    "Topic 2": {
        "image": "topic2.jpg",  # File path to the image for DNA
        "information_url": "/topic/topic2/information",
        "locations_url": "/topic/topic2/locations"
    },
    "Topic 3": {
        "image": "topic3.jpg",  # File path to the image for DNA
        "information_url": "/topic/topic3/information",
        "locations_url": "/topic/topic3/locations"
    }
}

@app.route('/')
def index():
    return render_template('index.html', topics=biological_topics)

@app.route('/topic/<topic_name>')
def topic(topic_name):
    topic_data = biological_topics.get(topic_name)
    if not topic_data:
        return "Topic not found", 404
    return render_template('topic.html', topic_name=topic_name, topic_data=topic_data)

@app.route('/topic/topic1')
def topic1():
    topic1_data = biological_topics.get("topic1")
    return render_template('topic1.html', topic_data=topic1_data)

@app.route('/topic/topic2')
def topic2():
    topic2_data = biological_topics.get("topic2")
    return render_template('topic2.html', topic2_data=topic2_data)

@app.route('/topic/topic3')
def topic3():
    topic3_data = biological_topics.get("topic3")
    return render_template('topic3.html', topic_data=topic3_data)

@app.route('/topic/<topic_name>/information')
def information(topic_name):
    topic_data = biological_topics.get(topic_name)
    if not topic_data:
        return "Topic not found", 404
    # You can add specific information pages for other topics if needed
    return render_template('information.html', topic_name=topic_name, topic_data=topic_data)

@app.route('/topic/<topic_name>/locations')
def locations(topic_name):
    topic_data = biological_topics.get(topic_name)
    if not topic_data:
        return "Topic not found", 404
    # You can add specific locations pages for other topics if needed
    return render_template('locations.html', topic_name=topic_name, topic_data=topic_data)

if __name__ == '__main__':
    app.run(debug=True)
