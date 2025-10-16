<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>University Login</title>
  <style>
    :root{
      --bg:#f5f7fb;
      --card:#ffffff;
      --accent:#0b67ff;
      --muted:#6b7280;
      --radius:12px;
      font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      background:linear-gradient(180deg,var(--bg),#eef3ff);
      color:#111827;
      padding:24px;
    }
    .container{
      width:100%;
      max-width:960px;
      display:grid;
      grid-template-columns: 420px 1fr;
      gap:28px;
      align-items:center;
    }
    @media (max-width:880px){
      .container{grid-template-columns:1fr; padding:12px;}
    }
    .card{
      background:var(--card);
      border-radius:var(--radius);
      padding:28px;
      box-shadow: 0 6px 18px rgba(16,24,40,0.06);
    }
    .branding{
      display:flex;
      gap:16px;
      align-items:center;
    }
    .branding img{
      width:72px;
      height:72px;
      object-fit:contain;
      border-radius:8px;
      background:linear-gradient(90deg,#fff,#f3f6ff);
      padding:6px;
      border:1px solid rgba(15,23,42,0.03);
    }
    .branding h1{
      font-size:20px;
      margin:0;
      line-height:1;
    }
    .branding p{ margin:0; color:var(--muted); font-size:13px }
    form{
      margin-top:18px;
      display:flex;
      flex-direction:column;
      gap:12px;
    }
    label{ font-size:13px; color:var(--muted) }
    input[type="text"],
    input[type="password"]{
      padding:12px 14px;
      border-radius:10px;
      border:1px solid #e6e9ef;
      font-size:15px;
      outline:none;
      transition:box-shadow .15s, border-color .15s;
      background:#fbfdff;
    }
    input:focus{
      border-color:var(--accent);
      box-shadow:0 0 0 4px rgba(11,103,255,0.08);
    }
    .row{
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:12px;
    }
    .btn{
      background:var(--accent);
      color:#fff;
      border:none;
      padding:12px 16px;
      border-radius:10px;
      font-weight:600;
      cursor:pointer;
      font-size:15px;
    }
    .btn:disabled{ opacity:.6; cursor:not-allowed}
    .meta{ font-size:13px; color:var(--muted) }
    .illustration{
      display:flex;
      align-items:center;
      justify-content:center;
      gap:18px;
      flex-direction:column;
      text-align:center;
      padding:28px;
    }
    .illustration h2 { margin:0; font-size:20px; }
    .illustration p { margin:0; color:var(--muted) }
    .help{
      margin-top:14px;
      font-size:13px;
      color:var(--muted);
    }
    .error{ color:#b91c1c; font-size:13px; display:none; }
  </style>
</head>
<body>
  <main class="container" role="main" aria-label="Login page">
    <section class="card" aria-labelledby="login-heading">
      <div class="branding" >
        <!-- Replace placeholder-logo.png with your own logo file (ensure you have rights to use it) -->
        <img src="placeholder-logo.png" alt="University logo" id="uni-logo">
        <div>
          <h1 id="login-heading">University Portal</h1>
          <p>Sign in to access your student and faculty resources</p>
        </div>
      </div>

      <form id="login-form" aria-describedby="help-text" novalidate>
        <div>
          <label for="username">Username or email</label>
          <input id="username" name="username" type="text" autocomplete="username" inputmode="email" required />
        </div>

        <div>
          <label for="password">Password</label>
          <input id="password" name="password" type="password" autocomplete="current-password" required minlength="6" />
        </div>

        <div class="row">
          <div style="display:flex;align-items:center;gap:8px">
            <input type="checkbox" id="remember" />
            <label for="remember" class="meta">Remember me</label>
          </div>
          <a href="#" class="meta" id="forgot-link">Forgot password?</a>
        </div>

        <div>
          <button type="submit" class="btn" id="submit-btn">Sign in</button>
        </div>

        <div class="error" id="error-msg" role="alert"></div>

        <div class="help" id="help-text">For security, this demo does not submit credentials. Implement secure server-side authentication and HTTPS for production.</div>
      </form>
    </section>

    <aside class="card illustration" aria-hidden="false">
      <svg width="120" height="120" viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <rect x="10" y="12" width="100" height="76" rx="8" fill="#f3f6ff"/>
        <rect x="20" y="26" width="80" height="8" rx="4" fill="#e6eefc"/>
        <rect x="20" y="40" width="80" height="8" rx="4" fill="#e6eefc"/>
        <rect x="20" y="54" width="52" height="8" rx="4" fill="#e6eefc"/>
        <circle cx="60" cy="96" r="12" fill="#dbe9ff"/>
      </svg>
      <h2>Secure access</h2>
      <p>Authorized users only. Make sure your site uses HTTPS and secure server-side authentication.</p>
    </aside>
  </main>

  <script>
    // Client-side validation demo only. DO NOT use as real auth.
    document.getElementById('login-form').addEventListener('submit', function(e){
      e.preventDefault();
      const user = document.getElementById('username').value.trim();
      const pass = document.getElementById('password').value;

      const err = document.getElementById('error-msg');
      err.style.display = 'none';
      err.textContent = '';

      if (!user){
        err.textContent = 'Please enter your username or email.';
        err.style.display = 'block';
        return;
      }
      if (pass.length < 6){
        err.textContent = 'Password must be at least 6 characters.';
        err.style.display = 'block';
        return;
      }

      // Demo success action: show a friendly message (not sending credentials anywhere)
      alert('Demo only: validation passed. Replace this with secure server-side auth.');
    });

    // Accessibility: focus first input
    document.getElementById('username').focus();
  </script>
</body>
</html>
