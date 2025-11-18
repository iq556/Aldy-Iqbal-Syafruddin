<section id="kontak" class="section">
  <h2>Kontak</h2>
  <div class="card">
    <p>Tertarik bekerja sama atau punya ide? Kirim pesan — saya akan membalas secepatnya.</p>
    <form action="https://formspree.io/f/your-id" method="POST">
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">
        <div>
          <label for="nama">Nama</label>
          <input id="nama" name="nama" type="text" required
            style="width:100%;padding:10px;border-radius:10px;border:1px solid #334155;background:#0c1323;color:var(--text)">
        </div>
        <div>
          <label for="email">Email</label>
          <input id="email" name="email" type="email" required
            style="width:100%;padding:10px;border-radius:10px;border:1px solid #334155;background:#0c1323;color:var(--text)">
        </div>
      </div>
      <div style="margin-top:12px">
        <label for="pesan">Pesan</label>
        <textarea id="pesan" name="pesan" rows="5" required
          style="width:100%;padding:10px;border-radius:10px;border:1px solid #334155;background:#0c1323;color:var(--text)"></textarea>
      </div>
      <div style="margin-top:12px;display:flex;gap:10px;flex-wrap:wrap">
        <button class="btn btn-primary" type="submit">Kirim</button>
        <!-- Email langsung -->
        <a class="btn btn-outline" href="mailto:aldyiqbalsyafruddin1@gmail.com">Email langsung</a>
        <!-- Instagram -->
        <a class="btn btn-outline" href="https://instagram.com/Aldy_Iqbal_syafruddin">Instagram</a>
      </div>
    </form>
  </div>
</section>

<footer>
  <div>© <span id="year"></span> Aldy Iqbal Syafruddin</div>
  <div class="social">
    <a href="mailto:aldyiqbalsyafruddin1@gmail.com">Email</a>
    <a href="https://instagram.com/Aldy_Iqbal_syafruddin">Instagram</a>
    <a href="https://github.com/aldy">GitHub</a>
    <a href="https://linkedin.com/in/aldy">LinkedIn</a>
    <a href="https://twitter.com/aldy">Twitter</a>
    <a href="https://dribbble.com/aldy">Dribbble</a>
  </div>
</footer>
from fastapi import FastAPI, UploadFile
from summarizer import summarize_journal
from generator import generate_content

app = FastAPI()

@app.post("/summarize/")
async def summarize(file: UploadFile):
    content = await file.read()
    summary = summarize_journal(content)
    return {"summary": summary}

@app.post("/generate/")
async def generate(prompt: str):
    result = generate_content(prompt)
    return {"content": result}

