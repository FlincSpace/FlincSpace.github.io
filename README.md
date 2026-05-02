<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>Workspace</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --accent: #5B50D6; --accent-l: #EEEDFB; --accent-d: #3B31B2;
  --teal: #1D9E75; --teal-l: #E1F5EE;
  --amber: #E8960A; --amber-l: #FEF3D7;
  --red: #E24B4A; --red-l: #FDEAEA;
  --blue: #2B7FD4; --blue-l: #E6F1FB;
  --slate: #64748B;
  --bg: #F1F0EE; --card: #fff; --text: #0F172A; --muted: #64748B;
  --border: rgba(0,0,0,0.08); --r: 14px; --r-sm: 9px;
  --sidebar-w: 230px; --nav-h: 64px; --font: 'Inter', sans-serif;
}
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #0F1117; --card: #1C1F2A; --text: #E8EAF0; --muted: #8892A4;
    --border: rgba(255,255,255,0.08);
    --accent-l: #1E1B3A; --accent-d: #A09DF5;
    --teal-l: #0D2820; --amber-l: #2A1E00; --red-l: #2A0E0E; --blue-l: #0C1E35;
  }
  .li:hover { background: #22263A; }
  .sr:hover { background: #22263A; }
  .cdc:hover { background: var(--accent-l); }
  .md input, .md select, .md textarea { background: #0F1117; }
  .mb.s:hover { background: #2a2d3a; }
  .eli { background: #0F1117; }
  .chat-window { background: #0F1117; }
  .chat-msg-in .chat-bubble { background: #1C1F2A; color: var(--text); }
  .vp-overlay { background: #0A0C12; }
  .vp-content { background: #0F1117; }
}
html, body { height: 100%; font-family: var(--font); background: var(--bg); color: var(--text); overflow: hidden; }

/* ── APP SHELL ── */
.app { display: flex; width: 100%; height: 100dvh; }

/* ── SIDEBAR ── */
.sidebar { width: var(--sidebar-w); background: var(--card); border-right: 1px solid var(--border); display: flex; flex-direction: column; flex-shrink: 0; z-index: 10; }
.sb-brand { padding: 22px 18px 18px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 10px; }
.sb-logo { width: 34px; height: 34px; border-radius: 9px; background: linear-gradient(135deg, #5B50D6, #3B31B2); display: flex; align-items: center; justify-content: center; font-weight: 800; font-size: 14px; color: #fff; flex-shrink: 0; letter-spacing: -0.5px; }
.sb-brand-text .brand-name { font-size: 15px; font-weight: 700; color: var(--text); }
.sb-brand-text .brand-org { font-size: 11px; color: var(--muted); margin-top: 1px; }
.sb-user { padding: 12px 14px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 10px; }
.sb-av { width: 34px; height: 34px; border-radius: 50%; background: linear-gradient(135deg, #5B50D6, #3B31B2); display: flex; align-items: center; justify-content: center; font-weight: 700; font-size: 11px; color: #fff; flex-shrink: 0; }
.sb-av-name { font-size: 13px; font-weight: 600; line-height: 1.2; color: var(--text); }
.sb-av-role { font-size: 11px; color: var(--muted); }
.sb-nav { flex: 1; padding: 10px 8px; display: flex; flex-direction: column; gap: 2px; overflow-y: auto; }
.sb-nav::-webkit-scrollbar { display: none; }
.sni { display: flex; align-items: center; gap: 9px; padding: 9px 11px; border-radius: 10px; cursor: pointer; transition: background 0.12s; color: var(--muted); user-select: none; }
.sni:hover { background: var(--bg); }
.sni.active { background: var(--accent-l); color: var(--accent-d); }
.sni svg { width: 18px; height: 18px; stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; fill: none; flex-shrink: 0; stroke: currentColor; }
.sni-label { font-size: 13px; font-weight: 600; }
.sb-section { font-size: 10px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; color: var(--muted); padding: 10px 11px 4px; }

/* ── MAIN ── */
.main { flex: 1; display: flex; flex-direction: column; overflow: hidden; min-width: 0; }
.main-header { background: var(--card); border-bottom: 1px solid var(--border); padding: 14px 28px; display: flex; align-items: center; justify-content: space-between; flex-shrink: 0; }
.main-title { font-size: 18px; font-weight: 700; }
.main-sub { font-size: 12px; color: var(--muted); margin-top: 1px; }
.mob-av { display: none; width: 34px; height: 34px; border-radius: 50%; background: linear-gradient(135deg,#5B50D6,#3B31B2); align-items: center; justify-content: center; font-weight: 700; font-size: 11px; color: #fff; flex-shrink: 0; }
.main-scroll { flex: 1; overflow-y: auto; overflow-x: hidden; padding: 22px 28px 32px; }
.main-scroll::-webkit-scrollbar { width: 5px; }
.main-scroll::-webkit-scrollbar-thumb { background: #ddd; border-radius: 3px; }

/* ── BOTTOM NAV (mobile) ── */
.nav-bar { display: none; }

/* ── TABS ── */
.tp { display: none; }
.tp.active { display: block; animation: fu 0.2s ease both; }
@keyframes fu { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: none; } }

/* ── SECTION LABEL ── */
.sl { font-size: 11px; font-weight: 700; letter-spacing: 0.06em; text-transform: uppercase; color: var(--muted); margin: 20px 0 10px; }
.sl:first-child { margin-top: 0; }
.sl-row { display: flex; align-items: center; justify-content: space-between; margin: 20px 0 10px; }
.sl-row:first-child { margin-top: 0; }
.sl-row .sl { margin: 0; }
.sl-more { font-size: 12px; font-weight: 600; color: var(--accent); cursor: pointer; }
.sl-more:hover { text-decoration: underline; }

/* ── CARD ── */
.card { background: var(--card); border-radius: var(--r); border: 1px solid var(--border); overflow: hidden; }

/* ── SCROLLABLE LIST ── */
.scroll-list { max-height: 280px; overflow-y: auto; background: var(--card); border-radius: var(--r); border: 1px solid var(--border); }
.scroll-list::-webkit-scrollbar { width: 4px; }
.scroll-list::-webkit-scrollbar-thumb { background: #e0e0e0; border-radius: 2px; }

.li { display: flex; gap: 12px; align-items: flex-start; padding: 12px 16px; border-bottom: 1px solid var(--border); cursor: pointer; transition: background 0.1s; }
.li:last-child { border-bottom: none; }
.li:hover { background: #fafafa; }
.it { font-size: 13px; font-weight: 600; margin-bottom: 2px; color: var(--text); }
.is { font-size: 12px; color: var(--muted); }
.li.read .it { font-weight: 500; color: var(--muted); }
.nd { width: 7px; height: 7px; border-radius: 50%; margin-top: 5px; flex-shrink: 0; }
.dp { background: var(--accent); } .dr { background: #d0d0d0; }

/* ── CHANNELS ── */
.ch-scroll { display: flex; gap: 10px; overflow-x: auto; scrollbar-width: thin; scrollbar-color: #ddd transparent; padding-bottom: 6px; max-height: 160px; flex-wrap: nowrap; }
.ch-scroll::-webkit-scrollbar { height: 4px; }
.ch-scroll::-webkit-scrollbar-thumb { background: #ddd; border-radius: 2px; }
.ch-card { flex: 0 0 94px; border-radius: var(--r); padding: 14px 8px 12px; text-align: center; cursor: pointer; border: 1px solid var(--border); transition: transform 0.15s, box-shadow 0.15s; }
.ch-card:hover { transform: translateY(-3px); box-shadow: 0 8px 20px rgba(0,0,0,0.09); }
.ch-icon { font-size: 22px; margin-bottom: 7px; display: block; }
.ch-name { font-size: 12px; font-weight: 600; }
.ch-card.c0 { background: var(--accent-l); } .ch-card.c0 .ch-name { color: var(--accent-d); }
.ch-card.c1 { background: var(--teal-l); }   .ch-card.c1 .ch-name { color: var(--teal); }
.ch-card.c2 { background: var(--amber-l); }  .ch-card.c2 .ch-name { color: var(--amber); }
.ch-card.c3 { background: var(--blue-l); }   .ch-card.c3 .ch-name { color: var(--blue); }
.ch-card.c4 { background: #F3E8FF; }         .ch-card.c4 .ch-name { color: #7C3AED; }
.ch-card.c5 { background: #FFF0F0; }         .ch-card.c5 .ch-name { color: var(--red); }

/* ── HOME GRID ── */
.home-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
@media (max-width: 900px) { .home-grid { grid-template-columns: 1fr; } }

/* ── HOME LEFT COLUMN INNER GRID ── */
.home-left-bottom { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 20px; }
@media (max-width: 700px) { .home-left-bottom { grid-template-columns: 1fr; } }

/* ── FEATURED VIDEO CARD ── */
.feat-vid-card { background: var(--card); border-radius: var(--r); border: 1px solid var(--border); overflow: hidden; cursor: pointer; transition: transform 0.15s, box-shadow 0.15s; }
.feat-vid-card:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(0,0,0,0.1); }
.feat-vid-thumb { position: relative; aspect-ratio: 16/9; display: flex; align-items: center; justify-content: center; overflow: hidden; }
.feat-vid-play { width: 36px; height: 36px; border-radius: 50%; background: rgba(255,255,255,0.9); display: flex; align-items: center; justify-content: center; font-size: 14px; position: relative; z-index: 1; box-shadow: 0 2px 12px rgba(0,0,0,0.2); }
.feat-vid-dur { position: absolute; bottom: 6px; right: 6px; background: rgba(0,0,0,0.72); color: #fff; font-size: 10px; font-weight: 700; padding: 2px 5px; border-radius: 4px; z-index:1; }
.feat-vid-info { padding: 10px 12px; }
.feat-vid-title { font-size: 12px; font-weight: 600; line-height: 1.3; margin-bottom: 4px; }
.feat-vid-sub { font-size: 11px; color: var(--muted); }

/* ── STATS ROW ── */
.stats-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(120px, 1fr)); gap: 10px; margin-bottom: 20px; }
.stat-card { background: var(--card); border: 1px solid var(--border); border-radius: var(--r); padding: 14px 16px; }
.stat-num { font-size: 22px; font-weight: 800; }
.stat-lbl { font-size: 11px; color: var(--muted); font-weight: 600; margin-top: 2px; }
.stat-card.s0 .stat-num { color: var(--accent); }
.stat-card.s1 .stat-num { color: var(--teal); }
.stat-card.s2 .stat-num { color: var(--amber); }
.stat-card.s3 .stat-num { color: var(--red); }

/* ── CHANNELS TAB GRID ── */
.ch-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(170px, 1fr)); gap: 12px; }
.ch-big { border-radius: var(--r); padding: 20px 18px; cursor: pointer; border: 1px solid var(--border); transition: transform 0.15s, box-shadow 0.15s; }
.ch-big:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(0,0,0,0.09); }
.ch-big-icon { font-size: 30px; margin-bottom: 10px; display: block; }
.ch-big-name { font-size: 15px; font-weight: 700; }
.ch-big-desc { font-size: 12px; margin-top: 3px; }
.ch-big-tag { font-size: 11px; margin-top: 10px; font-weight: 700; padding: 3px 10px; border-radius: 999px; display: inline-block; color: #fff; }
.ch-big.c0 { background: var(--accent-l); } .ch-big.c0 .ch-big-name { color: var(--accent-d); } .ch-big.c0 .ch-big-desc { color: #5B50D6; } .ch-big.c0 .ch-big-tag { background: var(--accent); }
.ch-big.c1 { background: var(--teal-l); }   .ch-big.c1 .ch-big-name { color: #085041; }     .ch-big.c1 .ch-big-desc { color: var(--teal); } .ch-big.c1 .ch-big-tag { background: var(--teal); }
.ch-big.c2 { background: var(--amber-l); }  .ch-big.c2 .ch-big-name { color: #7A4F00; }     .ch-big.c2 .ch-big-desc { color: var(--amber); } .ch-big.c2 .ch-big-tag { background: var(--amber); }
.ch-big.c3 { background: var(--blue-l); }   .ch-big.c3 .ch-big-name { color: #0C447C; }     .ch-big.c3 .ch-big-desc { color: var(--blue); } .ch-big.c3 .ch-big-tag { background: var(--blue); }
.ch-big.c4 { background: #F3E8FF; }         .ch-big.c4 .ch-big-name { color: #5B21B6; }     .ch-big.c4 .ch-big-desc { color: #7C3AED; } .ch-big.c4 .ch-big-tag { background: #7C3AED; }
.ch-big.c5 { background: #FFF0F0; }         .ch-big.c5 .ch-big-name { color: #991B1B; }     .ch-big.c5 .ch-big-desc { color: var(--red); } .ch-big.c5 .ch-big-tag { background: var(--red); }

/* ── CALENDAR ── */
.cal-wrap { display: grid; grid-template-columns: 1fr 300px; gap: 20px; align-items: start; }
@media (max-width: 1000px) { .cal-wrap { grid-template-columns: 1fr; } }
.cal-panel { background: var(--card); border-radius: var(--r); border: 1px solid var(--border); overflow: hidden; }
.chead { padding: 12px 14px; display: flex; align-items: center; gap: 8px; border-bottom: 1px solid var(--border); }
.cmt { font-size: 15px; font-weight: 700; flex: 1; text-align: center; }
.cnb { background: var(--accent-l); border: none; cursor: pointer; width: 28px; height: 28px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 14px; color: var(--accent-d); transition: background 0.12s; flex-shrink: 0; }
.cnb:hover { background: var(--accent); color: #fff; }
.cadd-btn { background: var(--accent); border: none; cursor: pointer; padding: 6px 12px; border-radius: 999px; color: #fff; font-family: var(--font); font-size: 12px; font-weight: 600; transition: background 0.12s; flex-shrink: 0; }
.cadd-btn:hover { background: var(--accent-d); }
.cgw { padding: 10px 12px 8px; }
.wr { display: grid; grid-template-columns: repeat(7,1fr); margin-bottom: 2px; }
.wl { text-align: center; font-size: 10px; font-weight: 700; color: var(--muted); padding: 4px 0; }
.cg { display: grid; grid-template-columns: repeat(7,1fr); gap: 2px; }
.cdc { aspect-ratio: 1; border-radius: 7px; display: flex; flex-direction: column; align-items: center; justify-content: flex-start; padding-top: 5px; cursor: pointer; transition: background 0.12s; }
.cdc:hover { background: var(--accent-l); }
.cdc.om .dn { color: #ccc; }
.cdc.today { background: var(--accent); }
.cdc.today .dn { color: #fff; }
.cdc.sel:not(.today) { background: var(--accent-l); outline: 2px solid var(--accent); outline-offset: -1px; }
.dn { font-size: 12px; font-weight: 600; line-height: 1; }
.eds { display: flex; gap: 2px; margin-top: 2px; justify-content: center; flex-wrap: wrap; max-width: 90%; }
.ed { width: 10px; height: 10px; border-radius: 50%; }
.dred { background: var(--red); } .damb { background: var(--amber); } .dteal { background: var(--teal); } .dacc { background: var(--accent); }
.ev-side { background: var(--card); border-radius: var(--r); border: 1px solid var(--border); }
.ev-side-hd { padding: 12px 14px; border-bottom: 1px solid var(--border); font-size: 13px; font-weight: 700; color: var(--muted); }
.ev-side-body { padding: 10px 12px; max-height: 380px; overflow-y: auto; }
.ev-side-body::-webkit-scrollbar { width: 4px; }
.ev-side-body::-webkit-scrollbar-thumb { background: #e0e0e0; border-radius: 2px; }
.eli { background: var(--bg); border-radius: var(--r-sm); border: 1px solid var(--border); padding: 10px 12px; margin-bottom: 8px; display: flex; align-items: center; gap: 9px; }
.eli:last-child { margin-bottom: 0; }
.ecb { width: 3px; height: 34px; border-radius: 2px; flex-shrink: 0; }
.elt { font-size: 13px; font-weight: 600; }
.els { font-size: 11px; color: var(--muted); margin-top: 2px; }
.ea { margin-left: auto; display: flex; gap: 4px; }
.eb { background: none; border: 1px solid var(--border); border-radius: 6px; cursor: pointer; padding: 4px 7px; font-family: var(--font); font-size: 11px; font-weight: 600; color: var(--muted); transition: all 0.1s; }
.eb:hover { background: var(--accent-l); color: var(--accent-d); border-color: var(--accent); }
.eb.del:hover { background: var(--red-l); color: var(--red); border-color: var(--red); }
.ne { font-size: 13px; color: var(--muted); text-align: center; padding: 20px 0; }

/* ── MESSAGES TAB ── */
.msg-layout { display: grid; grid-template-columns: 280px 1fr; gap: 0; height: calc(100dvh - 64px - 86px); border-radius: var(--r); border: 1px solid var(--border); overflow: hidden; background: var(--card); }
@media (max-width: 700px) { .msg-layout { grid-template-columns: 1fr; height: auto; } }
.msg-list-col { border-right: 1px solid var(--border); display: flex; flex-direction: column; overflow: hidden; }
.msg-list-hd { padding: 14px 16px; border-bottom: 1px solid var(--border); font-size: 13px; font-weight: 700; }
.msg-list-scroll { flex: 1; overflow-y: auto; }
.msg-list-scroll::-webkit-scrollbar { width: 4px; }
.msg-list-scroll::-webkit-scrollbar-thumb { background: #e0e0e0; border-radius: 2px; }
.msg-li { display: flex; gap: 10px; align-items: center; padding: 11px 14px; border-bottom: 1px solid var(--border); cursor: pointer; transition: background 0.1s; }
.msg-li:last-child { border-bottom: none; }
.msg-li:hover { background: var(--bg); }
.msg-li.active { background: var(--accent-l); }
.chat-av { width: 38px; height: 38px; border-radius: 50%; flex-shrink: 0; display: flex; align-items: center; justify-content: center; font-weight: 700; font-size: 12px; color: #fff; }
.chat-info { flex: 1; min-width: 0; }
.chat-name { font-size: 13px; font-weight: 600; color: var(--text); }
.chat-prev { font-size: 12px; color: var(--muted); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.chat-meta { display: flex; flex-direction: column; align-items: flex-end; gap: 4px; flex-shrink: 0; }
.chat-time { font-size: 11px; color: var(--muted); }
.chat-badge { background: var(--accent); color: #fff; font-size: 10px; font-weight: 700; padding: 2px 6px; border-radius: 999px; }
/* Chat window */
.chat-window { flex: 1; display: flex; flex-direction: column; background: var(--bg); }
.chat-win-hd { padding: 12px 16px; border-bottom: 1px solid var(--border); background: var(--card); display: flex; align-items: center; gap: 10px; }
.chat-win-name { font-size: 14px; font-weight: 700; }
.chat-win-status { font-size: 11px; color: var(--teal); font-weight: 600; }
.chat-messages { flex: 1; overflow-y: auto; padding: 16px; display: flex; flex-direction: column; gap: 12px; }
.chat-messages::-webkit-scrollbar { width: 4px; }
.chat-messages::-webkit-scrollbar-thumb { background: #e0e0e0; border-radius: 2px; }
.chat-msg { display: flex; gap: 8px; align-items: flex-end; max-width: 80%; }
.chat-msg-in { align-self: flex-start; }
.chat-msg-out { align-self: flex-end; flex-direction: row-reverse; }
.chat-bubble { padding: 9px 13px; border-radius: 16px; font-size: 13px; line-height: 1.45; }
.chat-msg-in .chat-bubble { background: var(--card); color: var(--text); border-bottom-left-radius: 4px; }
.chat-msg-out .chat-bubble { background: var(--accent); color: #fff; border-bottom-right-radius: 4px; }
.chat-msg-time { font-size: 10px; color: var(--muted); padding: 0 4px; white-space: nowrap; }
.chat-small-av { width: 26px; height: 26px; border-radius: 50%; flex-shrink: 0; display: flex; align-items: center; justify-content: center; font-weight: 700; font-size: 9px; color: #fff; }
.chat-input-row { padding: 12px 14px; border-top: 1px solid var(--border); background: var(--card); display: flex; gap: 10px; align-items: center; }
.chat-input { flex: 1; border: 1px solid var(--border); border-radius: 22px; padding: 9px 14px; font-family: var(--font); font-size: 13px; background: var(--bg); color: var(--text); outline: none; resize: none; }
.chat-input:focus { border-color: var(--accent); }
.chat-send-btn { background: var(--accent); border: none; border-radius: 50%; width: 36px; height: 36px; display: flex; align-items: center; justify-content: center; cursor: pointer; flex-shrink: 0; transition: background 0.12s; color: #fff; font-size: 15px; }
.chat-send-btn:hover { background: var(--accent-d); }
.chat-empty { flex: 1; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 8px; color: var(--muted); font-size: 14px; }

/* ── VIDEOS ── */
.vid-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 14px; }
.vid-card { background: var(--card); border-radius: var(--r); border: 1px solid var(--border); overflow: hidden; cursor: pointer; transition: transform 0.15s, box-shadow 0.15s; }
.vid-card:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(0,0,0,0.1); }
.vid-thumb { position: relative; aspect-ratio: 16/9; overflow: hidden; display: flex; align-items: center; justify-content: center; }
.vid-thumb-bg { position: absolute; inset: 0; }
.vid-play { width: 42px; height: 42px; border-radius: 50%; background: rgba(255,255,255,0.9); display: flex; align-items: center; justify-content: center; font-size: 16px; position: relative; z-index: 1; box-shadow: 0 2px 12px rgba(0,0,0,0.2); transition: transform 0.12s; }
.vid-card:hover .vid-play { transform: scale(1.1); }
.vid-duration { position: absolute; bottom: 8px; right: 8px; background: rgba(0,0,0,0.7); color: #fff; font-size: 10px; font-weight: 700; padding: 2px 6px; border-radius: 4px; z-index: 1; }
.vid-info { padding: 12px 14px; }
.vid-title { font-size: 13px; font-weight: 600; line-height: 1.3; margin-bottom: 6px; }
.vid-meta { display: flex; align-items: center; justify-content: space-between; }
.vid-author { display: flex; align-items: center; gap: 6px; }
.vid-author-av { width: 20px; height: 20px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 8px; font-weight: 700; color: #fff; }
.vid-author-name { font-size: 11px; color: var(--muted); font-weight: 500; }
.vid-views { font-size: 11px; color: var(--muted); }
.vid-tag { font-size: 10px; font-weight: 700; padding: 2px 8px; border-radius: 999px; margin-top: 8px; display: inline-block; }

/* ── VIDEO PLAYER OVERLAY ── */
.vp-overlay { position: fixed; inset: 0; z-index: 300; background: #0A0C12; display: none; flex-direction: column; overflow: hidden; animation: vpIn 0.22s ease; }
.vp-overlay.open { display: flex; }
@keyframes vpIn { from { opacity: 0; transform: scale(0.98); } to { opacity: 1; transform: none; } }
.vp-header { display: flex; align-items: center; gap: 12px; padding: 14px 20px; background: rgba(0,0,0,0.4); flex-shrink: 0; border-bottom: 1px solid rgba(255,255,255,0.08); }
.vp-close { background: rgba(255,255,255,0.12); border: none; color: #fff; border-radius: 50%; width: 34px; height: 34px; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 18px; transition: background 0.12s; flex-shrink: 0; }
.vp-close:hover { background: rgba(255,255,255,0.22); }
.vp-hd-title { font-size: 15px; font-weight: 700; color: #fff; flex: 1; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.vp-hd-tag { font-size: 11px; font-weight: 700; padding: 3px 10px; border-radius: 999px; color: #fff; flex-shrink: 0; }
.vp-body { flex: 1; overflow-y: auto; }
.vp-body::-webkit-scrollbar { width: 5px; }
.vp-body::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.15); border-radius: 3px; }
.vp-player { width: 100%; aspect-ratio: 16/9; max-height: 55vh; position: relative; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.vp-player-bg { position: absolute; inset: 0; }
.vp-player-btn { width: 64px; height: 64px; border-radius: 50%; background: rgba(255,255,255,0.15); border: 2px solid rgba(255,255,255,0.4); display: flex; align-items: center; justify-content: center; font-size: 26px; color: #fff; position: relative; z-index: 1; cursor: pointer; transition: background 0.15s; }
.vp-player-btn:hover { background: rgba(255,255,255,0.25); }
.vp-player-dur { position: absolute; bottom: 12px; right: 14px; background: rgba(0,0,0,0.7); color: #fff; font-size: 11px; font-weight: 700; padding: 3px 8px; border-radius: 5px; z-index: 1; }
.vp-content { background: var(--bg); padding: 24px; }
.vp-meta-row { display: flex; align-items: center; gap: 10px; margin-bottom: 20px; }
.vp-av { width: 36px; height: 36px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: 700; font-size: 11px; color: #fff; flex-shrink: 0; }
.vp-author { font-size: 13px; font-weight: 600; color: var(--text); }
.vp-views { font-size: 12px; color: var(--muted); margin-left: auto; }
.vp-section { font-size: 14px; font-weight: 700; margin-bottom: 12px; color: var(--text); }
/* Questions */
.vp-questions { display: flex; flex-direction: column; gap: 10px; margin-bottom: 28px; }
.vp-q { background: var(--card); border: 1px solid var(--border); border-radius: var(--r); padding: 16px; cursor: pointer; }
.vp-q-text { font-size: 13px; font-weight: 600; color: var(--text); margin-bottom: 0; display: flex; align-items: center; justify-content: space-between; gap: 10px; }
.vp-q-text::after { content: '›'; font-size: 16px; color: var(--muted); flex-shrink: 0; transition: transform 0.2s; }
.vp-q.open .vp-q-text::after { transform: rotate(90deg); }
.vp-q-answer { font-size: 13px; color: var(--muted); margin-top: 10px; line-height: 1.6; display: none; }
.vp-q.open .vp-q-answer { display: block; }
/* Exercises */
.vp-exercises { display: flex; flex-direction: column; gap: 12px; }
.vp-ex { background: var(--card); border: 1px solid var(--border); border-radius: var(--r); padding: 16px; }
.vp-ex-label { font-size: 10px; font-weight: 700; letter-spacing: 0.06em; text-transform: uppercase; color: var(--accent); margin-bottom: 6px; }
.vp-ex-text { font-size: 13px; font-weight: 600; color: var(--text); margin-bottom: 10px; line-height: 1.4; }
.vp-ex-opts { display: flex; flex-direction: column; gap: 6px; }
.vp-opt { background: var(--bg); border: 1px solid var(--border); border-radius: 8px; padding: 9px 12px; font-size: 13px; cursor: pointer; transition: all 0.12s; color: var(--text); }
.vp-opt:hover { border-color: var(--accent); background: var(--accent-l); }
.vp-opt.correct { background: var(--teal-l); border-color: var(--teal); color: var(--teal); font-weight: 600; }
.vp-opt.wrong { background: var(--red-l); border-color: var(--red); color: var(--red); }
.vp-ex-input { width: 100%; border: 1px solid var(--border); border-radius: 8px; padding: 9px 12px; font-family: var(--font); font-size: 13px; background: var(--bg); color: var(--text); outline: none; margin-bottom: 8px; }
.vp-ex-input:focus { border-color: var(--accent); }
.vp-ex-submit { background: var(--accent); color: #fff; border: none; border-radius: 8px; padding: 8px 16px; font-family: var(--font); font-size: 13px; font-weight: 600; cursor: pointer; transition: background 0.12s; }
.vp-ex-submit:hover { background: var(--accent-d); }
.vp-ex-feedback { font-size: 12px; margin-top: 6px; font-weight: 600; }

/* ── PROFILE ── */
.profil-wrap { display: grid; grid-template-columns: 260px 1fr; gap: 20px; align-items: start; }
@media (max-width: 800px) { .profil-wrap { grid-template-columns: 1fr; } }
.profile-card { background: var(--card); border-radius: var(--r); border: 1px solid var(--border); padding: 24px 18px; display: flex; flex-direction: column; align-items: center; gap: 6px; text-align: center; }
.profile-av { width: 68px; height: 68px; border-radius: 50%; background: linear-gradient(135deg,#5B50D6,#3B31B2); display: flex; align-items: center; justify-content: center; font-weight: 700; font-size: 22px; color: #fff; margin-bottom: 4px; }
.profile-name { font-size: 18px; font-weight: 700; }
.profile-role { font-size: 12px; color: var(--muted); }
.profile-stats { display: grid; grid-template-columns: repeat(3,1fr); gap: 1px; background: var(--border); border: 1px solid var(--border); border-radius: var(--r); margin-top: 14px; width: 100%; overflow: hidden; }
.psc { background: var(--card); padding: 12px 6px; text-align: center; }
.psn { font-size: 20px; font-weight: 700; color: var(--accent); }
.psl { font-size: 10px; color: var(--muted); font-weight: 600; margin-top: 2px; }
.sr { display: flex; align-items: center; justify-content: space-between; padding: 13px 16px; border-bottom: 1px solid var(--border); cursor: pointer; transition: background 0.1s; }
.sr:hover { background: #fafafa; }
.sr:last-child { border-bottom: none; }
.srl { font-size: 13px; font-weight: 600; }

/* ── MODAL ── */
.mo { position: fixed; inset: 0; z-index: 200; background: rgba(0,0,0,0.3); display: none; align-items: center; justify-content: center; padding: 20px; }
.mo.open { display: flex; }
.md { background: var(--card); border-radius: 18px; padding: 22px; width: 100%; max-width: 380px; box-shadow: 0 20px 60px rgba(0,0,0,0.18); animation: pi 0.17s ease; }
@keyframes pi { from { transform: scale(0.96); opacity: 0; } to { transform: scale(1); opacity: 1; } }
.md h3 { font-size: 16px; font-weight: 700; margin-bottom: 14px; }
.md label { font-size: 11px; font-weight: 700; color: var(--muted); display: block; margin-bottom: 4px; margin-top: 12px; }
.md input, .md select, .md textarea { width: 100%; border: 1px solid var(--border); border-radius: 9px; padding: 9px 12px; font-family: var(--font); font-size: 13px; background: var(--bg); color: var(--text); outline: none; }
.md textarea { resize: vertical; min-height: 70px; }
.md input:focus, .md select:focus, .md textarea:focus { border-color: var(--accent); }
.mbs { display: flex; gap: 8px; margin-top: 18px; }
.mb { flex: 1; border: none; border-radius: 10px; padding: 11px; font-family: var(--font); font-size: 13px; font-weight: 600; cursor: pointer; transition: background 0.12s; }
.mb.p { background: var(--accent); color: #fff; } .mb.p:hover { background: var(--accent-d); }
.mb.s { background: var(--bg); color: var(--muted); } .mb.s:hover { background: #e4e2de; }

/* ── RESPONSIVE ── */
@media (max-width: 640px) {
  .app { flex-direction: column; }
  .sidebar { display: none; }
  .main-scroll { padding: 14px 14px calc(var(--nav-h) + 14px); }
  .main-header { padding: 12px 16px; }
  .main-title { font-size: 16px; }
  .mob-av { display: flex !important; }
  .vid-grid { grid-template-columns: 1fr 1fr; }
  .nav-bar {
    display: flex; position: fixed; bottom: 0; left: 0; right: 0;
    height: var(--nav-h); background: var(--card); border-top: 1px solid var(--border);
    justify-content: space-around; align-items: center;
    padding: 0 4px env(safe-area-inset-bottom); z-index: 100;
  }
  .ni { display: flex; flex-direction: column; align-items: center; gap: 3px; padding: 7px 8px; border-radius: 10px; cursor: pointer; transition: background 0.12s; flex: 1; }
  .ni:hover, .ni.active { background: var(--accent-l); }
  .ni svg { width: 20px; height: 20px; stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; fill: none; }
  .ni.active svg { stroke: var(--accent-d); }
  .ni:not(.active) svg { stroke: var(--muted); }
  .nl { font-size: 9px; font-weight: 700; }
  .ni.active .nl { color: var(--accent-d); }
  .ni:not(.active) .nl { color: var(--muted); }
  .msg-layout { grid-template-columns: 1fr; height: auto; }
  .msg-list-col { max-height: 300px; border-right: none; border-bottom: 1px solid var(--border); }
}
@media (max-width: 480px) { .vid-grid { grid-template-columns: 1fr; } }
@media (max-width: 900px) and (orientation: landscape) and (max-height: 500px) {
  :root { --sidebar-w: 180px; }
  .sb-brand { padding: 12px 14px; }
  .sb-nav { padding: 6px 6px; }
  .sni { padding: 7px 9px; }
  .main-scroll { padding: 14px 18px 20px; }
}
</style>
</head>
<body>
<div class="app">

  <!-- ── SIDEBAR ── -->
  <aside class="sidebar">
    <div class="sb-brand">
      <div class="sb-logo">W</div>
      <div class="sb-brand-text">
        <div class="brand-name">Workspace</div>
        <div class="brand-org">Acme Corp</div>
      </div>
    </div>
    <div class="sb-user">
      <div class="sb-av">N</div>
      <div>
        <div class="sb-av-name">Nutzer</div>
        <div class="sb-av-role">Product Manager</div>
      </div>
    </div>
    <nav class="sb-nav">
      <div class="sb-section">Main</div>
      <div class="sni active" data-tab="home">
        <svg viewBox="0 0 24 24"><path d="M3 9.5L12 3l9 6.5V20a1 1 0 01-1 1H4a1 1 0 01-1-1V9.5z"/><path d="M9 21V12h6v9"/></svg>
        <span class="sni-label">Dashboard</span>
      </div>
      <div class="sni" data-tab="channels">
        <svg viewBox="0 0 24 24"><path d="M4 19.5A2.5 2.5 0 016.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 014 19.5v-15A2.5 2.5 0 016.5 2z"/></svg>
        <span class="sni-label">Channels</span>
      </div>
      <div class="sni" data-tab="kalender">
        <svg viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="3" y1="9" x2="21" y2="9"/><line x1="9" y1="4" x2="9" y2="9"/><line x1="15" y1="4" x2="15" y2="9"/></svg>
        <span class="sni-label">Calendar</span>
      </div>
      <div class="sni" data-tab="videos">
        <svg viewBox="0 0 24 24"><polygon points="23 7 16 12 23 17 23 7"/><rect x="1" y="5" width="15" height="14" rx="2"/></svg>
        <span class="sni-label">Videos</span>
      </div>
      <div class="sb-section">Communication</div>
      <div class="sni" data-tab="messages">
        <svg viewBox="0 0 24 24"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
        <span class="sni-label">Messages</span>
      </div>
      <div class="sb-section">Account</div>
      <div class="sni" data-tab="profil">
        <svg viewBox="0 0 24 24"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg>
        <span class="sni-label">Profile</span>
      </div>
    </nav>
  </aside>

  <!-- ── MAIN ── -->
  <div class="main">
    <div class="main-header">
      <div>
        <div class="main-title" id="page-title">Dashboard</div>
        <div class="main-sub" id="page-sub">Good morning, Alex 👋</div>
      </div>
      <div class="mob-av" style="display:none">AJ</div>
    </div>
    <div class="main-scroll" id="main-scroll">

      <!-- DASHBOARD -->
      <div class="tp active" id="tab-home">
        <div class="stats-row" id="home-stats"></div>
        <div class="home-grid">
          <!-- LEFT COLUMN -->
          <div>
            <div class="sl-row"><span class="sl">Channels</span><span class="sl-more" onclick="switchTab('channels')">View all</span></div>
            <div class="ch-scroll" id="home-channels"></div>
            <!-- Featured Video + Notifications row -->
            <div class="home-left-bottom">
              <div>
                <div class="sl-row" style="margin-top:0"><span class="sl">Featured Video</span></div>
                <div id="home-featured-video"></div>
              </div>
              <div>
                <div class="sl-row" style="margin-top:0"><span class="sl">Notifications</span></div>
                <div class="scroll-list" id="home-notifications"></div>
              </div>
            </div>
          </div>
          <!-- RIGHT COLUMN -->
          <div>
            <div class="sl-row"><span class="sl">Upcoming</span><span class="sl-more" onclick="switchTab('kalender')">Calendar</span></div>
            <div id="home-upcoming" class="scroll-list"></div>
            <div class="sl" style="margin-top:20px">Quick Access</div>
            <div class="card" id="home-quickaccess"></div>
          </div>
        </div>
      </div>

      <!-- CHANNELS -->
      <div class="tp" id="tab-channels">
        <div class="sl" style="margin-top:0">Your Channels</div>
        <div class="ch-grid" id="channels-grid"></div>
      </div>

      <!-- CALENDAR -->
      <div class="tp" id="tab-kalender">
        <div class="cal-wrap">
          <div>
            <div class="cal-panel">
              <div class="chead">
                <button class="cnb" id="cp">‹</button>
                <span class="cmt" id="ct"></span>
                <button class="cnb" id="cn">›</button>
                <button class="cadd-btn" id="cadd">＋ Event</button>
              </div>
              <div class="cgw">
                <div class="wr"><div class="wl">Mon</div><div class="wl">Tue</div><div class="wl">Wed</div><div class="wl">Thu</div><div class="wl">Fri</div><div class="wl">Sat</div><div class="wl">Sun</div></div>
                <div class="cg" id="cg"></div>
              </div>
            </div>
          </div>
          <div class="ev-side">
            <div class="ev-side-hd" id="csl">Select a day</div>
            <div class="ev-side-body" id="cel"></div>
          </div>
        </div>
      </div>

      <!-- VIDEOS -->
      <div class="tp" id="tab-videos">
        <div class="sl-row" style="margin-top:0"><span class="sl">Featured</span></div>
        <div class="vid-grid" id="vid-grid"></div>
      </div>

      <!-- MESSAGES -->
      <div class="tp" id="tab-messages">
        <div class="msg-layout">
          <div class="msg-list-col">
            <div class="msg-list-hd">Messages</div>
            <div class="msg-list-scroll" id="msg-list"></div>
          </div>
          <div class="chat-window" id="chat-window">
            <div class="chat-empty">
              <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
              <span>Select a conversation</span>
            </div>
          </div>
        </div>
      </div>

      <!-- PROFILE -->
      <div class="tp" id="tab-profil">
        <div class="profil-wrap">
          <div>
            <div class="profile-card">
              <div class="profile-av">AJ</div>
              <div class="profile-name">Alex Johnson</div>
              <div class="profile-role">Product Manager · Acme Corp</div>
              <div class="profile-stats">
                <div class="psc"><div class="psn" id="prof-ch-count">0</div><div class="psl">Channels</div></div>
                <div class="psc"><div class="psn">3</div><div class="psl">Tasks</div></div>
                <div class="psc"><div class="psn">12</div><div class="psl">Meetings</div></div>
              </div>
            </div>
          </div>
          <div>
            <div class="sl" style="margin-top:0">Settings</div>
            <div class="card">
              <div class="sr"><span class="srl">👤 Edit Profile</span><span style="color:var(--muted)">›</span></div>
              <div class="sr"><span class="srl">🔔 Notifications</span><span style="color:var(--muted)">›</span></div>
              <div class="sr"><span class="srl">🌐 Language & Region</span><span style="color:var(--muted)">›</span></div>
              <div class="sr"><span class="srl">🔒 Privacy & Security</span><span style="color:var(--muted)">›</span></div>
              <div class="sr"><span class="srl">🎨 Appearance</span><span style="color:var(--muted)">›</span></div>
              <div class="sr"><span class="srl" style="color:var(--red)">🚪 Sign Out</span><span style="color:var(--muted)">›</span></div>
            </div>
          </div>
        </div>
      </div>

    </div><!-- /main-scroll -->
  </div><!-- /main -->

  <!-- BOTTOM NAV (mobile) -->
  <nav class="nav-bar">
    <div class="ni active" data-tab="home"><svg viewBox="0 0 24 24" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" fill="none"><path d="M3 9.5L12 3l9 6.5V20a1 1 0 01-1 1H4a1 1 0 01-1-1V9.5z"/><path d="M9 21V12h6v9"/></svg><span class="nl">Home</span></div>
    <div class="ni" data-tab="channels"><svg viewBox="0 0 24 24" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" fill="none"><path d="M4 19.5A2.5 2.5 0 016.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 014 19.5v-15A2.5 2.5 0 016.5 2z"/></svg><span class="nl">Channels</span></div>
    <div class="ni" data-tab="videos"><svg viewBox="0 0 24 24" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" fill="none"><polygon points="23 7 16 12 23 17 23 7"/><rect x="1" y="5" width="15" height="14" rx="2"/></svg><span class="nl">Videos</span></div>
    <div class="ni" data-tab="messages"><svg viewBox="0 0 24 24" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" fill="none"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg><span class="nl">Messages</span></div>
    <div class="ni" data-tab="profil"><svg viewBox="0 0 24 24" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" fill="none"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg><span class="nl">Profile</span></div>
  </nav>
</div>

<!-- CALENDAR MODAL -->
<div class="mo" id="modal">
  <div class="md">
    <h3 id="mh">Add Event</h3>
    <label>Title</label><input type="text" id="et" placeholder="e.g. Q3 Strategy Review">
    <label>Date</label><input type="date" id="ed">
    <label>Details</label><input type="text" id="ede" placeholder="e.g. 10:00 – 11:00, Room 3B">
    <label>Category</label>
    <select id="ety">
      <option value="red">Deadline / Review</option>
      <option value="amber">Meeting / Workshop</option>
      <option value="teal">Event / Social</option>
      <option value="purple">Other</option>
    </select>
    <div class="mbs">
      <button class="mb s" id="mcancel">Cancel</button>
      <button class="mb p" id="msave">Save</button>
    </div>
  </div>
</div>

<!-- VIDEO PLAYER OVERLAY -->
<div class="vp-overlay" id="vp-overlay">
  <div class="vp-header">
    <button class="vp-close" onclick="closePlayer()">✕</button>
    <div class="vp-hd-title" id="vp-title"></div>
    <div class="vp-hd-tag" id="vp-tag"></div>
  </div>
  <div class="vp-body">
    <div class="vp-player">
      <div class="vp-player-bg" id="vp-bg"></div>
      <div class="vp-player-btn" id="vp-play-btn">▶</div>
      <div class="vp-player-dur" id="vp-dur"></div>
    </div>
    <div class="vp-content">
      <div class="vp-meta-row">
        <div class="vp-av" id="vp-av"></div>
        <div>
          <div class="vp-author" id="vp-author"></div>
          <div style="font-size:11px;color:var(--muted)" id="vp-views-el"></div>
        </div>
        <div class="vp-views" id="vp-views"></div>
      </div>
      <div class="vp-section">Discussion Questions</div>
      <div class="vp-questions" id="vp-questions"></div>
      <div class="vp-section">Exercises</div>
      <div class="vp-exercises" id="vp-exercises"></div>
    </div>
  </div>
</div>

<script>
// ════════════════════════════════════════════════════════
// ── EDIT YOUR DATA HERE — changes apply everywhere ──
// ════════════════════════════════════════════════════════

const CHANNELS = [
  // showOnDashboard: false hides the channel from the dashboard strip,
  // but it still appears in the full Channels tab
  { icon:'📊', name:'Strategy',    desc:'Leadership · 12 members',     tag:'Mon, 10:00',    color:0, showOnDashboard:true  },
  { icon:'🛠️', name:'Engineering', desc:'Dev team · 24 members',        tag:'Tue, 2nd hour', color:1, showOnDashboard:true  },
  { icon:'🎨', name:'Design',      desc:'UX & Visual · 8 members',      tag:'Wed, 1st hour', color:2, showOnDashboard:true  },
  { icon:'📣', name:'Marketing',   desc:'Growth team · 10 members',     tag:'Thu, 3rd hour', color:3, showOnDashboard:false },
  { icon:'💼', name:'HR',          desc:'People ops · 5 members',       tag:'Fri, 5th hour', color:4, showOnDashboard:false },
  { icon:'⚙️', name:'Operations',  desc:'Infra & Logistics · 7 members',tag:'Fri, 2nd hour', color:5, showOnDashboard:true  },
];

const NOTIFICATIONS = [
  { text:'Q3 Strategy deck shared',     sub:'Sarah Chen — Strategy · 30m ago',  read:false },
  { text:'PR #142 needs your review',   sub:'Dev team — Engineering · 1h ago',  read:false },
  { text:'Design system v2.0 launched', sub:'Mia Rossi — Design · 2h ago',      read:false },
  { text:'New onboarding video posted', sub:'HR Team — Videos · 3h ago',        read:false },
  { text:'All-hands recap available',   sub:'Leadership — Videos · Yesterday',  read:true  },
  { text:'Budget report updated',       sub:'Finance — Operations · Yesterday', read:true  },
];

const QUICK_ACCESS = [
  { icon:'📋', label:'Task Board',   sub:'3 tasks due this week', tab:'home'    },
  { icon:'📂', label:'Documents',    sub:'Last edited: Q3 Review',tab:'home'    },
  { icon:'🎥', label:'Latest Video', sub:'Product Roadmap 2025',  tab:'videos'  },
];

const STATS = [
  { num: () => CHANNELS.length, label:'Channels',    cls:'s0' },
  { num: 3,                      label:'Open Tasks',  cls:'s1' },
  { num: 2,                      label:'Events Today',cls:'s2' },
  { num: 7,                      label:'Unread Msgs', cls:'s3' },
];

// Each video can have questions (accordion) and exercises (MCQ or open-ended)
// Exercise types: 'mcq' (multiple choice) or 'open' (free text)
const VIDEOS = [
  {
    id:1, title:'Product Roadmap 2025 — All Hands Recap',
    author:'Sarah Chen', authorInitials:'SC', authorColor:'#5B50D6',
    duration:'18:34', views:'142 views', tag:'Leadership', tagBg:'#5B50D6',
    thumbGrad:['#667eea','#764ba2'],
    questions:[
      { q:'What are the three main pillars of the 2025 product strategy?', a:'The three pillars are: (1) Platform reliability and scale, (2) User experience simplification, and (3) Expanding into enterprise markets with new integrations.' },
      { q:'How does the roadmap address customer feedback from Q2?', a:'The roadmap directly responds to Q2 feedback by prioritising faster onboarding flows, improved notification controls, and better data export capabilities.' },
    ],
    exercises:[
      { type:'mcq', text:'Which quarter is the enterprise feature launch targeted for?', opts:['Q1','Q2','Q3','Q4'], correct:2 },
      { type:'open', text:'In your own words, summarise the key takeaway from this all-hands for your team.' },
    ],
  },
  {
    id:2, title:'Engineering Onboarding: Dev Environment Setup',
    author:'Tom Hartley', authorInitials:'TH', authorColor:'#1D9E75',
    duration:'24:10', views:'89 views', tag:'Engineering', tagBg:'#1D9E75',
    thumbGrad:['#11998e','#38ef7d'],
    questions:[
      { q:'What tools are required before starting the dev environment setup?', a:'You need Docker Desktop, Node.js v20+, Git configured with SSH keys, and access to the internal NPM registry.' },
      { q:'What should you do if the initial seed script fails?', a:'Check that your database container is running with `docker ps`, ensure the .env file is copied from .env.example, and retry the seed script with verbose logging enabled.' },
    ],
    exercises:[
      { type:'mcq', text:'Which Node.js version is required for the dev environment?', opts:['v16','v18','v20','v22'], correct:2 },
      { type:'open', text:'Describe one step from the setup process you found unclear, and how you resolved it.' },
    ],
  },
  {
    id:3, title:'Design System v2.0 — What\'s New',
    author:'Mia Rossi', authorInitials:'MR', authorColor:'#E8960A',
    duration:'12:05', views:'204 views', tag:'Design', tagBg:'#E8960A',
    thumbGrad:['#f7971e','#ffd200'],
    questions:[
      { q:'What is the biggest breaking change in v2.0?', a:'The token naming convention has changed from legacy BEM-style names to a semantic scale (e.g. `color-text-primary` instead of `color-grey-900`). All components need to be updated.' },
      { q:'How do you migrate existing components to v2.0?', a:'Run the codemod script `npx ds-migrate@latest`, review the diff, then update any custom overrides manually. The migration guide covers edge cases.' },
    ],
    exercises:[
      { type:'mcq', text:'What does the new semantic token `color-surface-raised` replace?', opts:['color-white','color-grey-50','color-bg-card','color-neutral-100'], correct:2 },
      { type:'open', text:'List two components in your current project that will need updating for v2.0 compatibility.' },
    ],
  },
  {
    id:4, title:'Q3 Marketing Strategy Deep Dive',
    author:'Laura Kim', authorInitials:'LK', authorColor:'#2B7FD4',
    duration:'31:47', views:'67 views', tag:'Marketing', tagBg:'#2B7FD4',
    thumbGrad:['#2193b0','#6dd5ed'],
    questions:[
      { q:'What is the primary target audience for Q3 campaigns?', a:'Mid-market SaaS companies with 50–500 employees, particularly those currently using legacy project management tools looking to consolidate their stack.' },
      { q:'Which channels are being prioritised, and why?', a:'LinkedIn and industry newsletters are prioritised due to highest conversion rates in Q2. Paid search is being scaled back due to rising CPCs in the segment.' },
    ],
    exercises:[
      { type:'mcq', text:'What was the Q2 conversion rate benchmark the Q3 strategy aims to beat?', opts:['1.2%','2.4%','3.1%','4.5%'], correct:1 },
      { type:'open', text:'Suggest one new channel or tactic not mentioned in the video that could support the Q3 goals.' },
    ],
  },
  {
    id:5, title:'HR: Benefits & Enrollment Guide 2025',
    author:'HR Team', authorInitials:'HR', authorColor:'#7C3AED',
    duration:'9:22', views:'312 views', tag:'HR', tagBg:'#7C3AED',
    thumbGrad:['#8E2DE2','#4A00E0'],
    questions:[
      { q:'What is the deadline for benefits enrollment this year?', a:'The enrollment window closes on the last Friday of October. Late submissions cannot be accepted, so employees should complete their selections at least 48 hours before the deadline.' },
      { q:'What happens if you miss the enrollment window?', a:'You will automatically roll over to your current plan selections. Changes can only be made during the next open enrollment period or following a qualifying life event.' },
    ],
    exercises:[
      { type:'mcq', text:'Which plan tier includes dental and vision at no additional cost?', opts:['Basic','Standard','Premium','Executive'], correct:2 },
      { type:'open', text:'What questions do you still have about your benefits options after watching this video?' },
    ],
  },
  {
    id:6, title:'Operations: Infrastructure Runbook',
    author:'James Wright', authorInitials:'JW', authorColor:'#E24B4A',
    duration:'41:03', views:'44 views', tag:'Operations', tagBg:'#E24B4A',
    thumbGrad:['#e52d27','#b31217'],
    questions:[
      { q:'What is the first step when responding to a P1 incident?', a:'Immediately post in #incidents Slack channel, page the on-call engineer, and start a war room video call. Do not wait for root cause before escalating — speed of communication is critical.' },
      { q:'How often are infrastructure runbooks reviewed and updated?', a:'Runbooks are reviewed quarterly by the platform team lead and after every P1 or P2 incident. All engineers are expected to flag outdated steps via a pull request.' },
    ],
    exercises:[
      { type:'mcq', text:'What is the maximum time before a P1 incident requires executive notification?', opts:['15 minutes','30 minutes','1 hour','2 hours'], correct:1 },
      { type:'open', text:'Describe a scenario where the runbook process might break down and how you would handle it.' },
    ],
  },
];

// Direct messages data
// Each conversation has an id, name, initials, avatarColor, time, unread count,
// a preview line, and a messages array.
// message role: 'in' = them, 'out' = you
const DIRECT_MESSAGES = [
  {
    id:1, name:'Sarah Chen', initials:'SC', avatarColor:'#5B50D6',
    time:'10:12', unread:3, preview:'Can you review the Q3 deck before EOD?',
    messages:[
      { role:'in',  text:'Hey! Do you have a moment to review the Q3 deck?', time:'09:50' },
      { role:'out', text:'Sure, send it over!', time:'09:52' },
      { role:'in',  text:'Just shared it in the Strategy channel. It\'s the latest version with the exec feedback incorporated.', time:'09:54' },
      { role:'in',  text:'Can you review the Q3 deck before EOD?', time:'10:12' },
    ],
  },
  {
    id:2, name:'Mia Rossi', initials:'MR', avatarColor:'#1D9E75',
    time:'09:45', unread:1, preview:'Design system v2 is live!',
    messages:[
      { role:'in',  text:'Design system v2 is live! 🎉', time:'09:45' },
      { role:'in',  text:'Check out the new token docs in the wiki.', time:'09:46' },
    ],
  },
  {
    id:3, name:'Engineering Team', initials:'ENG', avatarColor:'#2B7FD4',
    time:'08:30', unread:4, preview:'Tom: PR #142 is ready for review',
    messages:[
      { role:'in',  text:'PR #142 is up — added the new caching layer we discussed.', time:'08:15' },
      { role:'in',  text:'Tom: PR #142 is ready for review', time:'08:30' },
      { role:'out', text:'On it, will take a look this morning.', time:'08:35' },
    ],
  },
  {
    id:4, name:'HR — All Staff', initials:'HR', avatarColor:'#E8960A',
    time:'Yesterday', unread:2, preview:'Reminder: benefits enrollment closes Friday',
    messages:[
      { role:'in',  text:'Reminder: benefits enrollment closes this Friday at 5pm.', time:'Yesterday' },
      { role:'in',  text:'If you have questions, drop by the HR office or reply here.', time:'Yesterday' },
    ],
  },
  {
    id:5, name:'James Wright', initials:'JW', avatarColor:'#7C3AED',
    time:'Yesterday', unread:0, preview:'Thanks for the feedback!',
    messages:[
      { role:'out', text:'Great work on the runbook, James. Really thorough.', time:'Mon' },
      { role:'in',  text:'Thanks for the feedback!', time:'Yesterday' },
    ],
  },
  {
    id:6, name:'Operations', initials:'OPS', avatarColor:'#E24B4A',
    time:'Mon', unread:0, preview:'Server maintenance scheduled for Sunday',
    messages:[
      { role:'in', text:'Server maintenance scheduled for Sunday 02:00–04:00 UTC.', time:'Mon' },
    ],
  },
  {
    id:7, name:'Laura Kim', initials:'LK', avatarColor:'#085041',
    time:'Mon', unread:0, preview:'Budget approved — let\'s proceed!',
    messages:[
      { role:'out', text:'Any update on the Q3 budget approval?', time:'Mon' },
      { role:'in',  text:'Budget approved — let\'s proceed!', time:'Mon' },
    ],
  },
];

// ════════════════════════════════════════════════════════
// ── RENDERERS ──
// ════════════════════════════════════════════════════════

function renderStats() {
  document.getElementById('home-stats').innerHTML = STATS.map(s =>
    `<div class="stat-card ${s.cls}"><div class="stat-num">${typeof s.num === 'function' ? s.num() : s.num}</div><div class="stat-lbl">${s.label}</div></div>`
  ).join('');
}

function renderHomeChannels() {
  const visible = CHANNELS.filter(ch => ch.showOnDashboard);
  document.getElementById('home-channels').innerHTML = visible.map(ch =>
    `<div class="ch-card c${ch.color}" onclick="switchTab('channels')"><span class="ch-icon">${ch.icon}</span><span class="ch-name">${ch.name}</span></div>`
  ).join('');
}

function renderChannelsTab() {
  document.getElementById('channels-grid').innerHTML = CHANNELS.map(ch =>
    `<div class="ch-big c${ch.color}"><span class="ch-big-icon">${ch.icon}</span><div class="ch-big-name">${ch.name}</div><div class="ch-big-desc">${ch.desc}</div><span class="ch-big-tag">${ch.tag}</span></div>`
  ).join('');
}

function renderNotifications() {
  document.getElementById('home-notifications').innerHTML = NOTIFICATIONS.map(n =>
    `<div class="li${n.read ? ' read' : ''}"><div class="nd ${n.read ? 'dr' : 'dp'}"></div><div><p class="it">${n.text}</p><p class="is">${n.sub}</p></div></div>`
  ).join('');
}

function renderQuickAccess() {
  document.getElementById('home-quickaccess').innerHTML = QUICK_ACCESS.map(q =>
    `<div class="li" onclick="switchTab('${q.tab}')"><div style="font-size:17px;width:28px;text-align:center">${q.icon}</div><div><p class="it">${q.label}</p><p class="is">${q.sub}</p></div></div>`
  ).join('');
}

function renderFeaturedVideo() {
  const v = VIDEOS[Math.floor(Math.random() * VIDEOS.length)];
  document.getElementById('home-featured-video').innerHTML = `
    <div class="feat-vid-card" onclick="openPlayer(${v.id})">
      <div class="feat-vid-thumb">
        <div style="position:absolute;inset:0;background:linear-gradient(135deg,${v.thumbGrad[0]},${v.thumbGrad[1]})"></div>
        <div class="feat-vid-play">▶</div>
        <div class="feat-vid-dur">${v.duration}</div>
      </div>
      <div class="feat-vid-info">
        <div class="feat-vid-title">${v.title}</div>
        <div class="feat-vid-sub">${v.author} · ${v.views}</div>
      </div>
    </div>`;
}

function renderVideosTab() {
  const g = document.getElementById('vid-grid');
  g.innerHTML = '';
  VIDEOS.forEach(v => {
    const card = document.createElement('div');
    card.className = 'vid-card';
    card.onclick = () => openPlayer(v.id);
    card.innerHTML = `
      <div class="vid-thumb">
        <div class="vid-thumb-bg" style="background:linear-gradient(135deg,${v.thumbGrad[0]},${v.thumbGrad[1]})"></div>
        <div class="vid-play">▶</div>
        <div class="vid-duration">${v.duration}</div>
      </div>
      <div class="vid-info">
        <div class="vid-title">${v.title}</div>
        <div class="vid-meta">
          <div class="vid-author">
            <div class="vid-author-av" style="background:${v.authorColor}">${v.authorInitials}</div>
            <span class="vid-author-name">${v.author}</span>
          </div>
          <span class="vid-views">${v.views}</span>
        </div>
        <div class="vid-tag" style="background:${v.tagBg}18;color:${v.tagBg}">${v.tag}</div>
      </div>`;
    g.appendChild(card);
  });
}

// ── VIDEO PLAYER ──
function openPlayer(id) {
  const v = VIDEOS.find(x => x.id === id);
  if (!v) return;
  document.getElementById('vp-title').textContent = v.title;
  document.getElementById('vp-tag').textContent = v.tag;
  document.getElementById('vp-tag').style.background = v.tagBg;
  document.getElementById('vp-bg').style.background = `linear-gradient(135deg,${v.thumbGrad[0]},${v.thumbGrad[1]})`;
  document.getElementById('vp-dur').textContent = v.duration;
  document.getElementById('vp-av').textContent = v.authorInitials;
  document.getElementById('vp-av').style.background = v.authorColor;
  document.getElementById('vp-author').textContent = v.author;
  document.getElementById('vp-views-el').textContent = v.views;

  // Questions
  document.getElementById('vp-questions').innerHTML = v.questions.map((q, i) => `
    <div class="vp-q" id="vq-${id}-${i}">
      <div class="vp-q-text" onclick="toggleQ('vq-${id}-${i}')">${q.q}</div>
      <div class="vp-q-answer">${q.a}</div>
    </div>`).join('');

  // Exercises
  document.getElementById('vp-exercises').innerHTML = v.exercises.map((ex, i) => {
    if (ex.type === 'mcq') {
      return `<div class="vp-ex">
        <div class="vp-ex-label">Multiple Choice</div>
        <div class="vp-ex-text">${ex.text}</div>
        <div class="vp-ex-opts">${ex.opts.map((o, oi) =>
          `<div class="vp-opt" onclick="checkMCQ(this,${oi},${ex.correct})">${o}</div>`
        ).join('')}</div>
      </div>`;
    } else {
      return `<div class="vp-ex">
        <div class="vp-ex-label">Open Question</div>
        <div class="vp-ex-text">${ex.text}</div>
        <textarea class="vp-ex-input" id="vex-${id}-${i}" placeholder="Write your answer here…" rows="3"></textarea>
        <button class="vp-ex-submit" onclick="submitOpen('vex-${id}-${i}','vfb-${id}-${i}')">Submit</button>
        <div class="vp-ex-feedback" id="vfb-${id}-${i}"></div>
      </div>`;
    }
  }).join('');

  document.getElementById('vp-overlay').classList.add('open');
  document.getElementById('vp-overlay').querySelector('.vp-body').scrollTop = 0;
  document.body.style.overflow = 'hidden';
}

function closePlayer() {
  document.getElementById('vp-overlay').classList.remove('open');
  document.body.style.overflow = '';
}

function toggleQ(id) {
  document.getElementById(id).classList.toggle('open');
}

function checkMCQ(el, chosen, correct) {
  const opts = el.parentElement.querySelectorAll('.vp-opt');
  opts.forEach(o => o.style.pointerEvents = 'none');
  if (chosen === correct) el.classList.add('correct');
  else { el.classList.add('wrong'); opts[correct].classList.add('correct'); }
}

function submitOpen(inputId, fbId) {
  const val = document.getElementById(inputId).value.trim();
  const fb = document.getElementById(fbId);
  if (!val) { fb.style.color = 'var(--red)'; fb.textContent = 'Please write something before submitting.'; return; }
  fb.style.color = 'var(--teal)';
  fb.textContent = '✓ Answer submitted!';
  document.getElementById(inputId).disabled = true;
}

// Close player on Escape
document.addEventListener('keydown', e => { if (e.key === 'Escape') closePlayer(); });

// ── MESSAGES ──
let activeConvId = null;
let convMessages = {}; // local message state per conv id

function renderMsgList() {
  const list = document.getElementById('msg-list');
  list.innerHTML = DIRECT_MESSAGES.map(dm => `
    <div class="msg-li${activeConvId===dm.id?' active':''}" onclick="openConv(${dm.id})">
      <div class="chat-av" style="background:${dm.avatarColor}">${dm.initials}</div>
      <div class="chat-info">
        <div class="chat-name">${dm.name}</div>
        <div class="chat-prev">${dm.preview}</div>
      </div>
      <div class="chat-meta">
        <span class="chat-time">${dm.time}</span>
        ${dm.unread ? `<span class="chat-badge">${dm.unread}</span>` : ''}
      </div>
    </div>`).join('');
}

function openConv(id) {
  activeConvId = id;
  const dm = DIRECT_MESSAGES.find(d => d.id === id);
  dm.unread = 0;
  if (!convMessages[id]) convMessages[id] = [...dm.messages];
  renderMsgList();
  const win = document.getElementById('chat-window');
  win.innerHTML = `
    <div class="chat-win-hd">
      <div class="chat-av" style="background:${dm.avatarColor};width:32px;height:32px;font-size:10px">${dm.initials}</div>
      <div>
        <div class="chat-win-name">${dm.name}</div>
        <div class="chat-win-status">● Online</div>
      </div>
    </div>
    <div class="chat-messages" id="chat-msgs-${id}"></div>
    <div class="chat-input-row">
      <input class="chat-input" id="chat-input-${id}" placeholder="Message ${dm.name}…" onkeydown="if(event.key==='Enter'&&!event.shiftKey){event.preventDefault();sendMsg(${id});}">
      <button class="chat-send-btn" onclick="sendMsg(${id})">➤</button>
    </div>`;
  renderMessages(id, dm);
}

function renderMessages(id, dm) {
  const container = document.getElementById(`chat-msgs-${id}`);
  if (!container) return;
  container.innerHTML = convMessages[id].map(m => `
    <div class="chat-msg chat-msg-${m.role}">
      ${m.role==='in' ? `<div class="chat-small-av" style="background:${dm.avatarColor}">${dm.initials}</div>` : ''}
      <div>
        <div class="chat-bubble">${m.text}</div>
        <div class="chat-msg-time">${m.time}</div>
      </div>
    </div>`).join('');
  container.scrollTop = container.scrollHeight;
}

function sendMsg(id) {
  const input = document.getElementById(`chat-input-${id}`);
  const text = input.value.trim();
  if (!text) return;
  const now = new Date();
  const time = now.getHours().toString().padStart(2,'0') + ':' + now.getMinutes().toString().padStart(2,'0');
  convMessages[id].push({ role:'out', text, time });
  const dm = DIRECT_MESSAGES.find(d => d.id === id);
  dm.preview = text;
  input.value = '';
  renderMessages(id, dm);
  renderMsgList();
}

// ── NAV ──
const PAGE_INFO = {
  home:     { title:'Dashboard',  sub:'Good morning, Alex 👋' },
  channels: { title:'Channels',   sub:'Your workspaces and departments' },
  kalender: { title:'Calendar',   sub:'Meetings, deadlines & events' },
  videos:   { title:'Videos',     sub:'Recordings and training content' },
  messages: { title:'Messages',   sub:'Direct messages and group chats' },
  profil:   { title:'Profile',    sub:'Alex Johnson · Product Manager' },
};
function switchTab(tab) {
  document.querySelectorAll('.sni,.ni').forEach(n => n.classList.toggle('active', n.dataset.tab===tab));
  document.querySelectorAll('.tp').forEach(p => p.classList.remove('active'));
  document.getElementById('tab-'+tab).classList.add('active');
  document.getElementById('main-scroll').scrollTop = 0;
  const i = PAGE_INFO[tab]||{};
  document.getElementById('page-title').textContent = i.title||tab;
  document.getElementById('page-sub').textContent = i.sub||'';
}
document.querySelectorAll('.sni,.ni').forEach(n => n.addEventListener('click',()=>switchTab(n.dataset.tab)));

// ── CALENDAR ──
const T = new Date();
const MONTHS = ['January','February','March','April','May','June','July','August','September','October','November','December'];
const DAYS = ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
const COLS = { red:{bar:'#E24B4A',dot:'dred'}, amber:{bar:'#E8960A',dot:'damb'}, teal:{bar:'#1D9E75',dot:'dteal'}, purple:{bar:'#5B50D6',dot:'dacc'} };
let vy=T.getFullYear(), vm=T.getMonth(), sel=null, eid=null;
let evs = [
  {id:1, date:f(T.getFullYear(),T.getMonth(),15),  title:'Q3 Strategy Review',   detail:'10:00 – 12:00 · Conference Room A', type:'red'},
  {id:2, date:f(T.getFullYear(),T.getMonth(),22),  title:'All-Hands Meeting',     detail:'14:00 – 15:30 · Main Hall',          type:'amber'},
  {id:3, date:f(T.getFullYear(),T.getMonth()+1,3), title:'Team Off-site',         detail:'Fri–Sun · Berlin',                    type:'teal'},
  {id:4, date:f(T.getFullYear(),T.getMonth(),28),  title:'Product Launch',        detail:'09:00 · Virtual + In-person',         type:'purple'},
];
let nid = 5;
function f(y,m,d){const dt=new Date(y,m,d);return dt.getFullYear()+'-'+String(dt.getMonth()+1).padStart(2,'0')+'-'+String(dt.getDate()).padStart(2,'0');}
function td(){return f(T.getFullYear(),T.getMonth(),T.getDate());}
function rc(){
  const g=document.getElementById('cg');
  document.getElementById('ct').textContent=MONTHS[vm]+' '+vy;
  g.innerHTML='';
  const fd=new Date(vy,vm,1).getDay(), off=fd===0?6:fd-1;
  const dim=new Date(vy,vm+1,0).getDate(), dimp=new Date(vy,vm,0).getDate();
  const tot=Math.ceil((off+dim)/7)*7;
  for(let i=0;i<tot;i++){
    let cd,om=false;
    if(i<off){cd=new Date(vy,vm-1,dimp-off+i+1);om=true;}
    else if(i>=off+dim){cd=new Date(vy,vm+1,i-off-dim+1);om=true;}
    else cd=new Date(vy,vm,i-off+1);
    const ds=f(cd.getFullYear(),cd.getMonth(),cd.getDate());
    const c=document.createElement('div');c.className='cdc';
    if(om)c.classList.add('om');
    if(ds===td())c.classList.add('today');
    if(sel&&ds===sel&&ds!==td())c.classList.add('sel');
    const n=document.createElement('div');n.className='dn';n.textContent=cd.getDate();c.appendChild(n);
    const de=evs.filter(e=>e.date===ds);
    if(de.length){const dots=document.createElement('div');dots.className='eds';de.slice(0,3).forEach(e=>{const d=document.createElement('div');d.className='ed '+(COLS[e.type]||COLS.purple).dot;dots.appendChild(d);});c.appendChild(dots);}
    c.addEventListener('click',()=>{sel=ds;rc();rel();});
    g.appendChild(c);
  }
}
function rel(){
  const l=document.getElementById('cel'),lb=document.getElementById('csl');
  if(!sel){lb.textContent='Select a day';l.innerHTML='<p class="ne">Click a day to see events</p>';return;}
  const[y,m,d]=sel.split('-').map(Number);
  lb.textContent=DAYS[new Date(y,m-1,d).getDay()]+', '+MONTHS[m-1]+' '+d;
  const de=evs.filter(e=>e.date===sel);
  if(!de.length){l.innerHTML='<p class="ne">No events on this day</p>';return;}
  l.innerHTML='';
  de.forEach(ev=>{
    const c=COLS[ev.type]||COLS.purple,el=document.createElement('div');el.className='eli';
    el.innerHTML=`<div class="ecb" style="background:${c.bar}"></div><div style="flex:1;min-width:0"><div class="elt">${ev.title}</div><div class="els">${ev.detail}</div></div><div class="ea"><button class="eb" onclick="oe(${ev.id})">✏️</button><button class="eb del" onclick="de2(${ev.id})">🗑</button></div>`;
    l.appendChild(el);
  });
}
function rhu(){
  const c=document.getElementById('home-upcoming');
  const up=evs.filter(e=>e.date>=td()).sort((a,b)=>a.date.localeCompare(b.date)).slice(0,3);
  if(!up.length){c.innerHTML='<div class="li"><p class="is">No upcoming events</p></div>';return;}
  c.innerHTML='';
  up.forEach(ev=>{
    const col=COLS[ev.type]||COLS.purple,[y,m,d]=ev.date.split('-').map(Number),el=document.createElement('div');el.className='li';
    el.innerHTML=`<div style="width:3px;height:34px;border-radius:2px;background:${col.bar};flex-shrink:0"></div><div><p class="it">${ev.title}</p><p class="is">${MONTHS[m-1]} ${d} · ${ev.detail}</p></div>`;
    c.appendChild(el);
  });
}
document.getElementById('cp').addEventListener('click',()=>{vm--;if(vm<0){vm=11;vy--;}rc();rel();});
document.getElementById('cn').addEventListener('click',()=>{vm++;if(vm>11){vm=0;vy++;}rc();rel();});
function openAdd(){eid=null;document.getElementById('mh').textContent='Add Event';document.getElementById('et').value='';document.getElementById('ed').value=sel||td();document.getElementById('ede').value='';document.getElementById('ety').value='amber';document.getElementById('modal').classList.add('open');}
function oe(id){const ev=evs.find(e=>e.id===id);if(!ev)return;eid=id;document.getElementById('mh').textContent='Edit Event';document.getElementById('et').value=ev.title;document.getElementById('ed').value=ev.date;document.getElementById('ede').value=ev.detail;document.getElementById('ety').value=ev.type;document.getElementById('modal').classList.add('open');}
function cm(){document.getElementById('modal').classList.remove('open');}
function de2(id){evs=evs.filter(e=>e.id!==id);rc();rel();rhu();}
document.getElementById('cadd').addEventListener('click',openAdd);
document.getElementById('mcancel').addEventListener('click',cm);
document.getElementById('modal').addEventListener('click',e=>{if(e.target===e.currentTarget)cm();});
document.getElementById('msave').addEventListener('click',()=>{
  const t=document.getElementById('et').value.trim(),d=document.getElementById('ed').value,det=document.getElementById('ede').value.trim(),ty=document.getElementById('ety').value;
  if(!t||!d)return;
  if(eid!==null){const ev=evs.find(e=>e.id===eid);if(ev)Object.assign(ev,{title:t,date:d,detail:det,type:ty});}
  else evs.push({id:nid++,date:d,title:t,detail:det,type:ty});
  cm();rc();rel();rhu();
});
rc();rel();rhu();

// ── BOOT ──
renderStats();
renderHomeChannels();
renderChannelsTab();
renderNotifications();
renderQuickAccess();
renderFeaturedVideo();
renderVideosTab();
renderMsgList();
document.getElementById('prof-ch-count').textContent = CHANNELS.length;
</script>
</body>
</html>
