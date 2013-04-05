import os
from flask import Flask,  request, redirect, url_for, render_template
from flask.ext.sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = os.environ['DATABASE_URL']
db = SQLAlchemy(app)

class User(db.Model):
    __tablename__ = 'users'
    id = db.Column(db.Integer, primary_key=True)
    firstName = db.Column(db.String(80))
    lastName = db.Column(db.String(80))
    address = db.Column(db.String(900))
    isAuthenticated = db.Column(db.Boolean())
    email = db.Column(db.String(80))
    def __init__(self, firstName, lastName, address, isAuthenticated, email):
        self.firstName = firstName
        self.lastName = lastName
        self.address = address
        self.isAuthenticated = isAuthenticated
        self.email = email
    def __repr__(self):
        return '<Name %r>' % self.name

@app.route('/')
def home():
    entries = ""
    for row in User.query.all():
        entries = entries + "first name: " + row.firstName + '\n'
        entries = entries + "last name: " + row.lastName + '\n'
        entries = entries + "address: " + row.address + '\n'
        entries = entries + "is authenticated: " + str(row.isAuthenticated) + '\n'
        entries = entries + "email: " + row.email + '\n\n\n'
    return entries

@app.route('/new', methods=['GET', 'POST'])
def submit():
    if request.method == 'POST':
        user = User(request.form['firstname'], request.form['lastname'], request.form['addre\
ss'], False, request.form['email'])
        db.session.add(user)
        db.session.commit()
        return redirect(url_for('home'))
    return render_template('form.html')

if __name__ == '__main__':
    port = int(os.environ.get('PORT', 5000))
    app.run(host='0.0.0.0', port=port, debug=True)
