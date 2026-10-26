# Claude Code Video Toolkit

Skills, MCP servers, and tools for producing video with Claude Code. Covers programmatic video (Remotion, Manim), screen recording, YouTube clipping, and FFmpeg post-processing.

`February 2026`

---

## Table of Contents

- [Programmatic Video (Remotion)](#programmatic-video-remotion) — React components rendered to MP4
- [Math & Science Animation (Manim)](#math--science-animation-manim) — 3Blue1Brown-style explainers
- [Screen Recording & Demos](#screen-recording--demos) — Product walkthroughs via Playwright
- [YouTube Clipping & Subtitles](#youtube-clipping--subtitles) — Download, chapter, clip, translate
- [FFmpeg & Post-Processing](#ffmpeg--post-processing) — Encode, resize, compress, concat
- [Recommended Stacks](#recommended-stacks)
- [Further Reading](#further-reading)

---

## Programmatic Video (Remotion)

*Write React components. Get MP4s. No timeline editor, no After Effects. Claude describes each frame in TypeScript, Remotion renders it.*

### Remotion Agent Skills (Official)

The official Remotion skill for Claude Code. Went viral in January 2026 — 6M+ views on the launch demo, 25k+ installs in the first week. Teaches Claude how to write correct Remotion code: `useCurrentFrame()`, `interpolate()`, `spring()`, `<Sequence>`, `<Composition>`. Without this, Claude tries to use web animation patterns that break during rendering.

| | |
|---|---|
| **Install** | `npx skills add remotion` |
| **Docs** | [remotion.dev/docs/ai/claude-code](https://www.remotion.dev/docs/ai/claude-code) |

One command to install. Then just describe what you want: "Create a 30-second product launch video with logo animation, feature callouts, and a CTA at the end." Claude writes the React components, Remotion renders to MP4.

What it's good for: marketing videos, product demos, data visualizations, explainers, branded content, onboarding videos. Anything that's motion graphics rather than live footage.

### Claude Code Video Toolkit (digitalsamba)

The most complete video production setup for Claude Code. Not just a skill — it's a full project template with skills, slash commands, reusable components, transitions, a theme system, brand profiles, and a multi-session project lifecycle.

| | |
|---|---|
| **Author** | digitalsamba |
| **Source** | [digitalsamba/claude-code-video-toolkit](https://github.com/digitalsamba/claude-code-video-toolkit) |

What's in the box:
- **Skills** — Remotion, ElevenLabs, FFmpeg, Playwright expertise
- **Commands** — `/video` (start a new video project), `/record-demo` (screen recording), `/brand` (create brand profile), `/contribute`
- **9 reusable components** — titles, callouts, transitions, lower thirds
- **7 custom transitions** + 4 official Remotion transitions
- **Theme system** — `ThemeProvider` + `useTheme` for consistent styling
- **Brand profiles** — define colors, fonts, voice settings in `brands/my-brand/`
- **Project lifecycle** — planning, assets, review, audio, editing, rendering, complete

The project system auto-generates a `CLAUDE.md` per video project so Claude can pick up where you left off across sessions.

### brand-film

Narrated, on-brand explainer films from a deck, a document or a story. Instead of Remotion, each scene is a plain HTML page whose `render(t)` draws any moment; headless Chrome steps it frame by frame and ffmpeg encodes it. The focus is brand fidelity and narration you can trust.

| | |
|---|---|
| **Author** | davidscotttufts |
| **Source** | [davidscotttufts/brand-film](https://github.com/davidscotttufts/brand-film) |
| **Install** | `/plugin marketplace add davidscotttufts/brand-film` or `npx skills add davidscotttufts/brand-film` |
| **Example** | [48-second film, made with it](https://davidscotttufts.github.io/brand-film/) |

What's in the box:
- **Brand tokens** — exact colours (contrast-checked), typefaces, official logo files and narrator in one `brand-tokens.json`
- **Pronunciation lexicon** — write "ffmpeg", the voice is sent "eff eff em peg", the captions keep the written form
- **Listening check** — every ElevenLabs take is transcribed with speech-to-text and re-voiced if a word or brand name is wrong
- **Verified renders** — frame count, loudness and captions checked on the finished MP4; a lock file records how each take was made

---

## Math & Science Animation (Manim)

*The library behind 3Blue1Brown. Python-based, renders LaTeX, graphs, 3D objects, geometric proofs to video. Claude writes the scene code, Manim renders it.*

### Manim Skill (Yusuke710)

Claude Code plugin that handles the full Manim workflow: plan scenes, write code, render video, iterate based on your feedback. Uses Claude's plan mode for scene structure, then writes and renders until all scenes compile.

| | |
|---|---|
| **Author** | Yusuke710 |
| **Install** | `/plugin marketplace add Yusuke710/manim-skill` then `/plugin install manim-skill/manim-skill` |
| **Source** | [Yusuke710/manim-skill](https://github.com/Yusuke710/manim-skill) |

Also installs `manimce-best-practices` from adithya-s-k for correct ManimCE patterns.

### Math-To-Manim (HarleyCoops)

Goes further than a basic Manim skill — three separate AI pipelines (Claude, Gemini, Kimi K2.5) for generating Manim animations from text or images. 55+ working examples across physics, mathematics, CS, cosmology, and finance. Has a Claude Code plugin that requires no setup beyond cloning the repo.

| | |
|---|---|
| **Author** | HarleyCoops |
| **Install** | `git clone` then `claude --plugin-dir ./Math-To-Manim/skill` |
| **Source** | [HarleyCoops/Math-To-Manim](https://github.com/HarleyCoops/Math-To-Manim) |

### Manim MCP Server

Renders Manim scenes as an MCP server. Claude writes the scene code, sends it to the server, gets back a rendered MP4. Works with Claude Desktop, Cursor, and any MCP client. Public and open-source.

| | |
|---|---|
| **Source** | [Medium writeup](https://medium.com/@omchoksi108/i-built-a-public-manim-mcp-server-now-claude-can-produce-real-3blue1brown-videos-on-demand-050995551c4e) |

---

## Screen Recording & Demos

*Record your app in action. Claude drives a browser via Playwright, records the session, and outputs video.*

### Playwright MCP `--save-video`

Not a separate plugin — just a flag on the Playwright MCP you probably already have installed. Records browser sessions to video file.

```bash
claude mcp add playwright -s user -- npx @playwright/mcp@latest --save-video=1920x1080
```

Claude navigates your app, clicks through flows, fills forms — and it's all recorded. Good for product demos, bug reproductions, onboarding walkthroughs. The digitalsamba video toolkit also has a `/record-demo` command that feeds Playwright recordings into Remotion for post-processing (branded intros, transitions, captions).

---

## YouTube Clipping & Subtitles

### Youtube Clipper Skill — 633 stars

Download YouTube videos, generate AI-powered semantic chapters (not just mechanical time splits), clip segments, translate subtitles to bilingual format, and burn subtitles into videos. Chapters are 2-5 minutes each, based on content analysis.

| | |
|---|---|
| **Author** | op7418 |
| **Install** | `npx skills add https://github.com/op7418/Youtube-clipper-skill` |
| **Source** | [op7418/Youtube-clipper-skill](https://github.com/op7418/Youtube-clipper-skill) |

What it does:
- Downloads video + English subtitles via yt-dlp
- AI analyzes subtitle content to generate semantic chapters
- You pick which chapters to clip
- FFmpeg extracts clips with frame-accurate timing
- Batch translates subtitles to bilingual (default: Chinese/English, 95% API call reduction)
- Burns subtitles into video with customizable styling
- Generates social media summaries for each clip

Requires: `yt-dlp`, `ffmpeg` (with libass), `pysrt`.

---

## FFmpeg & Post-Processing

### FFmpeg Skill (Video Toolkit)

Part of the digitalsamba video toolkit. FFmpeg patterns specifically for Remotion workflows: GIF-to-MP4 conversion (web-friendly flags), resolution/format normalization, CRF-based compression, platform-specific encoding presets, audio extraction, and batch processing.

| | |
|---|---|
| **Source** | [skills.sh/digitalsamba/.../ffmpeg](https://skills.sh/digitalsamba/claude-code-video-toolkit/ffmpeg) |

Common patterns:

```bash
# Normalize to 1080p 30fps for Remotion
ffmpeg -i raw.mp4 \
  -vf "scale=1920:1080:force_original_aspect_ratio=decrease,pad=1920:1080:(ow-iw)/2:(oh-ih)/2,fps=30" \
  -c:v libx264 -crf 18 -preset slow \
  -movflags faststart output.mp4

# Aggressive compression for web preview
ffmpeg -i input.mp4 -c:v libx264 -crf 28 -preset fast -c:a aac -b:a 96k output.mp4

# Batch GIF to MP4
for f in assets/*.gif; do
  ffmpeg -i "$f" -movflags faststart -pix_fmt yuv420p \
    -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" \
    "public/demos/$(basename "$f" .gif).mp4"
done
```

---

## Recommended Stacks

### Motion graphics (marketing, product demos, explainers)

```bash
# Remotion for video generation
npx skills add remotion

# Playwright for screen recording
claude mcp add playwright -s user -- npx @playwright/mcp@latest --save-video=1920x1080
```

Or use the digitalsamba video toolkit for the full pipeline with brand profiles and slash commands.

### Math/science educational content

```bash
# Manim for 3Blue1Brown-style animations
/plugin marketplace add Yusuke710/manim-skill
/plugin install manim-skill/manim-skill

# System deps (macOS)
brew install cairo pkg-config ffmpeg
uv tool install manim
```

### YouTube content repurposing

```bash
# Clipper skill
npx skills add https://github.com/op7418/Youtube-clipper-skill

# Dependencies
pip install yt-dlp pysrt
brew install ffmpeg  # needs libass support
```

---

## Quick Reference

| Tool | Type | What it does | Setup |
|------|------|-------------|-------|
| Remotion Agent Skills | Skill | React-to-MP4 video generation | One command |
| Video Toolkit (digitalsamba) | Skills + Commands | Full video production pipeline | Clone repo |
| brand-film | Plugin | Narrated brand films from HTML + ElevenLabs | Plugin install |
| Manim Skill (Yusuke710) | Plugin | 3Blue1Brown-style math animation | Plugin install |
| Math-To-Manim | Plugin | Multi-pipeline Manim (Claude/Gemini/Kimi) | Clone repo |
| Manim MCP Server | MCP | Renders Manim scenes server-side | Config needed |
| Youtube Clipper | Skill | Download, chapter, clip, subtitle | One command |
| Playwright `--save-video` | MCP flag | Screen recording | One command |
| FFmpeg Skill | Skill | Video encoding and processing | Part of Video Toolkit |

---

## Further Reading

| Resource | |
|----------|---|
| [Remotion + Claude Code docs](https://www.remotion.dev/docs/ai/claude-code) | Official setup guide |
| [Remotion examples gallery](https://www.remotion.dev/showcase) | What people have built |
| [digitalsamba/claude-code-video-toolkit](https://github.com/digitalsamba/claude-code-video-toolkit) | Full toolkit with docs |
| [Manim Community docs](https://docs.manim.community/) | ManimCE reference |
| [op7418/Youtube-clipper-skill](https://github.com/op7418/Youtube-clipper-skill) | YouTube clipper docs |
| [awesome-claude-code](https://github.com/jqueryscript/awesome-claude-code) | Master list of all Claude Code tools |

---

## Contributing

Know a video tool that should be on this list? Open a PR.

To get included:
- Has to work with Claude Code (not just Cursor/Copilot)
- Has to be specifically useful for video/audio production
- Has to be maintained or from a trusted source

---

## License

[MIT](LICENSE)

---

*[wilwaldon.com](https://wilwaldon.com) · February 2026*
