from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(_name_)
app.secret_key = "Secret key"
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///my_database.sqlite3"
app.config["SQLALCHEMY_TRACK_MODIFICATIONS"] = False

db = SQLAlchemy(app)

class Data(db.Model):
    product_id = db.Column(db.Integer, primary_key = True)
    location_id = db.Column(db.String(50))
    movement_id = db.Column(db.String(50))
    timestamp = db.Column(db.decimal(50))
    from_location=db.column(db.String(50))
    to_location=db.column(db.String(50))
    qty=db.column(db.String(50))

db.create_all()

# add a row
# comment out after the 1st run
table_row = Data(product="product name", location="movement name", movement="A to B",time="5.00",from_location="movement name",to_location="movement name",qty="5")
db.session.add(table_row)
db.session.commit()
print "A row was added to the table"

# read the data
row = Data.query.filter_by(product="product Name").first()
print "Found:", row.location, row.movement,row.time,row.from_location,row.to_location,row.qty

if _name_ == "_main_":
    app.run(debug=True)
