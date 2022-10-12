# Deploy-credit-card-model

## Models
We've prepared a dictionary vectorizer and a model.

They were trained (roughly) using this code:

features = ['reports', 'share', 'expenditure', 'owner']
dicts = df[features].to_dict(orient='records')

dv = DictVectorizer(sparse=False)
X = dv.fit_transform(dicts)

model = LogisticRegression(solver='liblinear').fit(X, y)


## Preparation

Import the pickle package to save the model

## Running without Docker

First, install flask:

```bash
pip install flask
```

Run the service:

```bash
python credit_card.py
```

Test it from python:

```python
import requests
url = 'http://localhost:9696/predict'
response = requests.post(url, json=customer)
result = response.json()
```

## Managing dependencies with Pipenv

Install `pipenv`:

```bash
pip install pipenv
```

Install the depencencies from the [Pipfile](Pipfile):

```bash
pipenv install
```

Enter the pipenv virtual environment:

```bash
pipenv shell
```

And run the code:

```bash
python credit_card.py
```

Alternatively, you can do both steps with one command:

```bash
pipenv run python credit_card.py
```

Now you can use the same code for testing the model locally.


## Running with Docker

Build the image (defined in [Dockerfile](Dockerfile))

```bash
docker build -t credit-card-prediction .
```

Run it:

```bash
docker run -it -p 9696:9696 credit-card-prediction:latest
```
