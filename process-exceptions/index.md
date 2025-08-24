# How to Properly Catch and Raise Exceptions


# 🐍 How to Properly Catch and Raise Exceptions – A Guide for Junior Developers
(This article was created by Qwen AI)

Handling exceptions correctly isn't just about preventing crashes — it makes your code **more stable**, **easier to debug**, and **simpler to maintain**. Here are simple, practical rules every junior developer should follow.

---

## ✅ Only catch an exception when you know what to do

> ❌ Don't catch an exception just "because you can".

```python
def c():
    try:
        save_data()
    except OSError:
        pass  # ❌ Wrong! This "swallows" the error — no one will know something went wrong
```

> ✅ Only catch it if you can **handle it meaningfully**:

```python
try:
    load_config()
except FileNotFoundError:
    return DEFAULT_CONFIG  # ✅ Good: use default if file is missing
```

---

## ✅ If you only log, then re-raise the exception

When you're in a **low-level function** (e.g., writing to a file, calling an API), you might want to **log the error for debugging**, but if you **can't fully handle it**, you **must re-raise**.

```python
def c():
    try:
        write_to_file(data)
    except OSError as e:
        logging.error(f"[c()] Failed to write file: {e}")
        raise  # ✅ Important: propagate the error up for higher-level handling
```

> 🔹 Using `raise` (without arguments) preserves the **original traceback** — very helpful for debugging later.

---

## ✅ Handle errors where you have enough context

> ✅ Higher-level functions (like `a()`) are usually closest to the user, so they're the **best place** to:
- Show user-friendly error messages.
- Suggest actions (retry, check permissions, etc.).
- Log high-level system events.

```python
def a():
    try:
        b()
    except OSError:
        print("Failed to save data. Please check your disk space.")
```

---

## ✅ When should you NOT re-raise?

Only when you’ve **fully resolved** the issue and the program can **safely continue**:

```python
def get_user_setting():
    try:
        return read_from_file("setting.txt")
    except FileNotFoundError:
        return "default"  # ✅ Valid: no file → use default value
```

→ In this case, the error is not a failure — it's part of a **valid execution path**.

---

## 🚫 What you should NOT do

- ❌ Catch an exception and just `pass` or use `raise Exception("...")` (this loses the traceback).
- ❌ Catch the same error at multiple levels without adding value.
- ❌ Log and then stay silent — if you can't handle it, don’t hide it.

---

## 💡 The 3 Golden Rules

1. **Don’t catch if you don’t know what to do.**
2. **Logged the error? Still `raise` if it’s not fully handled.**
3. **Handle the error where you have user or system context.**

---

> 📌 Remember: **Exceptions are not bad** — what matters is that you **handle them responsibly**.

---

*— Written by a dev who once swallowed an exception and spent 3 hours debugging* 😅

