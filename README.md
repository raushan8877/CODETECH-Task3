# CODETECH-Task3
import nltk
import random
import string
from nltk.chat.util import Chat, reflections
from nltk.tokenize import word_tokenize
from nltk.corpus import wordnet, stopwords
from nltk.stem import WordNetLemmatizer

# Download necessary NLTK data files
nltk.download('punkt')
nltk.download('wordnet')
nltk.download('stopwords')
nltk.download('omw-1.4')

# Define stopwords
stop_words = set(stopwords.words('english'))

# Predefined responses
pairs = [
    ["(hi|hello|hey)", ["Hello Raushan Raj ", "Hi there!", "Hey! How can I help you?"]],
    ["how are you", ["I'm a chatbot, but I'm here to help!", "I'm great! How about you?"]],
    ["what is your name", ["I'm a simple chatbot built using NLTK!", "You can call me ChatBot!"]],
    ["(bye|goodbye)", ["Goodbye! Have a great day!", "See you later!"]],
    ["how does machine learning work", ["Machine learning is a way for computers to learn patterns from data."]],
    ["who created you", ["I was created using Python and NLTK by a developer."]],
    ["(.*)", ["I'm not sure about that. Can you ask something else?", "I don't have an answer for that."]]
]

# Create chatbot instance
chatbot = Chat(pairs, reflections)

# Lemmatizer
lemmatizer = WordNetLemmatizer()

# Function to process user input
def preprocess(text):
    tokens = word_tokenize(text.lower())  
    tokens = [lemmatizer.lemmatize(word) for word in tokens if word not in string.punctuation and word not in stop_words]  
    return " ".join(tokens)

# Chat loop
print("Hello! I'm your chatbot. Type 'bye' to exit.")
while True:
    user_input = input("You: ").strip()

    if not user_input:
        print("ChatBot: Please enter a valid message.")
        continue

    user_input = preprocess(user_input)

    if user_input == "bye":
        print("ChatBot: Goodbye! Have a nice day!")
        break

    response = chatbot.respond(user_input)
    print(f"ChatBot: {response}")
