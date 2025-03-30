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
   `"Create a 1-minute emotional cinematic score in A minor, like Interstellar."`
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
```

✅ This provides a socket interface between Python and Ableton.

---

### 2. Install the Ableton Remote Script

1. Download `AbletonMCP_Remote_Script/__init__.py` from the [AbletonMCP GitHub](https://github.com/ahujasid/ableton-mcp)
2. Copy it into your **MIDI Remote Scripts** directory:

#### macOS

- `/Applications/Ableton Live XX.app/Contents/App-Resources/MIDI Remote Scripts/`
- Or: `~/Library/Preferences/Ableton/Live XX/User Remote Scripts/`

#### Windows

- `C:\Users\[Username]\AppData\Roaming\Ableton\Live XX\Preferences\User Remote Scripts\`

> Replace `XX` with your Ableton version (e.g., `11`)

3. Create a new folder named `AbletonMCP` and paste the `__init__.py` file inside.

4. Launch Ableton Live → Preferences → Link, Tempo & MIDI:

- Control Surface: `AbletonMCP`
- Input: `None`
- Output: `None`

---

### 3. Connect Cursor to MCP

In **Cursor**, go to:

`Settings → MCP`

Paste this:

```
{
    "mcpServers": {
        "AbletonMCP": {
            "command": "uvx",
            "args": [
                "ableton-mcp"
            ]
        }
    }
}
```

And run this command in Terminal:

```bash
uvx ableton-mcp
```

⚠️ Only run **one** instance of MCP — in Cursor **or** Claude, not both.

---

## 🧩 Add Custom Rules to Cursor

1. Go to `Cursor → Settings → Custom Rules`
2. Create a new ruleset (or use USER Rules):  
   **Name:** `Music Composition (Ableton MCP)`
3. Paste in the contents of:  
   [`Cursor-UserRules-MusicProduction.txt`](./Cursor-UserRules-MusicProduction.txt)
4. Save the ruleset and make sure it's active

These rules guide the model to:

- Choose a key signature first
- Compose in functional harmony
- Write melodies that match the chords
- Structure music in sections (e.g., Intro, Build, Drop)
- Output clean, usable, and musical MCP commands

---

## ✍️ Example Prompt

```text
I want to create a 1-minute cinematic composition inspired by Interstellar.
It should be in A minor, have a slow tempo, and evolve in three parts:
- Intro with soft piano and pads
- Build with low strings and pulsing rhythm
- Climax with high strings, layered chords, and percussion
```

Cursor will respond with:

- Key selection
- Chord progression (e.g., i–VI–III–VII)
- Track creation (Piano, Strings, Percussion, Pads)
- Clip creation and note data using scale-aligned pitches
- Commands to load instruments from Ableton’s browser

---

## 🛠️ Example MCP Commands (Generated by the LLM)

```python
create_midi_track(index=0)
set_track_name(track_index=0, name="Cinematic Piano")
load_browser_item(track_index=0, item_uri="instrument_uri_here")

create_clip(track_index=0, clip_index=0, length=8.0)
add_notes_to_clip(track_index=0, clip_index=0, notes=[
    {"pitch": 57, "start_time": 0.0, "duration": 1.0, "velocity": 100, "mute": False},
    ...
])
```

---

## 🎹 Supported Capabilities

- 🎵 Create/rename MIDI and audio tracks
- 🎹 Add MIDI clips and notes
- 🥁 Load instruments and effects from the browser
- 🎛️ Control tempo, playback, and clip triggering
- 🧠 Query session and track data
- 🔄 Structured song building via sections and motifs

---

## 💡 Tips for Best Results

- Be specific: define the style, emotion, tempo, and structure
- Mention a reference track or artist (e.g., "like Hans Zimmer")
- Use section language: *Intro → Build → Drop → Outro*
- Let the LLM choose the key if unsure — it will guide everything else
- Review note data for realism, phrasing, and spacing

---

## 📂 File Reference

- [`Cursor-UserRules-MusicProduction.txt`](./Cursor-UserRules-MusicProduction.txt)  
  A detailed set of LLM guidance rules to enforce musical theory and structure in generations.

---

## 🧪 Troubleshooting

- 🔌 **Connection issues**: Ensure AbletonMCP is loaded and only one MCP server is running.
- ⏱️ **Timeouts**: Try simplifying your request or generating one section at a time.
- 🔁 **No response in Ableton**: Restart Ableton, Cursor, and re-check the Remote Script setup.

---

## 📎 Related Links

- 🎛️ [AbletonMCP GitHub](https://github.com/ahujasid/ableton-mcp)
- 🧠 [Cursor IDE](https://www.cursor.so/)
- 🎓 [uv Package Manager](https://docs.astral.sh/uv/getting-started/installation/)

---

## 📝 License

This project is MIT licensed.

Please follow the licensing terms for:
- [Ableton Live](https://www.ableton.com/en/legal/)
- [AbletonMCP Project](https://github.com/ahujasid/ableton-mcp)

---

## 🙏 Credits

- 🔧 Built on [AbletonMCP](https://github.com/ahujasid/ableton-mcp) by Siddharth Ahuja
- ✍️ Prompt system designed for use with Cursor + OpenAI models
- 🎶 Inspired by film scoring, AI-assisted production, and modern composition workflows
