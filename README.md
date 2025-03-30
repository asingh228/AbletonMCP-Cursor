# 🎼 AI Music Composition with Cursor + Ableton MCP

This project connects [Cursor IDE](https://www.cursor.so/) with [Ableton Live](https://www.ableton.com/) using the [AbletonMCP](https://github.com/ahujasid/ableton-mcp) server to enable **natural language-driven music composition**.

By writing prompts in Cursor, you can generate structured Python code that controls Ableton Live — creating tracks, clips, instruments, and MIDI content through a socket-based API.

---

## 🚀 What You Can Do

- Compose music using plain English prompts
- Generate rich chord progressions and melodies in a chosen key
- Automatically create structured MIDI clips with melody, harmony, rhythm
- Control playback, tempo, and instrument loading inside Ableton Live
- Structure music with clear sections like *Intro → Build → Climax*

---

## 🧠 How It Works

1. Cursor uses a custom ruleset to guide the LLM toward musical structure and theory.
2. You write a prompt like:
   > “Create a 1-minute emotional cinematic score in A minor, like Interstellar.”
3. The model outputs **MCP-compatible Python commands**:
   - `create_midi_track`
   - `set_track_name`
   - `create_clip`
   - `add_notes_to_clip`
   - `load_browser_item`
4. These commands are sent to the **Ableton MCP server**, which applies them live in Ableton.

---

## 📦 Prerequisites

- **Ableton Live 10 or newer**
- **Python 3.8+**
- **[uv package manager](https://docs.astral.sh/uv/getting-started/installation/)**  
  - macOS: `brew install uv`

---

## 🎛️ Setup Instructions

### 1. Install AbletonMCP

Clone or install the [Ableton-MCP GitHub repo](https://github.com/ahujasid/ableton-mcp):

```bash
npx -y @smithery/cli install @ahujasid/ableton-mcp --client claude
