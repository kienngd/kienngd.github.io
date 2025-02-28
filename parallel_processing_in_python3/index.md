# Parallel Processing In Python3


## 🤔 Why Use Parallel Processing?

When running 🐍 Python programs, some tasks take a long ⏳ time to complete. For example, calling an external 🌐 API or reading large 📂 files. If we run these tasks one by one, it can be 🐌 slow. Instead, we can run them in parallel to save ⏱️ time.

<!--more-->

## 🚀 Introduction to `concurrent.futures`

🐍 Python provides the `concurrent.futures` module to run tasks in parallel. It has two main classes:

- `ThreadPoolExecutor`: Uses 🧵 threads, good for I/O-bound tasks (e.g., API calls, file 📁 I/O).
- `ProcessPoolExecutor`: Uses 🖥️ processes, better for CPU-bound tasks (e.g., 🧮 calculations, data 📊 processing).

### 🔥 Example: Running API Calls in Parallel

Here is a simple example using `ThreadPoolExecutor` to make multiple 🌍 API requests faster.

```python
import concurrent.futures
import requests

def fetch_url(url):
    response = requests.get(url)
    return url, response.status_code

urls = [
    "https://jsonplaceholder.typicode.com/posts/1",
    "https://jsonplaceholder.typicode.com/posts/2",
    "https://jsonplaceholder.typicode.com/posts/3",
]

with concurrent.futures.ThreadPoolExecutor() as executor:
    results = executor.map(fetch_url, urls)

for url, status in results:
    print(f"URL: {url}, Status Code: {status}")
```

### 🧐 Explanation
- We define a function `fetch_url` to get data 📡 from a URL.
- We use `ThreadPoolExecutor` to run `fetch_url` for multiple URLs in parallel.
- The `executor.map` method applies the function to all URLs and returns results.

## 🔄 Other Parallel Processing Methods in Python

Besides `concurrent.futures`, 🐍 Python has other ways to run tasks in parallel:

- `multiprocessing` module: Runs tasks in separate 🖥️ processes.
- `asyncio` module: Handles asynchronous tasks efficiently ⚡.
- `joblib` library: Useful for parallel computing in 🧠 machine learning.

Each method has its own use case. `concurrent.futures` is a simple and effective choice for many parallel tasks.

## 🎯 Conclusion

Using `concurrent.futures`, we can speed up ⏩ tasks that involve I/O operations like API calls. It is easy 🤓 to use and improves performance significantly 🚀. If you need parallel processing in 🐍 Python, give it a try! 💡

