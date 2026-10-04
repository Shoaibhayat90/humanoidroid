# HUMANOIDROID — Offline AI Assistant

**Live demo:** https://shoaibhayat90.github.io/humanoidroid/

> Your private AI assistant that runs entirely offline. No accounts, no cloud, nothing leaving your machine.

## Two backends

1. **Browser brain** — runs models directly in your browser via WebLLM + WebGPU (needs a WebGPU-capable GPU).
2. **Ollama** — connect to Ollama on your machine (`http://localhost:11434`) and use any model you've pulled.

## Features

- Streaming chat with markdown rendering
- Voice replies
- Thinking timer — see how long the model thought
- 30-minute model keep-alive
- Chat history
- Editable personality — make it yours

## Run it locally with Ollama

1. Install Ollama from [ollama.com](https://ollama.com) and launch it.
2. Pull a model: `ollama pull qwen3:1.7b` (fast) — verify with `ollama list`.
3. Save the HTML as `index.html` in your Downloads folder, then serve it over localhost (browsers block `file://` pages from reaching Ollama). In PowerShell, paste:

```powershell
cd $env:USERPROFILE\Downloads; $f=(Get-ChildItem 'index*.html'|Sort-Object LastWriteTime -Descending|Select-Object -First 1).FullName; Write-Host "Serving $f"; $l=New-Object Net.HttpListener; $l.Prefixes.Add('http://localhost:8000/'); $l.Start(); Write-Host 'OPEN http://localhost:8000 IN CHROME'; while($l.IsListening){ $c=$l.GetContext(); $b=[IO.File]::ReadAllBytes($f); $c.Response.ContentType='text/html'; $c.Response.OutputStream.Write($b,0,$b.Length); $c.Response.Close() }
```

4. Open `http://localhost:8000` in Chrome (leave PowerShell open).
5. Click the Ollama card → Refresh → click the `qwen3:1.7b` card → Connect. First answer is slowest — the model is loading into memory.

## Privacy

Everything runs locally. The browser backend never touches the network for inference; the Ollama backend talks only to your own localhost. No analytics, no accounts, no telemetry.

## License

MIT — see [LICENSE](LICENSE).

---

Built by [Shoaib Hayat](https://github.com/Shoaibhayat90).
