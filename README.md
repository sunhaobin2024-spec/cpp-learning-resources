:root {
  --bg: #0b1020;
  --panel: #121a2d;
  --panel-2: #1a243d;
  --text: #e5edf9;
  --muted: #a7b3c9;
  --primary: #6ea8fe;
  --primary-strong: #4d7dff;
  --accent: #7ef0d0;
  --border: rgba(255, 255, 255, 0.08);
}

* {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  font-family: "Segoe UI", Tahoma, sans-serif;
  background: linear-gradient(180deg, #0b1020 0%, #111827 100%);
  color: var(--text);
}

.hero {
  padding: 24px 8% 60px;
  background: radial-gradient(circle at top, rgba(110, 168, 254, 0.15), transparent 35%),
    linear-gradient(180deg, #0d1326 0%, #0b1020 100%);
}

.topbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 10px 0 28px;
}

.brand {
  font-size: 1.25rem;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.nav-links {
  display: flex;
  gap: 22px;
  flex-wrap: wrap;
}

.nav-links a {
  text-decoration: none;
  color: var(--text);
  opacity: 0.85;
}

.hero-content {
  max-width: 1200px;
  margin: 0 auto;
  padding-top: 40px;
}

.eyebrow {
  display: inline-block;
  margin: 0 0 12px;
  letter-spacing: 0.1em;
  font-size: 0.72rem;
  text-transform: uppercase;
  color: var(--accent);
}

h1 {
  margin: 0;
  font-size: clamp(2.2rem, 4vw, 4rem);
  line-height: 1.1;
  max-width: 760px;
}

.subtitle {
  margin-top: 18px;
  max-width: 760px;
  color: var(--muted);
  font-size: 1.05rem;
  line-height: 1.8;
}

.actions {
  display: flex;
  gap: 16px;
  margin-top: 28px;
  flex-wrap: wrap;
}

.actions a {
  display: inline-block;
  padding: 12px 22px;
  border-radius: 999px;
  text-decoration: none;
  transition: 0.2s ease;
}

.primary {
  background: linear-gradient(135deg, var(--primary), var(--primary-strong));
  color: #fff;
}

.secondary {
  border: 1px solid var(--border);
  color: var(--text);
  background: rgba(255, 255, 255, 0.02);
}

.section {
  max-width: 1200px;
  margin: 0 auto;
  padding: 42px 8% 12px;
}

.section-header {
  display: flex;
  align-items: center;
  gap: 14px;
  margin-bottom: 22px;
}

.tag {
  display: inline-flex;
  width: 42px;
  height: 42px;
  border-radius: 12px;
  align-items: center;
  justify-content: center;
  background: rgba(110, 168, 254, 0.12);
  color: var(--primary);
  font-weight: 700;
}

h2 {
  margin: 0;
  font-size: clamp(1.6rem, 2vw, 2.4rem);
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 22px;
}

.card {
  padding: 22px 20px;
  border: 1px solid var(--border);
  background: rgba(255, 255, 255, 0.02);
  border-radius: 18px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
}

.card h3 {
  margin-top: 0;
  margin-bottom: 10px;
  font-size: 1.12rem;
}

.card p {
  margin: 0 0 16px;
  color: var(--muted);
  line-height: 1.7;
}

.card a {
  color: var(--primary);
  text-decoration: none;
  font-weight: 600;
}

.roadmap {
  padding-bottom: 70px;
}

.timeline {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 18px;
}

.timeline li {
  padding: 18px 20px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid var(--border);
  border-radius: 14px;
  color: var(--muted);
  line-height: 1.8;
}

@media (max-width: 640px) {
  .topbar {
    flex-direction: column;
    align-items: flex-start;
    gap: 12px;
  }

  .nav-links {
    gap: 10px 16px;
  }

  .actions {
    flex-direction: column;
    align-items: flex-start;
  }
}
