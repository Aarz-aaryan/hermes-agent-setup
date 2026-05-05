# MLOps Research — DSPy Declarative LM Programs

## Concept
DSPy is a framework for building and optimizing LLM pipelines declaratively. Instead of writing prompt strings, you define modules and compile them to optimize performance.

## Core Idea
```python
import dspy

# Define a simple module
class BasicQA(dspy.Module):
    def __init__(self):
        self.propose = dspy.ChainOfThought("question -> answer")
        
    def forward(self, question):
        return self.propose(question=question)

# Use it
qa = BasicQA()
response = qa(question="What is the capital of France?")
```

## Signatures
Signatures define input/output behavior:
```python
# Simple signature
"question -> answer"

# Multiple inputs/outputs
"context, question -> answer, confidence"

# With descriptions
dspy.Signature("context: Wikipedia paragraph, question: user query -> answer: short answer, confidence: 0-1")
```

## Modules

### dspy.ChainOfThought
```python
class QAWithCoT(dspy.Module):
    def __init__(self):
        self.chain = dspy.ChainOfThought("question -> answer")
    
    def forward(self, question):
        return self.chain(question=question)
```

### dspy.MultiChainComparison
Compares outputs from multiple chains:
```python
class CompareAnswers(dspy.Module):
    def __init__(self):
        self.compare = dspy.MultiChainComparison(CoT_signature, num_chains=3)
```

### dspy.Retrieve
```python
class RAG(dspy.Module):
    def __init__(self):
        self.retrieve = dspy.Retrieve(k=3)
        self.generate_answer = dspy.ChainOfThought("context, question -> answer")
    
    def forward(self, question):
        context = self.retrieve(question).passages
        return self.generate_answer(context=context, question=question)
```

## Compilation (Optimization)

### BootstrapFewShot (metric learning)
```python
from dspy.teleprompt import BootstrapFewShot

teleprompter = BootstrapFewShot(metric=my_metric)
compiled_qa = teleprompter.compile(student=BasicQA(), trainset=train_examples)
```

### LabeledFewShot
```python
from dspy.teleprompt import LabeledFewShot

teleprompter = LabeledFewShot(k=8)
compiled_qa = teleprompter.compile(BasicQA(), trainset=train_examples)
```

## Predict Module
```python
# Basic prediction
predict = dspy.Predict("question -> answer")
result = predict(question="What is 2+2?")

# With settings
predict = dspy.Predict("question -> answer", max_tokens=50, temperature=0.3)
```

## Connecting to Different LLMs

### OpenAI
```python
llm = dspy.OpenAI(model="gpt-4")
dspy.settings.configure(lm=llm)
```

### Anthropic
```python
llm = dspy.Anthropic(model="claude-3-opus")
dspy.settings.configure(lm=llm)
```

### Local (llama.cpp via OAI-compatible server)
```python
llm = dspy.LM(model="/path/to/model.gguf", api_base="http://localhost:8080")
dspy.settings.configure(lm=llm)
```

## Backward Compatibility
If DSPy 3.x changes APIs:
```python
# Check version
import dspy
print(dspy.__version__)

# Import legacy if needed
import dspy.lm as legacy_lm
```

## Metrics
```python
def my_metric(example, prediction, trace=None):
    return prediction.answer == example.answer

# Or with confidence
def my_metric(example, prediction, trace=None):
    return prediction.answer == example.answer and prediction.confidence > 0.8
```

## Best Practices
- Start with simple Predict, upgrade to ChainOfThought if needed
- Compile on a small validation set before full evaluation
- Use Retrieve for RAG tasks
- Monitor cost during compilation (many LLM calls)
