## SUM-AG NATIONAL HIGH SCHOOL DIGITAL LIBRARY
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

books = []

@app.route('/')
def index():
    return render_template('index.html', books=books)

@app.route('/add', methods=['GET', 'POST'])
def add_book():
    if request.method == 'POST':
        title = request.form['title']
        author = request.form['author']
        books.append({'title': title, 'author': author})
        return redirect(url_for('index'))
    return render_template('add_book.html')

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        # Handle login logic here
        return redirect(url_for('index'))
    return render_template('login.html')

@app.route('/register', methods=['GET', 'POST'])
def register():
    if request.method == 'POST':
        # Handle registration logic here
        return redirect(url_for('index'))
    return render_template('register.html')

if __name__ == '__main__':
    app.run(debug=True)
    <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Digital Library</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
</head>
<body>
    <h1 style="background-color: yellow;">Digital Library</h1>
    <ul>
        {% for book in books %}
            <li>{{ book.title }} by {{ book.author }}</li>
        {% endfor %}
    </ul>
    <a href="{{ url_for('add_book') }}">Add a new book</a>
    <form method="get" action="{{ url_for('search') }}">
        <input type="text" name="query" placeholder="Search for books">
        <button type="submit">Search</button>
    </form>
    <a href="{{ url_for('login') }}">Log In</a>
    <a href="{{ url_for('register') }}">Sign Up</a>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Log In</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
</head>
<body>
    <h1 style="background-color: yellow;">Log In</h1>
    <form method="post">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required><br>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br>
        <button type="submit">Log In</button>
    </form>
    <a href="{{ url_for('index') }}">Back to Library</a>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Sign Up</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
</head>
<body>
    <h1 style="background-color: yellow;">Sign Up</h1>
    <form method="post">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required><br>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required><br>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br>
        <label for="confirm_password">Confirm Password:</label>
        <input type="password" id="confirm_password" name="confirm_password" required><br>
        <button type="submit">Sign Up</button>
    </form>
    <a href="{{ url_for('index') }}">Back to Library</a>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 0;
}

h1 {
    background-color: yellow;
    color: #333;
    padding: 10px;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    background-color: #fff;
    margin: 5px;
    padding: 10px;
    border: 1px solid #ddd;
}

a {
    display: inline-block;
    margin-top: 20px;
    text-decoration: none;
    color: #333;
    background-color: yellow;
    padding: 10px 20px;
    border-radius: 5px;
}

a:hover {
    background-color: #333;
    color: #fff;
}

form {
    margin-top: 20px;
}
