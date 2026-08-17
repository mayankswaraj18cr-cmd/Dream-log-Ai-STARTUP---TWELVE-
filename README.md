# 🌙 DreamLog AI

### Privacy-Focused AI Dream Journal

**DreamLog AI** is a browser-based dream journaling application that combines personal dream logging with locally hosted AI analysis through **Ollama**. Users can record dreams, moods, clarity levels, and themes, then use local AI models to generate thoughtful dream interpretations and identify recurring patterns across multiple entries. 

---

## ✨ Features

* 🌙 **Dream Logging** — Record and save detailed dream descriptions.
* 😊 **Mood Tracking** — Associate a mood with every dream.
* ⭐ **Clarity Rating** — Rate dream clarity from 1–5.
* 🏷️ **Theme Tags** — Tag dreams with themes such as Flying, Falling, Chase, Water, Love, Exam, and more.
* 📚 **Dream History** — Browse previously recorded dreams.
* 🧠 **AI Dream Interpretation** — Generate AI-assisted interpretations using Ollama.
* 🔮 **Pattern Analysis** — Analyze recurring symbols and themes across dreams.
* 📊 **Mood Distribution** — Visualize recorded mood frequency.
* ☁️ **Theme Cloud** — Display frequently occurring dream themes.
* 💾 **Local Storage** — Store dream entries in the browser using `localStorage`.
* 🔌 **Local AI Connection** — Connect to an Ollama server running locally.
* 📱 **Mobile-Friendly Interface** — Designed around a compact mobile-first layout.
* 📴 **Offline-First Logging** — Dreams can be recorded without an AI connection.  

---

## 🧠 AI-Powered Interpretation

DreamLog AI can connect to a locally running Ollama server.

The application defaults to:

```text
http://localhost:11434
```

Available model options in the interface include:

```text
llama3.2
mistral
gemma2
qwen2.5
```

When connected, the application retrieves the available Ollama models and allows the user to select one.  

The AI interpretation prompt asks for:

1. **2–3 key symbols** and what they may represent.
2. An **overall emotional theme**.
3. **One gentle personal insight**.

The implementation explicitly instructs the AI to remain warm, thoughtful, and non-prescriptive. 

---

## 🔮 Dream Pattern Analysis

DreamLog AI can analyze multiple logged dreams to identify broader patterns.

At least **three dreams** are required before pattern analysis becomes available. 

The pattern analysis considers:

* Recurring symbols or themes
* Dominant emotional states
* Changes in themes over time
* An integrative insight about the observed patterns

The application sends recent dream information to the connected Ollama model to generate the AI pattern report. 

---

## 📊 Built-In Statistics

Once dreams have been logged, the Patterns section provides:

```text
Dreams
Average Clarity
Interpreted Dreams
```

It also calculates:

* Mood distribution
* Theme frequency
* Recurring symbols
* Average dream clarity
* Number of interpreted dreams 

---

## 📝 Logging a Dream

A dream entry contains:

```javascript
{
  id,
  text,
  mood,
  clarity,
  tags,
  date,
  interpretation
}
```

When a dream is saved, the application stores the entry in the browser's local storage. 

The logging interface provides predefined themes including:

* Flying
* Falling
* Chase
* Water
* House
* Animals
* Death
* Love
* Lost
* Teeth
* Exam
* People 

---

## 💾 Data Storage

DreamLog AI uses the browser's **LocalStorage** mechanism.

The stored collection is accessed using:

```javascript
localStorage.getItem('dl_dreams')
```

and updated with:

```javascript
localStorage.setItem('dl_dreams', JSON.stringify(dreams))
```

This means the application's dream records are maintained in the browser rather than requiring a traditional remote database.  

---

## 🔌 Ollama Integration

DreamLog AI communicates with Ollama through its HTTP API.

### Check Connection

```text
/api/tags
```

The application uses this endpoint to check whether Ollama is available and retrieve installed models. 

### Generate AI Response

```text
/api/generate
```

The application sends the selected model and prompt to Ollama and receives the generated response. 

Conceptually:

```text
DreamLog AI
     │
     ▼
Local Ollama Server
     │
     ▼
Selected Local Model
     │
     ▼
AI Interpretation
     │
     ▼
DreamLog AI
```

---

## 🖥️ Application Structure

The interface is divided into three primary sections:

```text
DreamLog AI
│
├── 🌙 Log
│   ├── Mood
│   ├── Clarity
│   ├── Dream Description
│   ├── Themes
│   └── Save Dream
│
├── 📖 Dreams
│   ├── Dream History
│   ├── Mood
│   ├── Clarity
│   ├── Themes
│   ├── Interpretation
│   └── Delete
│
└── ✨ Patterns
    ├── Dream Count
    ├── Average Clarity
    ├── Interpreted Count
    ├── Mood Distribution
    ├── Theme Cloud
    └── AI Pattern Report
```

