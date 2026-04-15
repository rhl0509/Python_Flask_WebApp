# 1. 플라스크 첫걸음
# flask 클래스를 import 한다
from flask import Flask, render_template, url_for, request

# flask 클래스를 인스턴스화한다.
app = Flask(__name__)

# URL과 실행할 함수를 매핑한다.
@app.route("/")
def index():
    return "Hello, Flaskbook!"

@app.route("/hello/<name>", endpoint="hello_endpoint")
def hello(name):
    return f"Hello, {name}!"
# flask2부터는 @app.get("/hello"), @app.post("/hello")라고 기술하는 것이 가능
# @app.get("/hello")
# @app.post("/hello")
# def hello():
#     return "Hello, World!"

@app.route("/name/<name>")
def show_name(name):
    # 변수를 템플릿 엔진에게 건넨다.
    return render_template("index.html", name=name)

with app.test_request_context("/users?updated=true"):
    # / 
    print(url_for("index"))
    #/hello/world
    print(url_for("hello_endpoint", name="world"))
    # /name/AK?page=1
    print(url_for("show_name", name="AK", page="1"))
    # 출력한다.
    print(request.args.get("updated"))
