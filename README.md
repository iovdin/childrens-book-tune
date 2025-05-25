# AI Children's Book Generator with Tune

This repository contains an AI-powered workflow for creating a children's book using [tune](https://github.com/iovdin/tune) - a tool that enables chatting with LLMs using .chat text files.

## 📁 Project Structure

```
├── chats/          # Chat files for generating poems
├── pictures/       # Generated illustrations (PNG)
├── chapters/       # Individual LaTeX chapter files
├── book.md         # Markdown version of the complete book
├── book.tex        # Main LaTeX file for the book
├── book.pdf        # Compiled PDF book
├── system.prompt   # Main prompt for creating new chapters/poems
├── append.tool.mjs # Custom tool for appending content to files
└── append.schema.json # Schema for the append tool
```

## 🎯 What This Project Does

This workflow creates a collection of simple, mischievous poems for children in Russian, complete with illustrations. Each poem:
- Has 2 quatrains (8 lines total)
- Uses simple words and rhymes
- Has a playful/mischievous spirit
- Comes with a simple black and white stickman illustration

## 🚀 How to Use Tune for AI Workflows

### Prerequisites
1. Install [tune](https://github.com/iovdin/tune)
2. Have LaTeX installed (XeLaTeX specifically) for PDF compilation
3. Configure your AI model access (Claude/OpenAI)

### Creating a New Poem

Create a new `.chat` file in the `chats/` directory and start a conversation. Here's an example:

**File: `chats/playground.chat`**
```chat
system: @@system
user: make a poem about "playground"
assistant: I'll create a playful poem about the playground following your workflow:

### 1. Story idea
A mischievous child at the playground who gets into fun trouble on the swings, slides, and sandbox.

### 2. First version
Качели-карусели крутятся быстрей,
Песочек насыпаю прямо на людей.
Со горки еду вниз как быстрая стрела,
Штаны порвал, но мама не ругала!

### 3. Checking rhyme
Simple rhymes: быстрей-людей, стрела-ругала ✓

### 4. Adding to book.md...
[AI continues with the full workflow automatically]
```

Then press `Shift+Enter` in tune to execute the workflow. The AI will automatically follow all 9 steps from the system prompt.

### The Automated Workflow

The `system.prompt` defines a 9-step process that runs automatically:

1. **Generate story idea** - AI creates a concept for the poem
2. **Write first version** - Creates the initial poem
3. **Check rhyme** - Validates and improves rhyming
4. **Add to book.md** - Appends the poem using the `append` tool
5. **Create illustration** - Generates a PNG image using OpenAI image generation
6. **Read book.tex** - Checks current LaTeX structure
7. **Create chapter** - Makes a new `.tex` file in `chapters/`
8. **Update book.tex** - Adds the new chapter using `patch` tool
9. **Compile book** - Runs `xelatex book.tex` to generate PDF

### Custom Tools Used

- **@append** - Adds content to files without overwriting
- **@patch** - Updates files using diff-style patches
- **@openai_imgen** - Generates illustrations
- **@sh** - Executes shell commands (like LaTeX compilation)
- **@rf** - Reads file contents
- **@wf** - Writes new files

## 📝 Example Poem Structure

Each poem follows this format in the final book:

```latex
\vspace*{\fill}
\begin{center}
  {\huge\textbf{Пора спать}}
  \vspace{1.5em}
  \includegraphics[width=0.7\textwidth]{pictures/sleep.png}
  \vspace{4em}
  \parbox{0.6\textwidth}{
    \LARGE
    \begin{spacing}{1.2}
      Мальчик спать совсем не хочет,\\
      На подушке он хохочет.\\
      Но приходит тишина,\\
      И закрылись вдруг глаза. %
    \end{spacing}
  }
\end{center}
\vspace*{\fill}
```

## 🎨 Illustration Style

All illustrations are generated with this prompt style:
- Simple black and white stickman drawings
- Childlike, rough lines
- Minimalist details
- Landscape orientation
- Low quality (for speed)

## 🔧 Configuration

### System Prompt Features
- **Language**: Russian poems for children
- **Style**: Simple words, mischievous/playful tone
- **Format**: 2 quatrains per poem
- **Workflow**: Fully automated from idea to compiled PDF

### File Templates
- Chapters follow the template in `chapters/01_sleep.tex`
- Illustrations stored as PNG files in `pictures/`
- Markdown version maintained in `book.md`

## 📚 Building the Complete Book

The workflow automatically:
1. Maintains a markdown version (`book.md`)
2. Creates individual LaTeX chapters
3. Updates the main `book.tex` file
4. Compiles to PDF using XeLaTeX

To manually compile:
```bash
xelatex book.tex
```

## 🤝 Contributing

To add new poems:
1. Create a new chat file with your topic
2. Let the AI workflow handle the creation process
3. The poem will be automatically added to all formats

## 📄 License

This is a personal project for creating a children's book. Feel free to use the workflow structure for your own AI-powered book projects!

---

*This book is being created for educational and entertainment purposes using AI assistance through the tune framework.*