These three tabs are directly implemented in the application interface.  

---

## 🎨 UI Design

DreamLog AI uses a dark, compact interface with:

* Dark background
* Purple accent colors
* Rounded cards
* Mood emoji controls
* Theme chips
* Dream cards
* Pattern statistics
* Responsive scrolling areas
* Connection status indicator

The application is constrained to a maximum width of **480px**, giving it a mobile-oriented interface. 

---

## 🛠️ Technology Stack

| Technology             | Purpose                          |
| ---------------------- | -------------------------------- |
| **HTML5**              | Application structure            |
| **CSS3**               | Interface and responsive styling |
| **Vanilla JavaScript** | Application logic                |
| **LocalStorage**       | Local dream persistence          |
| **Ollama API**         | Local AI inference               |
| **Fetch API**          | Communication with Ollama        |
| **JSON**               | Dream and API data handling      |

The project is implemented as a self-contained HTML application with its styling and JavaScript logic included in the file.  

---

## 🚀 Getting Started

### 1. Download or Clone the Project

Place the HTML file in your project directory.

### 2. Open the Application

Open the HTML file in a modern browser.

### 3. Optional — Start Ollama

If you want AI interpretation and pattern analysis, run an Ollama server locally.

DreamLog AI expects the default Ollama address:

```text
http://localhost:11434
```

You can change the URL through the connection field in the application. 

### 4. Connect

Click:

```text
Connect
```

The application checks the Ollama `/api/tags` endpoint and updates the connection indicator when successful. 

### 5. Start Journaling

Go to **Log**, choose your mood, set clarity, describe your dream, select relevant themes, and press **Save Dream**.

If Ollama is connected, the application can automatically request an interpretation. 

---

## 🔄 Application Workflow

```text
Write Dream
     │
     ▼
Select Mood
     │
     ▼
Set Clarity
     │
     ▼
Select Themes
     │
     ▼
Save Dream
     │
     ├──────────────► LocalStorage
     │
     ▼
Ollama Connected?
     │
   ┌─┴─┐
  Yes  No
   │    │
   ▼    ▼
AI Analysis   Saved Locally
   │
   ▼
Dream History
   │
   ▼
3+ Dreams?
   │
   ▼
Pattern Analysis
```

---

## 🔐 Privacy-Oriented Architecture

A key design characteristic of DreamLog AI is its use of **local browser storage** for dream records and optional **locally hosted Ollama inference** rather than requiring a conventional cloud AI backend.

The source explicitly identifies the application as **“OFFLINE AI”** and provides a local Ollama connection interface. 

This architecture is particularly suited to a journaling application where users may prefer keeping personal dream records on their own device.

---

## ⚠️ Important Note

Dream interpretations generated by the application are AI-generated reflections, not professional psychological or medical diagnoses. The implementation itself instructs the AI to provide **gentle, thoughtful, and non-prescriptive** insights. 

---

## 📱 Responsive Design

The application is designed around a mobile-first interface and includes:

* Touch-friendly controls
* Compact cards
* Scrollable content
* Responsive viewport configuration
* Mobile-sized layout

The viewport configuration specifically disables user scaling and establishes a responsive mobile presentation. 

---

## 🧩 Project Highlights

### Local-First Data

Dream entries are maintained in browser `localStorage`. 

### Local AI

AI functionality can be connected to an Ollama server running locally. 

### Structured Dream Data

Every entry tracks text, mood, clarity, tags, date, and optional interpretation. 

### Pattern Discovery

The application calculates mood and theme frequencies and can generate an AI pattern report from recent dreams. 

---

## 📌 Current Project Status

**Status: Functional Prototype**

Current implementation includes:

* ✅ Dream logging
* ✅ Dream persistence
* ✅ Mood tracking
* ✅ Clarity tracking
* ✅ Theme tagging
* ✅ Dream history
* ✅ Dream deletion
* ✅ Ollama connection
* ✅ AI dream interpretation
* ✅ Automatic interpretation after saving when connected
* ✅ Pattern statistics
* ✅ AI pattern reports
* ✅ Responsive UI

These capabilities are implemented directly in the provided application source.   

---

## 👨‍💻 Creator

**Mayank Swaraj**

**Mayank Creations**

A project focused on combining **local-first software, personal journaling, and locally hosted generative AI** into a simple browser experience.

---

## ⭐ DreamLog AI

> **Record your dreams. Understand your patterns. Keep your data close.**

**Built with HTML5 + CSS3 + Vanilla JavaScript + LocalStorage + Ollama AI.**
