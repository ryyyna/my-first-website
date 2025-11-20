# my-first-website
First website made by me
<!doctype html>
<html lang="uk">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Привіт — мій перший сайт</title>
  <style>
    :root{ --bg:#f7f8fb; --card:#fff; --accent:#ff6b81; --muted:#666 }
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; background:linear-gradient(180deg,#f7f8fb 0%, #eef6ff 100%); color:#223}
    .wrap{max-width:900px;margin:48px auto;padding:28px}
    .card{background:var(--card);border-radius:16px;box-shadow:0 8px 30px rgba(35,40,50,0.08);padding:32px;text-align:center}
    h1{margin:0 0 12px;font-size:28px;line-height:1.1}
    p.lead{margin:0 0 20px;color:var(--muted);font-size:16px}
    .kitten{display:block;margin:0 auto 18px;border-radius:12px;max-width:100%;height:auto;box-shadow:0 12px 30px rgba(34,40,50,0.08);cursor:pointer;transition:transform .25s ease}
    .kitten:hover{transform:translateY(-6px) scale(1.01)}
    .controls{display:flex;gap:10px;justify-content:center;flex-wrap:wrap}
    .btn{background:linear-gradient(90deg,var(--accent),#ff8aa2);border:none;color:white;padding:10px 16px;border-radius:10px;font-weight:600;cursor:pointer}
    .file{padding:10px;border-radius:10px;border:1px dashed #e2e8f0;background:#fbfdff}
    footer{margin-top:18px;color:var(--muted);font-size:13px}
    @media (max-width:520px){.wrap{margin:18px;padding:12px}.card{padding:18px}h1{font-size:20px}}
  </style>
</head>
<body>
  <main class="wrap">
    <section class="card" aria-labelledby="title">
      <h1 id="title">Привіт, це мій перший сайт! ❤️</h1>
      <p class="lead">Погляньте на фото милого котика та позбавтесь стресу — клацніть на котика, або завантажте свій.</p>

      <!-- Вбудована картинка (замість цієї можна підставити власну) -->
      <img id="kittenImg" class="kitten" src="https://placekitten.com/800/600" alt="Миленький котик" width="800" height="600">

      <div class="controls">
        <!-- Дозволяємо завантажити своє фото -->
        <label class="file">
          Завантажити своє фото
          <input id="fileInput" type="file" accept="image/*" style="display:none">
        </label>

        <!-- Кнопка для скидання на стандартне зображення -->
        <button id="resetBtn" class="btn" type="button">Повернути котика</button>
      </div>

      <footer>Порада: глибоко вдихніть, подивіться на котика 30 секунд — часто це допомагає розслабитись 😊</footer>
    </section>
  </main>

  <script>
    const img = document.getElementById('kittenImg');
    const fileInput = document.getElementById('fileInput');
    const resetBtn = document.getElementById('resetBtn');
    const defaultSrc = img.src;

    // Коли користувач завантажує файл — показуємо його замість прикладу
    fileInput.addEventListener('change', (e) => {
      const file = e.target.files && e.target.files[0];
      if (!file) return;
      if (!file.type.startsWith('image/')){
        alert('Будь ласка, завантажте зображення.');
        return;
      }
      const reader = new FileReader();
      reader.onload = (ev) => { img.src = ev.target.result; };
      reader.readAsDataURL(file);
    });

    // Клацання по картинці — робимо невелику анімацію "мурчання" (пульсація)
    img.addEventListener('click', () => {
      img.animate([
        { transform: 'scale(1)' },
        { transform: 'scale(1.05)' },
        { transform: 'scale(1)' }
      ], { duration: 500, easing: 'ease-out' });
    });

    // Повернути оригінал
    resetBtn.addEventListener('click', () => { img.src = defaultSrc; fileInput.value = ''; });

    // Доступність: дозволимо натискати на label для fileInput
    document.querySelector('.file').addEventListener('click', () => { fileInput.click(); });
  </script>
</body>
</html>
