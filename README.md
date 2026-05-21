<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>나는 어떤 몬스터인가 — 세계 괴담 테스트</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@300;400;600;700&family=Noto+Sans+KR:wght@300;400;700&family=Noto+Serif+KR:wght@400;700;900&family=Jua&display=swap" rel="stylesheet">
<style>
:root {
  --bg:      #080a0e;
  --bg2:     #0d1117;
  --card:    #10141c;
  --gold:    #e8c547;
  --gold2:   #f0d060;
  --gold3:   #f8e898;
  --red:     #ff6b35;
  --red2:    #e8a030;
  --cream:   #e8ecf4;
  --dim:     #4a5060;
  --dim2:    #8090a8;
  --border:  rgba(232,197,71,0.25);
  --brite:   rgba(232,197,71,0.6);
}
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
body{
  background:var(--bg);
  font-family:'Noto Sans KR',sans-serif;
  color:var(--cream);
  min-height:100vh;
  overflow-x:hidden;
  /* ✅ 수정 7: word-break keep-all */
  word-break:keep-all;
  overflow-wrap:break-word;
  cursor:default;
  transition:filter 1.5s ease;
}
body.darkening { filter: brightness(0.88) saturate(0.92); }
body.darker    { filter: brightness(0.78) saturate(0.85); }

/* ── BG ── */
body::before{
  content:'';position:fixed;inset:0;pointer-events:none;z-index:0;
  background:
    radial-gradient(ellipse 70% 50% at 50% 0%,   rgba(30,40,60,0.22) 0%,transparent 60%),
    radial-gradient(ellipse 50% 70% at 10% 50%,  rgba(232,197,71,0.08) 0%,transparent 60%),
    radial-gradient(ellipse 50% 70% at 90% 50%,  rgba(232,197,71,0.08) 0%,transparent 60%),
    radial-gradient(ellipse 100% 60% at 50% 100%,rgba(100,10,140,0.18) 0%,transparent 50%);
}
body::after{
  content:'';position:fixed;inset:0;pointer-events:none;z-index:0;
  background:radial-gradient(ellipse 90% 90% at 50% 50%,transparent 45%,rgba(10,0,20,0.55) 100%);
}

/* ── CURTAINS ── */
.curtain{position:fixed;top:0;height:100vh;width:55px;z-index:2;pointer-events:none}
.curtain-l{left:0; background:linear-gradient(90deg,rgba(30,40,60,0.25),transparent)}
.curtain-r{right:0;background:linear-gradient(270deg,rgba(30,40,60,0.25),transparent)}

/* ── SCANLINES ── */
.scanlines{position:fixed;inset:0;pointer-events:none;z-index:2;
  background:repeating-linear-gradient(0deg,transparent,transparent 3px,rgba(0,0,0,0.025) 3px,rgba(0,0,0,0.025) 4px)}

/* ── PARTICLES ── */
#ptcl{position:fixed;inset:0;pointer-events:none;z-index:2;overflow:hidden}
.p{position:absolute;animation:pfloat linear infinite;opacity:0.13;user-select:none;font-family:'Rajdhani',sans-serif;color:var(--gold);}
@keyframes pfloat{from{transform:translateY(108vh) rotate(0deg);opacity:.1}to{transform:translateY(-5vh) rotate(540deg);opacity:0}}

/* ── LAYOUT ── */
#app{position:relative;z-index:3;min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:2.5rem 1rem}
.screen{display:none;width:100%;max-width:700px;flex-direction:column;align-items:center}
.screen.active{display:flex;animation:reveal .6s cubic-bezier(.22,1,.36,1) both}
@keyframes reveal{from{opacity:0;transform:translateY(28px) scale(.96)}to{opacity:1;transform:none}}

/* ── ORNAMENTAL ── */
.orn{display:flex;align-items:center;gap:.7rem;width:100%;margin:1rem 0;color:var(--gold);font-size:.75rem;letter-spacing:.3em}
.orn::before,.orn::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,transparent,var(--gold),transparent)}

/* ── CARD ── */
.card{
  background:var(--card);
  border:1.5px solid var(--border);
  border-radius:4px;
  padding:2rem 1.8rem;
  width:100%;position:relative;overflow:hidden;
  box-shadow:0 0 0 1px rgba(224,168,74,0.12),0 12px 50px rgba(0,0,0,.5),inset 0 1px 0 rgba(224,168,74,0.14);
}
.card::before{content:'';position:absolute;top:0;left:10%;width:80%;height:1.5px;background:linear-gradient(90deg,transparent,var(--gold),var(--gold2),transparent)}
.card::after {content:'';position:absolute;bottom:0;left:10%;width:80%;height:1px;background:linear-gradient(90deg,transparent,rgba(201,146,58,0.3),transparent)}
.card .co{position:absolute;color:var(--gold);font-size:1rem;opacity:.35}
.card .co.tl{top:.6rem;left:.7rem}.card .co.tr{top:.6rem;right:.7rem}
.card .co.bl{bottom:.6rem;left:.7rem}.card .co.br{bottom:.6rem;right:.7rem}

/* ── BUTTONS ── */
.btn{
  display:inline-flex;align-items:center;gap:.5rem;
  padding:.85rem 2.6rem;border:none;border-radius:3px;
  font-family:'Noto Sans KR',sans-serif;font-size:1.25rem;font-weight:700;
  cursor:pointer;transition:all .2s ease;letter-spacing:.05em;
}
.btn-main{
  background:linear-gradient(135deg,#e8c547,#e8a030);
  color:#ffffff;
  box-shadow:0 0 0 1.5px var(--gold),0 6px 28px rgba(30,40,60,.55);
  text-shadow:0 1px 3px rgba(0,0,0,.5);
  border-radius:50px;
}
/* ── 인트로 화면 텍스트 흰색 오버라이드 ── */
#sc-intro .intro-sub,
#sc-intro .story-box,
#sc-intro .ax-item span,
#sc-intro .ax-item { color: rgba(255,255,255,0.8); }
#sc-intro .story-box { color: rgba(255,255,255,0.8); border-left-color: var(--red2); }
#sc-intro > div[style*="color:var(--dim)"] { color: rgba(255,255,255,0.8) !important; }
.btn-main:hover{transform:translateY(-2px);box-shadow:0 0 0 1.5px var(--gold2),0 10px 36px rgba(150,30,200,.7)}
.btn-main:active{transform:scale(.97)}
.btn-ghost{background:transparent;border:1px solid var(--border);color:var(--dim2);font-size:1.05rem;padding:.7rem 1.8rem}
.btn-ghost:hover{border-color:var(--gold);color:var(--gold)}

/* ════ INTRO ════ */
.intro-marquee{font-family:'Rajdhani',sans-serif;font-size:.7rem;letter-spacing:.4em;color:var(--gold);text-transform:uppercase;text-align:center;margin-bottom:1.2rem;opacity:.6}

/* ✅ 수정 1: 제목 둥근 폰트 + 단색 */
.intro-title{
  font-family:'Jua',sans-serif;
  font-size:clamp(2rem,7vw,3.4rem);
  font-weight:900;
  text-align:center;
  line-height:1.1;
  color: var(--gold2);
  filter:drop-shadow(0 0 20px rgba(201,146,58,.4));
  margin-bottom:.5rem;
}

.intro-sub{font-family:'Rajdhani',sans-serif;font-size:.95rem;color:var(--dim2);letter-spacing:.15em;text-align:center;margin-bottom:.2rem}
.intro-sigil{margin:1rem auto 1.2rem;animation:sigilPulse 6s ease-in-out infinite}
@keyframes sigilPulse{0%,100%{filter:drop-shadow(0 0 18px rgba(232,197,71,.45)) brightness(1)}50%{filter:drop-shadow(0 0 32px rgba(232,197,71,.75)) brightness(1.08)}}
.intro-big{font-size:6rem;text-align:center;margin:1rem 0;animation:flicker 4s ease-in-out infinite;filter:drop-shadow(0 0 30px rgba(201,146,58,.6))}
@keyframes flicker{0%,100%{opacity:1}92%{opacity:1}93%{opacity:.6}94%{opacity:1}96%{opacity:.7}97%{opacity:1}}

/* ── STORY BOX ── */
.story-box{
  background:rgba(30,40,60,0.15);
  border:1px solid rgba(224,168,74,0.3);
  border-left:3px solid var(--red2);
  border-radius:4px;
  padding:1.2rem 1.4rem;
  font-size:1.05rem;line-height:1.95;
  color:var(--dim2);
  text-align:left;
  max-width:480px;
  width:100%;
  margin-bottom:1.6rem;
  position:relative;
}
.story-box::before{
  content:'"';
  position:absolute;top:-.5rem;left:.8rem;
  font-family:'Rajdhani',sans-serif;font-size:3rem;
  color:var(--red2);opacity:.3;line-height:1;
}
.story-kw{
  color:var(--gold2);
  font-weight:700;
  /* ✅ 수정 2: 키워드 opacity 90% */
  opacity:0.9;
}

/* ✅ 수정 4: axis 항목 — 전체 중앙, 내부 좌측 정렬로 깔끔하게 */
.axis-explain{display:flex;flex-direction:column;gap:.35rem;margin-bottom:2rem;width:100%;max-width:280px;align-self:center;align-items:flex-start}
.ax-item{display:flex;align-items:center;gap:0;padding:.15rem 0}
.ax-item span{
  font-size:.88rem !important;
  color:rgba(255,255,255,0.8);
}
.ax-item .ax-label{
  color:var(--gold) !important;
  font-family:'Rajdhani',sans-serif !important;
  letter-spacing:.1em;
  font-size:.88rem !important;
  width:88px;
  flex-shrink:0;
}
.ax-sep{color:rgba(224,168,74,.3);margin:0 .4rem;font-size:.88rem;flex-shrink:0;}

/* ════ PROGRESS ════ */
.prog-wrap{width:100%;margin-bottom:1.5rem}
.prog-meta{display:flex;justify-content:space-between;font-size:1rem;color:var(--dim2);margin-bottom:.5rem}
.prog-track{width:100%;height:6px;background:rgba(201,146,58,.1);position:relative;overflow:hidden}
.prog-track::before{content:'';position:absolute;inset:0;background:repeating-linear-gradient(90deg,rgba(201,146,58,.05) 0,rgba(201,146,58,.05) 2px,transparent 2px,transparent 12px)}
.prog-fill{height:100%;background:linear-gradient(90deg,var(--red2),var(--gold),var(--gold2));transition:width .55s cubic-bezier(.4,0,.2,1);box-shadow:0 0 8px rgba(201,146,58,.5)}

/* AXIS TRACKER */
.atrack{display:flex;gap:.4rem;justify-content:center;flex-wrap:wrap;margin-bottom:1.4rem}
.atag{padding:.2rem .75rem;border-radius:20px;font-size:.88rem;font-weight:700;border:1px solid rgba(224,168,74,.25);color:var(--dim2);background:rgba(224,168,74,.08);transition:all .35s;letter-spacing:.05em}
.atag.on{background:rgba(224,168,74,.22);border-color:var(--gold);color:var(--gold2)}

/* ════ QUESTION ════ */
.q-scene{
  font-family:'Rajdhani',sans-serif;font-size:.65rem;letter-spacing:.35em;
  color:var(--red2);text-align:center;margin-bottom:.3rem;
  text-transform:uppercase;opacity:.8;
}
.q-num{font-family:'Rajdhani',sans-serif;font-size:.75rem;letter-spacing:.35em;color:var(--gold);text-align:center;margin-bottom:.5rem;opacity:.7}
.q-emoji{font-size:3.8rem;text-align:center;margin-bottom:.8rem;animation:bob .9s ease-in-out infinite}
.q-img-slot{
  width:100px;height:100px;
  margin:0 auto .8rem;
  border:1px dashed rgba(232,197,71,0.25);
  border-radius:2px;
  background:rgba(30,40,60,0.08);
  display:flex;align-items:center;justify-content:center;
}
.q-img-slot img{width:100%;height:100%;object-fit:contain;border-radius:2px}
.q-img-slot:empty::after{
  content:'IMG';
  font-family:'Rajdhani',sans-serif;font-size:.6rem;
  letter-spacing:.25em;color:rgba(232,197,71,0.2);
}
@keyframes bob{0%,100%{transform:translateY(0)}50%{transform:translateY(-8px)}}

.q-situation{
  background:rgba(160,40,40,.12);
  border-left:2px solid rgba(224,168,74,.45);
  padding:.6rem .9rem;
  font-size:.95rem;line-height:1.75;
  color:var(--dim2);
  margin-bottom:.9rem;
  font-style:italic;
}
.q-text{font-size:1.35rem;font-weight:700;text-align:center;line-height:1.5;color:rgba(232,236,244,0.8);margin-bottom:1.6rem}

.choices{display:flex;flex-direction:column;gap:.7rem;width:100%}
.choice{
  padding:.95rem 1.3rem;
  background:rgba(224,168,74,.07);
  border:1.5px solid rgba(224,168,74,.22);
  border-radius:4px;
  color:var(--cream);font-family:'Noto Sans KR',sans-serif;font-size:1.15rem;
  text-align:left;cursor:pointer;
  transition:all .2s ease;
  display:flex;align-items:center;gap:.9rem;
  position:relative;overflow:hidden;
}
.choice::before{content:'';position:absolute;left:0;top:0;width:3px;height:100%;background:var(--red2);transform:scaleY(0);transition:transform .2s}
.choice:hover{background:rgba(224,168,74,.16);border-color:var(--gold);padding-left:1.6rem}
.choice:hover::before{transform:scaleY(1)}
.choice.chosen{background:rgba(30,40,60,.32);border-color:var(--red2);animation:choicePop .3s ease}
.choice.chosen::before{transform:scaleY(1)}
@keyframes choicePop{0%{transform:scale(1)}50%{transform:scale(1.01) translateX(4px)}100%{transform:translateX(4px)}}
.cico{font-size:1.5rem;flex-shrink:0}

/* ════ REVEAL SCREEN ════ */
#sc-reveal{background:transparent}
.reveal-wrap{
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  min-height:60vh;text-align:center;gap:1.5rem;
}
.reveal-msg{
  font-family:'Rajdhani',sans-serif;
  font-size:clamp(1.2rem,4vw,1.8rem);
  color:var(--gold2);
  letter-spacing:.1em;
  line-height:1.6;
  animation:pulseText 1.5s ease-in-out infinite;
}
@keyframes pulseText{0%,100%{opacity:.6}50%{opacity:1}}
.reveal-dots{font-size:2rem;letter-spacing:.3em;color:var(--red2);animation:dotPulse 1s ease-in-out infinite}
@keyframes dotPulse{0%,100%{opacity:.3}50%{opacity:1}}

/* ════ RESULT ════ */
.result-seal{display:flex;align-items:center;justify-content:center;font-size:7.5rem;
  width:100%;margin-bottom:0;animation:sealIn .85s cubic-bezier(.175,.885,.32,1.275) both;}
.result-img-card {
  height: 100%;
  margin-bottom: 0;
  background: #1a0d24;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 3rem 1.2rem;
  border: 1.5px solid var(--border);
  border-radius: 22px;
  position: relative;
  overflow: hidden;
  box-shadow: 0 0 0 1px rgba(224,168,74,0.1), 0 16px 60px rgba(0,0,0,.6), inset 0 1px 0 rgba(224,168,74,0.12);
}
.result-img-card::before{content:'';position:absolute;top:0;left:10%;width:80%;height:1.5px;background:linear-gradient(90deg,transparent,var(--gold),var(--gold2),transparent)}
.result-img-card .co{position:absolute;color:var(--gold);font-size:1rem;opacity:.35}
.result-img-card .co.tl{top:.6rem;left:.7rem}
.result-img-card .co.tr{top:.6rem;right:.7rem}
@keyframes sealIn{from{transform:scale(0) rotate(-20deg);opacity:0}to{transform:none;opacity:1}}
.result-origin{font-family:'Rajdhani',sans-serif;font-size:.75rem;letter-spacing:.4em;color:var(--gold);text-align:center;margin-bottom:.3rem;text-transform:uppercase;animation:reveal .5s .2s both}
.result-name{
  font-family:'Noto Serif KR',serif;font-size:clamp(1.8rem,5.5vw,2.7rem);font-weight:900;
  text-align:center;line-height:1.2;margin-bottom:.3rem;
  background:linear-gradient(135deg,var(--gold3),var(--gold));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  background-clip: text;
  filter:drop-shadow(0 0 12px rgba(201,146,58,.3));
  animation:reveal .5s .3s both;
}
.result-aka{font-size:1rem;color:var(--dim2);text-align:center;margin-bottom:1.5rem;animation:reveal .5s .35s both}
.result-code{display:flex;gap:.45rem;justify-content:center;margin-bottom:1.5rem}
.rc{
  width:2.6rem;height:2.6rem;border-radius:10px;
  display:flex;align-items:center;justify-content:center;
  font-family:'Rajdhani',sans-serif;font-size:1.2rem;font-weight:700;
  border:1.5px solid var(--gold);color:var(--gold2);
  background:rgba(201,146,58,.1);
  animation:rcIn .4s cubic-bezier(.175,.885,.32,1.275) both;
}
@keyframes rcIn{from{transform:scale(0) rotate(-10deg);opacity:0}to{transform:none;opacity:1}}
.result-lore{font-family:'Rajdhani',sans-serif;font-size:.7rem;letter-spacing:.25em;color:var(--dim);text-align:center;margin-bottom:.8rem;text-transform:uppercase;border-top:1px solid var(--border);border-bottom:1px solid var(--border);padding:.5rem 0}
.result-desc{font-size:1.1rem;line-height:1.9;color:var(--dim2);text-align:center;margin-bottom:1.4rem}
.r-stats{display:grid;grid-template-columns:1fr 1fr;gap:.65rem;margin-bottom:1.4rem}
.rstat{background:rgba(224,168,74,.1);border:1px solid rgba(224,168,74,.2);border-radius:10px;padding:.7rem;text-align:center}
.rstat-l{font-size:.85rem;color:rgba(255,255,255,0.6);margin-bottom:.2rem}
.rstat-v{font-size:1rem;font-weight:700;color:var(--gold2)}
.horror-scroll{background:rgba(110,20,150,.18);border:1px solid rgba(160,60,200,.4);border-radius:4px;padding:1rem 1.2rem;margin-bottom:1.4rem;font-size:1.05rem;line-height:1.85;color:var(--dim2);position:relative}
.horror-scroll-title{font-family:'Rajdhani',sans-serif;font-size:.7rem;letter-spacing:.3em;color:var(--red2);display:block;margin-bottom:.4rem;text-transform:uppercase}
.compat-box{background:rgba(224,168,74,.1);border:1px solid var(--border);border-radius:4px;padding:.85rem 1.2rem;margin-bottom:1.8rem;text-align:left;font-size:1.05rem;color:var(--gold2)}
.compat-label{font-size:.75rem;letter-spacing:.2em;color:rgba(255,255,255,0.6);display:block;margin-bottom:.25rem;text-transform:uppercase;font-family:'Rajdhani',sans-serif}
.btn-row{display:flex;gap:.8rem;justify-content:center;flex-wrap:wrap}

/* ════ ALL GRID ════ */
.all-title{font-family:'Rajdhani',sans-serif;font-size:1.6rem;font-weight:900;text-align:center;margin-bottom:.3rem;background:linear-gradient(135deg,var(--gold3),var(--gold));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip: text;letter-spacing:.05em}
.all-sub{font-size:.75rem;color:var(--dim);text-align:center;letter-spacing:.3em;margin-bottom:1.5rem;font-family:'Rajdhani',sans-serif;opacity:.7}
.all-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(145px,1fr));gap:.75rem;width:100%;margin-bottom:1.8rem}
.monster-tile{
  background:linear-gradient(145deg,rgba(224,168,74,.06) 0%,rgba(30,40,60,.12) 100%);
  border:1.5px solid rgba(224,168,74,.18);border-radius:4px;padding:1rem .7rem;text-align:center;cursor:pointer;transition:all .2s;
  position:relative;overflow:hidden;
}
.monster-tile::before{content:'';position:absolute;top:0;left:15%;width:70%;height:1px;background:linear-gradient(90deg,transparent,rgba(232,197,71,.3),transparent)}
.monster-tile:hover{background:linear-gradient(145deg,rgba(224,168,74,.16) 0%,rgba(160,40,180,.22) 100%);border-color:var(--gold);transform:scale(1.04) translateY(-2px)}
.monster-tile.me{background:linear-gradient(145deg,rgba(160,40,40,.25) 0%,rgba(30,40,60,.3) 100%);border-color:var(--red2)}
.tile-emoji{font-size:2.4rem;margin-bottom:.35rem;display:flex;align-items:center;justify-content:center;height:64px;}
.tile-code{font-family:'Rajdhani',sans-serif;font-size:.65rem;letter-spacing:.2em;color:var(--gold);margin-bottom:.2rem}
.tile-name{font-size:.95rem;color:var(--cream);line-height:1.3}
.tile-me{font-size:.7rem;color:var(--gold2);margin-top:.3rem;letter-spacing:.08em;font-family:'Rajdhani',sans-serif}

.result-monster-img{width:360px;height:360px;max-width:90vw;max-height:90vw;object-fit:contain}

.tile-tooltip {
  position:fixed;z-index:999;
  background:var(--card);border:1.5px solid var(--gold);border-radius:4px;
  padding:1rem 1.2rem;max-width:260px;
  box-shadow:0 8px 40px rgba(0,0,0,.8),0 0 0 1px rgba(224,168,74,.1);
  pointer-events:none;
  animation:reveal .2s ease both;
}
.tile-tooltip-name{font-family:'Rajdhani',sans-serif;font-size:.95rem;font-weight:700;color:var(--gold2);margin-bottom:.3rem}
.tile-tooltip-origin{font-size:.75rem;color:var(--dim);margin-bottom:.5rem;letter-spacing:.05em}
.tile-tooltip-desc{font-size:.88rem;line-height:1.65;color:var(--dim2)}

#flash{position:fixed;inset:0;background:#e8a030;opacity:0;pointer-events:none;z-index:999}
.doflash{animation:flashfx .45s ease!important}
@keyframes flashfx{0%{opacity:0}20%{opacity:.1}100%{opacity:0}}

#bigflash{position:fixed;inset:0;background:#000;opacity:0;pointer-events:none;z-index:998;transition:opacity .3s}

::-webkit-scrollbar{width:5px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:rgba(201,146,58,.2);border-radius:2px}

/* ✅ 수정 5: crack layer — z-index를 낮게, 애니메이션 위로 올라오지 않게 */
#crack-layer{
  position:fixed;inset:0;pointer-events:none;
  z-index:1; /* 낮춰서 콘텐츠(z-index:3) 위로 올라오지 않게 */
  opacity:0;transition:opacity 1.2s ease;
}
#crack-layer.crack1{opacity:.2}
#crack-layer.crack2{opacity:.4}
#crack-layer.crack3{opacity:.6; filter: drop-shadow(0 0 8px rgba(220,120,20,.75));}

/* ── SOUL ROULETTE ── */
.roulette-wrap {
  position: relative;
  width: 100%;
  max-width: 320px;
  margin: 2.5rem auto;
  min-height: 180px; 
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  perspective: 1000px;
}
.soul-roulette{
  font-size:6rem;text-align:center;
  font-family:'Noto Serif KR',serif;
  animation:soulSpin .08s steps(1) infinite;
  filter:drop-shadow(0 0 30px rgba(201,146,58,.8));
}
@keyframes soulSpin{0%{transform:scale(1)}50%{transform:scale(1.08) rotate(5deg)}}

.reveal-title{
  font-family:'Rajdhani',sans-serif;
  font-size:clamp(.75rem,2.5vw,1rem);
  letter-spacing:.4em;color:var(--red2);
  text-transform:uppercase;opacity:.7;
  margin-bottom:.5rem;
}

/* ── FLIP CARD ── */
.flip-wrap {
  width: 100%;
  perspective: 1200px;
  margin-bottom: 1.4rem;
  cursor: pointer;
  height: 620px;
}
.flip-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}
.flip-wrap.flipped .flip-inner {
  transform: rotateY(180deg);
}
.flip-front, .flip-back {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}
.flip-back {
  transform: rotateY(180deg);
}
.flip-back-content {
  background: #0e0812;
  border: 1.5px solid var(--gold);
  border-radius: 22px;
  padding: 1.6rem 1.4rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  gap: 0.85rem;
  box-shadow: 0 20px 80px rgba(0, 0, 0, 0.9);
  overflow-y: auto;
  overflow-x: hidden;
  position: relative;
  box-sizing: border-box;
}
.flip-back-content::before {
  content:''; position:absolute; top:0; left:10%; width:80%; height:1.5px;
  background:linear-gradient(90deg,transparent,var(--gold),var(--gold2),transparent);
}
.flip-back-content .flip-back-name { margin-bottom: 0; }
.flip-back-content .flip-back-stats { margin-bottom: 0; }
.flip-back-content .horror-scroll   { margin-bottom: 0; }
.flip-back-content .compat-box      { margin-bottom: 0; }

.flip-back-name {
  font-family:'Noto Serif KR',serif; font-size:clamp(1.2rem,3.5vw,1.6rem); font-weight:900;
  text-align:center;
  background:linear-gradient(135deg,var(--gold3),var(--gold));
  -webkit-background-clip:text; -webkit-text-fill-color:transparent;
  background-clip: text;
  margin-bottom:.1rem;
  flex-shrink:0;
}
.flip-back-desc {
  font-size: .9rem;
  line-height: 1.65;
  color: rgba(232,236,244,0.8);
  text-align: center;
  word-break: keep-all;
  flex-shrink:0;
}
.flip-hint {
  font-family:'Rajdhani',sans-serif; font-size:.8rem; letter-spacing:.25em;
  color:var(--gold2); text-align:center; margin-top:1.4rem;
  opacity:0; animation:hintFadeIn 1s ease 1.2s forwards, pulseText 2s ease-in-out 2.2s infinite;
}
@keyframes hintFadeIn{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:none}}
.flip-back-stats{display:grid;grid-template-columns:1fr 1fr;gap:.4rem;width:100%;margin-bottom:.2rem;flex-shrink:0}
.flip-back-stat{background:rgba(232,197,71,.08);border:1px solid rgba(232,197,71,.18);border-radius:8px;padding:.4rem .6rem;text-align:center}
.flip-back-stat-l{font-size:.75rem;color:rgba(255,255,255,0.6);margin-bottom:.1rem}
.flip-back-stat-v{font-size:.82rem;font-weight:700;color:var(--gold2)}
#qimgslot svg {
  width: 50px;
  height: 50px;
  stroke: var(--dim2);
}

/* ✅ 수정 6: SCENE OVERLAY — 닫을 때 애니메이션도 정지 */
#scene-overlay{
  position:fixed;inset:0;z-index:9999;
  background:rgba(0,0,0,0.82);
  display:flex;align-items:center;justify-content:center;
  opacity:0;pointer-events:none;
  transition:opacity 0.6s ease;
  padding:20px;
}
#scene-overlay.active{opacity:1;pointer-events:all;}
#scene-overlay img{
  width:min(560px,88vw);
  height:min(340px,52vw);
  max-height:55vh;
  object-fit:cover;
  display:block;
  border-radius:4px;
  box-shadow:0 8px 48px rgba(0,0,0,0.7),0 0 0 1px rgba(255,255,255,0.07);
  transform:scale(0.93);
  transition:transform 0.6s ease;
}
#scene-overlay.active img{
  transform:scale(1);
}
/* 닫기 버튼 */
#scene-close-btn {
  position: absolute;
  top: 18px;
  right: 22px;
  background: rgba(255,255,255,0.12);
  border: 1px solid rgba(255,255,255,0.25);
  color: #fff;
  font-size: 1.4rem;
  width: 2.2rem;
  height: 2.2rem;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background .2s;
  z-index: 10000;
  line-height: 1;
}
#scene-close-btn:hover { background: rgba(255,255,255,0.25); }

/* ✅ 수정 3: 촛불 glow 이펙트 — 더 선명하되 텍스트에 거슬리지 않게 */
#candle-glow {
  position: fixed;
  pointer-events: none;
  z-index: 9998;
  width: 260px;
  height: 260px;
  border-radius: 50%;
  background: radial-gradient(circle,
    rgba(255,215,90,0.28) 0%,
    rgba(255,160,30,0.13) 38%,
    rgba(255,100,10,0.05) 62%,
    transparent 78%
  );
  transform: translate(-50%, -50%);
  filter: blur(10px);
  transition: opacity 0.6s ease;
  opacity: 0;
  mix-blend-mode: screen;
}

/* ── MOBILE RESPONSIVE ── */
@media (max-width: 600px) {
  #app {
    padding: 1rem 0.6rem;
    justify-content: flex-start;
    padding-top: 1.2rem;
  }
  .screen { max-width: 100%; }
  .card { padding: 1.4rem 1.1rem; border-radius: 14px; }
  .choice { padding: 0.8rem 1rem; font-size: 1rem; }
  .btn { padding: 0.75rem 1.8rem; font-size: 1.1rem; }
  #scene-overlay img { width: 92vw; height: 56vw; max-height: 48vh; border-radius: 10px; }
  .rev-img, .result-img { max-width: 100%; height: auto; }
  #atrack { font-size: 0.78rem; gap: 6px; }
  .prog-wrap { padding: 0 0.2rem; }
  .curtain { width: 28px !important; }
}
@media (max-width: 380px) {
  .card { padding: 1.1rem 0.8rem; }
  .choice { font-size: 0.93rem; padding: 0.7rem 0.85rem; }
}

/* ── SCENE REPLAY BUTTON ── */
#btn-scene-replay {
  display: none;
  align-items: center;
  gap: .4rem;
  padding: .42rem 1rem;
  font-size: .82rem;
  background: rgba(224,168,74,.1);
  color: var(--gold2);
  border: 1px solid rgba(224,168,74,.3);
  border-radius: 50px;
  font-family: 'Noto Sans KR', sans-serif;
  letter-spacing: .08em;
  cursor: pointer;
  transition: background .2s, border-color .2s;
}
#btn-scene-replay:hover { background: rgba(224,168,74,.2); border-color: rgba(224,168,74,.6); }
#btn-scene-replay.visible { display: inline-flex; }

/* ── GAME ENCOUNTER BUTTON ── */
.encounter-wrap { margin: 1rem .5rem 0; text-align: center; }
.encounter-btn {
  display: inline-flex;
  align-items: center;
  gap: .55rem;
  padding: .75rem 1.8rem;
  background: linear-gradient(135deg, rgba(224,168,74,.15), rgba(224,168,74,.05));
  border: 1px solid rgba(224,168,74,.45);
  border-radius: 50px;
  color: var(--gold2);
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 1.1rem;
  font-weight: 700;
  cursor: pointer;
  text-decoration: none;
  transition: background .25s, border-color .25s, transform .2s;
  letter-spacing: .04em;
}
.encounter-btn:hover {
  background: linear-gradient(135deg, rgba(224,168,74,.28), rgba(224,168,74,.12));
  border-color: var(--gold);
  transform: translateY(-2px);
}
.encounter-btn .enc-icon { font-size: 1.2rem; }
.encounter-btn.disabled { opacity: .38; cursor: not-allowed; pointer-events: none; }
.encounter-title {
  font-family: 'Rajdhani', serif;
  font-size: .78rem;
  letter-spacing: .2em;
  color: var(--gold2);
  opacity: .7;
  margin-bottom: .7rem;
  text-transform: uppercase;
}
.encounter-list { display: flex; flex-wrap: wrap; gap: .6rem; justify-content: center; }
@media (max-width: 600px) {
  .encounter-list { flex-direction: column; align-items: center; }
  .encounter-btn  { width: 100%; justify-content: center; }
}

body::before{
  content:'';
  position:fixed;inset:0;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.025'/%3E%3C/svg%3E");
  pointer-events:none;z-index:0;
}

.btn-archive{
  display:inline-flex;align-items:center;gap:.5rem;
  padding:.7rem 1.8rem;
  background:transparent;
  border:1px solid rgba(232,197,71,0.4);
  border-radius:3px;
  color:var(--gold2);
  font-family:'Rajdhani',sans-serif;
  font-size:1rem;font-weight:600;
  letter-spacing:.1em;
  text-decoration:none;
  cursor:pointer;
  transition:all .2s;
}
.btn-archive:hover{ background:rgba(232,197,71,.1); border-color:var(--gold); color:var(--gold); }

/* ════ ARCHIVE SCREEN ════ */
.arc-hero{
  text-align:center;
  padding:2rem 1rem 1.5rem;
  border-bottom:1px solid var(--border);
  position:relative;
}
.arc-hero::after{
  content:'';position:absolute;top:-80px;left:50%;transform:translateX(-50%);
  width:400px;height:400px;
  background:radial-gradient(ellipse,rgba(232,197,71,0.07) 0%,transparent 70%);
  pointer-events:none;
}
.arc-eyebrow{
  font-family:'Rajdhani',sans-serif;font-size:.68rem;
  letter-spacing:.5em;color:var(--gold);text-transform:uppercase;
  margin-bottom:.8rem;opacity:.8;
}
.arc-title{
  font-family:'Bebas Neue','Rajdhani',sans-serif;
  font-size:clamp(2.4rem,9vw,4.5rem);
  line-height:.9;letter-spacing:.04em;color:#fff;margin-bottom:.4rem;
}
.arc-title span{color:var(--gold);display:block;}
.arc-sub{
  font-family:'Rajdhani',sans-serif;font-size:.85rem;
  letter-spacing:.18em;color:var(--dim);margin-top:.8rem;
}
.arc-count{
  display:inline-flex;align-items:center;gap:.5rem;
  margin-top:1.2rem;padding:.45rem 1.2rem;
  border:1px solid var(--border);border-radius:2px;
  font-family:'Rajdhani',sans-serif;font-size:.72rem;
  letter-spacing:.22em;color:var(--dim);
}
.arc-count b{color:var(--gold);font-size:1.1rem;}

.arc-filter{
  display:flex;align-items:center;justify-content:center;
  gap:.5rem;flex-wrap:wrap;
  padding:.75rem 1rem;
  border-bottom:1px solid var(--border);
  background:rgba(8,10,14,0.85);
}
.arc-filter-label{
  font-family:'Rajdhani',sans-serif;font-size:.68rem;
  letter-spacing:.2em;color:var(--dim);white-space:nowrap;margin-right:.25rem;
}
.arc-filter-btn{
  background:transparent;border:1px solid var(--border);
  color:var(--dim);font-family:'Rajdhani',sans-serif;
  font-size:.68rem;letter-spacing:.15em;
  padding:.3rem .85rem;border-radius:2px;cursor:pointer;
  white-space:nowrap;transition:all .2s;
}
.arc-filter-btn:hover{border-color:rgba(255,255,255,.2);color:var(--cream);}
.arc-filter-btn.active{background:var(--gold);border-color:var(--gold);color:#000;font-weight:700;}

.arc-list{width:100%;margin-bottom:1.5rem;}

.arc-item{
  border:1px solid var(--border);border-radius:4px;
  margin-bottom:.5rem;overflow:hidden;
  transition:border-color .25s;
  opacity:0;transform:translateY(12px);
  animation:arcSlideIn .35s ease forwards;
}
@keyframes arcSlideIn{to{opacity:1;transform:translateY(0);}}
.arc-item:hover{border-color:rgba(255,255,255,.12);}
.arc-item.open{border-color:rgba(232,197,71,.3);}

.arc-item-header{
  display:flex;align-items:center;gap:.9rem;
  padding:1rem 1.2rem;cursor:pointer;
  background:var(--card);transition:background .2s;user-select:none;
}
.arc-item-header:hover{background:#161b26;}
.arc-item.open .arc-item-header{background:#161b26;}

.arc-monster-img{
  flex-shrink:0;width:52px;height:52px;border-radius:4px;
  object-fit:cover;object-position:center top;
  background:#080a0e;
  transition:transform .25s;
  font-size:2rem;display:flex;align-items:center;justify-content:center;
}
.arc-item.open .arc-monster-img,
.arc-item-header:hover .arc-monster-img{transform:scale(1.08);}

.arc-item-info{flex:1;min-width:0;}
.arc-item-name{
  font-family:'Bebas Neue','Rajdhani',sans-serif;
  font-size:1rem;letter-spacing:.06em;color:#fff;line-height:1;
}
.arc-item-name-en{
  font-family:'Rajdhani',sans-serif;font-size:.68rem;
  letter-spacing:.2em;color:var(--dim);margin-top:.15rem;
}
.arc-item-code{
  font-family:'Rajdhani',sans-serif;font-size:.62rem;
  letter-spacing:.25em;color:var(--gold);opacity:.6;margin-top:.25rem;
}
.arc-item-meta{display:flex;align-items:center;gap:.75rem;flex-shrink:0;}
.arc-game-badge{
  font-family:'Rajdhani',sans-serif;font-size:.68rem;
  letter-spacing:.1em;color:var(--dim);white-space:nowrap;
}
.arc-game-badge b{color:var(--gold);}
.arc-chevron{
  width:18px;height:18px;color:var(--dim);
  transition:transform .3s;flex-shrink:0;
}
.arc-item.open .arc-chevron{transform:rotate(180deg);}

.arc-item-body{
  max-height:0;overflow:hidden;
  transition:max-height .4s cubic-bezier(.4,0,.2,1);
  background:var(--bg2);
}
.arc-item-body-inner{
  padding:1rem 1.2rem 1.2rem;
  border-top:1px solid var(--border);
}
.arc-axis-tags{display:flex;flex-wrap:wrap;gap:.4rem;margin-bottom:.9rem;}
.arc-axis-tag{
  font-family:'Rajdhani',sans-serif;font-size:.62rem;
  letter-spacing:.2em;padding:.2rem .6rem;border-radius:2px;border:1px solid;
}
.arc-tag-D{color:#f4a460;border-color:rgba(244,164,96,.3);background:rgba(244,164,96,.06);}
.arc-tag-N{color:#8b9dc3;border-color:rgba(139,157,195,.3);background:rgba(139,157,195,.06);}
.arc-tag-C{color:#f4a7b9;border-color:rgba(244,167,185,.3);background:rgba(244,167,185,.06);}
.arc-tag-S{color:#7ecfcf;border-color:rgba(126,207,207,.3);background:rgba(126,207,207,.06);}
.arc-tag-T{color:#a8d8a8;border-color:rgba(168,216,168,.3);background:rgba(168,216,168,.06);}
.arc-tag-Q{color:#c3a6d4;border-color:rgba(195,166,212,.3);background:rgba(195,166,212,.06);}
.arc-tag-W{color:#e8c547;border-color:rgba(232,197,71,.3);background:rgba(232,197,71,.06);}
.arc-tag-B{color:#ff8c69;border-color:rgba(255,140,105,.3);background:rgba(255,140,105,.06);}

.arc-game-list{display:flex;flex-direction:column;gap:.6rem;}
.arc-game-card{
  display:flex;align-items:center;gap:.65rem;
  padding:.85rem 1rem;background:var(--card);
  border:1px solid var(--border);border-radius:4px;
  text-decoration:none;color:var(--cream);
  transition:all .2s;position:relative;overflow:hidden;
}
.arc-game-card::before{
  content:'';position:absolute;left:0;top:0;bottom:0;width:2px;
  background:var(--gold);transform:scaleY(0);transition:transform .2s;
}
.arc-game-card:hover{background:#161b26;border-color:rgba(232,197,71,.25);transform:translateX(4px);}
.arc-game-card:hover::before{transform:scaleY(1);}
.arc-game-icon{
  flex-shrink:0;width:30px;height:30px;
  background:rgba(232,197,71,.08);border:1px solid rgba(232,197,71,.15);
  border-radius:3px;display:flex;align-items:center;justify-content:center;font-size:.85rem;
}
.arc-game-info{flex:1;min-width:0;}
.arc-game-title{
  font-family:'Rajdhani',sans-serif;font-size:.93rem;font-weight:600;
  letter-spacing:.04em;color:#e8ecf4;line-height:1.2;
  white-space:nowrap;overflow:hidden;text-overflow:ellipsis;
}
.arc-game-note{font-size:.68rem;color:var(--dim);margin-top:.1rem;letter-spacing:.05em;}
.arc-game-arrow{flex-shrink:0;color:var(--dim);font-size:.85rem;transition:color .2s,transform .2s;}
.arc-game-card:hover .arc-game-arrow{color:var(--gold);transform:translateX(3px);}

.arc-empty{
  text-align:center;padding:3rem 1rem;color:var(--dim);
  font-family:'Rajdhani',sans-serif;font-size:.82rem;letter-spacing:.15em;
}
</style>
</head>
<body>
<div class="curtain curtain-l"></div>
<div class="curtain curtain-r"></div>
<div class="scanlines"></div>
<div id="ptcl"></div>
<div id="flash"></div>
<div id="bigflash"></div>
<!-- ✅ 수정 3: 촛불 glow 요소 -->
<div id="candle-glow"></div>

<!-- ✅ 수정 5: crack polyline — stroke-linecap="butt" → 끝을 날카롭게 -->
<svg id="crack-layer" viewBox="0 0 800 600" preserveAspectRatio="xMidYMid slice" xmlns="http://www.w3.org/2000/svg">
  <g class="crack-g1" stroke="rgba(160,20,20,0.85)" stroke-width="1.2" fill="none" stroke-linecap="butt" stroke-linejoin="miter">
    <polyline points="420,0 405,95 440,140 415,200 430,260"/>
    <polyline points="415,200 380,230 360,210"/>
    <polyline points="430,260 460,300 445,340"/>
  </g>
  <g class="crack-g2" stroke="rgba(185,50,15,0.75)" stroke-width="0.9" fill="none" stroke-linecap="butt" stroke-linejoin="miter">
    <polyline points="0,180 80,195 120,175 185,210 210,195"/>
    <polyline points="120,175 100,145 115,120"/>
    <polyline points="800,320 720,305 680,335 620,315"/>
    <polyline points="680,335 660,370 675,400"/>
  </g>
  <g class="crack-g3" stroke="rgba(215,120,15,0.95)" stroke-width="1.5" fill="none" stroke-linecap="butt" stroke-linejoin="miter">
    <polyline points="200,0 195,60 210,100 185,160 220,220 195,290 240,350 210,420"/>
    <polyline points="185,160 150,180 120,160 80,175"/>
    <polyline points="220,220 260,240 285,225"/>
    <polyline points="600,600 615,520 595,470 625,400 600,330"/>
    <polyline points="595,470 560,450 540,460"/>
  </g>
  <radialGradient id="vgn" cx="50%" cy="50%" r="70%">
    <stop offset="30%" stop-color="transparent"/>
    <stop offset="100%" stop-color="rgba(60,10,10,0.45)"/>
  </radialGradient>
  <rect width="800" height="600" fill="url(#vgn)"/>
</svg>

<div id="app">

<!-- ════════ INTRO ════════ -->
<div class="screen active" id="sc-intro">
  <div class="intro-marquee">✦ WORLD HORROR CARNIVAL ✦ EST. UNKNOWN ✦</div>
  <!-- ✅ 수정 1: 둥근 폰트(Jua) + 단색 -->
  <div class="intro-title">나는 어떤 몬스터인가</div>
  <div class="intro-sub">세계 괴담 × 16 Monster Types</div>

  <div class="orn">✦</div>

  <div class="story-box">
    <!-- ✅ 수정 2: story-kw opacity 90% (CSS로 처리) -->
    <span class="story-kw">차가운 바닥</span>에서 정신을 차렸다.<br>
    내가 누구인지, 왜 이곳에 있는지 — <span class="story-kw">기억나지 않는다.</span><br>
    들려오는 건 기괴한 웃음소리와<br>어디선가 타는 듯한 <span class="story-kw">냄새뿐.</span><br><br>
    <span style="font-size:.95rem;color:rgba(255,255,255,0.8)">하지만 본능이 먼저 알고 있을지도 모른다 —<br>내가 어떤 존재인지.</span>
  </div>

  <!-- ✅ 수정 4: 축 항목 텍스트 크기 통일 (모두 .88rem, ax-label 클래스 사용) -->
  <div class="axis-explain" style="margin:0 auto 2rem">
    <div class="ax-item">
      <span class="ax-label">◆ 활동 시간</span><span class="ax-sep">·</span><span>낮형 vs 밤형</span>
    </div>
    <div class="ax-item">
      <span class="ax-label">◆ 외형</span><span class="ax-sep">·</span><span>귀여움 vs 으스스</span>
    </div>
    <div class="ax-item">
      <span class="ax-label">◆ 소통</span><span class="ax-sep">·</span><span>말많음 vs 조용</span>
    </div>
    <div class="ax-item">
      <span class="ax-label">◆ 행동</span><span class="ax-sep">·</span><span>겁쟁이 vs 대담</span>
    </div>
  </div>

  <div style="text-align:center;color:#ffffff;font-size:.9rem;margin-bottom:1.8rem;letter-spacing:.05em">
    12개의 본능적 질문 &nbsp;·&nbsp; 4개의 축 &nbsp;·&nbsp; 16가지 정체
  </div>

  <button class="btn btn-main" onclick="startQuiz()">눈을 뜬다</button>
  <button class="btn btn-archive" onclick="showArchive('intro')" style="margin-top:.9rem">⚔ 게임 아카이브 보기</button>
</div>

<!-- ════════ ARCHIVE ════════ -->
<div class="screen" id="sc-archive">
  <div class="arc-hero">
    <div class="arc-eyebrow">✦ World Monster Database ✦</div>
    <div class="arc-title">MONSTER<span>GAME ARCHIVE</span></div>
    <p class="arc-sub">당신의 본질과 닮은 괴물들이 등장하는 게임 모음</p>
    <div class="arc-count">
      <b>16</b> MONSTERS &nbsp;·&nbsp; <b id="arc-total-games">0</b> GAMES
    </div>
  </div>
  <div class="arc-filter" id="arc-filter">
    <span class="arc-filter-label">FILTER</span>
    <button class="arc-filter-btn active" data-filter="all">ALL</button>
    <button class="arc-filter-btn" data-filter="D">낮</button>
    <button class="arc-filter-btn" data-filter="N">밤</button>
    <button class="arc-filter-btn" data-filter="C">귀여움</button>
    <button class="arc-filter-btn" data-filter="S">으스스</button>
    <button class="arc-filter-btn" data-filter="T">말많음</button>
    <button class="arc-filter-btn" data-filter="Q">조용</button>
    <button class="arc-filter-btn" data-filter="W">겁쟁이</button>
    <button class="arc-filter-btn" data-filter="B">대담</button>
  </div>
  <div class="arc-list" id="arc-list"></div>
  <div class="btn-row" style="margin-top:.5rem;margin-bottom:1.5rem">
    <button class="btn btn-ghost" id="arc-back-btn" onclick="backFromArchive()">← 돌아가기</button>
  </div>
</div>

<!-- ════════ QUIZ ════════ -->
<div class="screen" id="sc-quiz">
  <div class="prog-wrap">
    <div class="prog-meta">
      <span id="q-label" style="font-family:'Rajdhani',sans-serif;font-size:.85rem;letter-spacing:.1em">QUESTION 1 / 12</span>
      <span id="q-axis" style="color:var(--gold)">◆</span>
    </div>
    <div class="prog-track"><div class="prog-fill" id="pfill" style="width:0%"></div></div>
  </div>
  <div style="display:flex;gap:.6rem;justify-content:center;margin-bottom:.8rem;flex-wrap:wrap">
    <button onclick="goBack()" id="btn-back" class="btn" style="padding:.45rem 1.1rem;font-size:.85rem;background:rgba(224,168,74,.1);color:var(--gold2);border:1px solid rgba(224,168,74,.3);display:none">← 이전 질문</button>
    <button id="btn-scene-replay" onclick="replayCurrentScene()">▶ 씬 다시보기</button>
    <button onclick="restartQuiz()" class="btn" style="padding:.45rem 1.1rem;font-size:.85rem;background:rgba(180,60,60,.1);color:#e08080;border:1px solid rgba(180,60,60,.3)">↺ 처음으로</button>
  </div>
  <div class="atrack" id="atrack"></div>
  <div class="card">
    <div class="co tl">✦</div><div class="co tr">✦</div>
    <div class="co bl">✦</div><div class="co br">✦</div>
    <div class="q-scene" id="qscene">— SCENE —</div>
    <div class="q-num"   id="qnum">I</div>
    <div class="q-emoji" id="qemoji" style="display:none"></div>
    <div class="q-img-slot" id="qimgslot"></div>
    <div class="q-situation" id="qsituation" style="display:none"></div>
    <div class="q-text"  id="qtext">로딩 중...</div>
    <div class="choices" id="choices"></div>
  </div>
</div>

<!-- ════════ REVEAL ════════ -->
<div class="screen" id="sc-reveal">
  <div class="reveal-wrap">
    <div class="reveal-title">✦ 깨어나는 중 ✦</div>
    <div class="soul-roulette" id="soul-emoji">✦</div>
    <div class="reveal-msg" id="reveal-msg">당신의 진짜 모습이<br>깨어나고 있습니다</div>
    <div class="reveal-dots">· · ·</div>
  </div>
</div>

<!-- ════════ RESULT ════════ -->
<div class="screen" id="sc-result">
  <div class="intro-marquee">✦ 그들이 본 당신의 진짜 모습이 드러났습니다 ✦</div>

  <div class="flip-wrap" id="flip-wrap" onclick="this.classList.toggle('flipped')">
    <div class="flip-inner">
      <div class="flip-front">
        <div class="result-img-card">
          <div class="co tl">✦</div><div class="co tr">✦</div>
          <div class="result-seal" id="r-emoji"></div>
          <div class="result-origin" id="r-origin" style="margin-top:.9rem">Origin</div>
          <div class="result-name"   id="r-name">이름</div>
          <div class="result-aka"    id="r-aka">별명</div>
          <div class="result-code"   id="r-code"></div>
        </div>
      </div>
      <div class="flip-back">
        <div class="flip-back-content">
          <div class="result-origin" id="r-origin-b" style="margin-top:1rem"></div>
          <div class="flip-back-name" id="r-name-b"></div>
          <div class="result-lore"   id="r-lore-b"></div>
          <div class="flip-back-desc" id="r-desc-b"></div>
          <div class="flip-back-stats" id="r-stats-b"></div>
          <div class="horror-scroll"  id="r-horror-b"></div>
          <div class="compat-box"     id="r-compat-b"></div>
          <div class="encounter-wrap" id="encounter-wrap" style="margin-top:.6rem;width:100%"></div>
        </div>
      </div>
    </div>
  </div>
  <div class="flip-hint">↩ 카드를 눌러 뒤집어보세요</div>

  <div class="btn-row" style="margin-top:1.2rem">
    <button class="btn btn-main" onclick="showAll()">모든 몬스터 보기</button>
    <button class="btn btn-ghost" onclick="restartQuiz()">↺ 다시 테스트</button>
  </div>
  <div style="text-align:center;margin-top:.8rem">
    <button class="btn btn-archive" onclick="showArchive('result')">⚔ 게임 아카이브</button>
  </div>
</div>

<!-- ════════ ALL ════════ -->
<div class="screen" id="sc-all">
  <div class="all-title">MONSTER ARCHIVE</div>
  <div class="all-sub">✦ 16 TYPES ✦</div>
  <div class="all-grid" id="allgrid"></div>
  <button class="btn btn-ghost" onclick="backAll()">← 내 결과로 돌아가기</button>
</div>

</div><!-- /#app -->

<!-- ✅ 수정 6: scene overlay — 닫기 버튼 포함, 클릭 시 애니메이션 정지 -->
<div id="scene-overlay" onclick="closeSceneOverlay()">
  <button id="scene-close-btn" onclick="event.stopPropagation();closeSceneOverlay()">✕</button>
  <img id="scene-img" src="" alt="scene">
</div>

<script>
/* ════════════════════════════════════════
   SCENE IMAGES
════════════════════════════════════════ */
const SCENE_IMGS = {
  img1:  'img1.png',
  img2:  'img2.png',
  img3:  'img3.png',
  img4:  'img4.png',
  img5:  'img5.png',
  img6:  'img6.png',
  img7:  'img7.png',
  img8:  'img8.png',
  img9:  'img9.png',
  img10: 'img10.png',
  img11: 'img11.png',
  img12: 'img12.png',
  img13: 'img13.png',
};

/* ════════════════════════════════════════
   MONSTER IMAGES
════════════════════════════════════════ */
const IMG = {
  DCTW:  'fox.png',
  DCTB:  'Cheshire.png',
  DCQW:  'Mandragora.png',
  DCQB:  'Mimic.png',
  DSTW:  'goblin.png',
  DSTB:  'bugaboo.png',
  DSQW:  'mummy.png',
  DSQB:  'snow.png',
  NCTW:  'pixie.png',
  NCTB:  'gremlin.png',
  NCQW:  'dobby.png',
  NCQB:  'kodama.png',
  NSTW:  'ghost.png',
  NSTB:  'vampire.png',
  NSQW:  'boogeyman.png',
  NSQB:  'Slender.png',
};

const SCENE_MAP = [
  'img1','img2','img3','img4','img5','img6',
  'img7','img8','img9','img10','img11','img12'
];

let _sceneTimer1 = null, _sceneTimer2 = null;
let _sceneTimer3 = null;
let _lastSceneKey = null;
let _pendingCb = null; // 닫기 버튼으로 스킵할 때 실행할 콜백

function replayCurrentScene(){
  if(!_lastSceneKey) return;
  showScene(_lastSceneKey, 2200, ()=>{});
}

function updateSceneReplayBtn(key){
  _lastSceneKey = key;
  const btn = document.getElementById('btn-scene-replay');
  if(btn){
    if(key && SCENE_IMGS[key]) btn.classList.add('visible');
    else btn.classList.remove('visible');
  }
}

/* ✅ 수정 6: closeSceneOverlay — 타이머 정지 + 오버레이 닫기 + 콜백 즉시 실행 */
function closeSceneOverlay(){
  if(_sceneTimer1){ clearTimeout(_sceneTimer1); _sceneTimer1=null; }
  if(_sceneTimer2){ clearTimeout(_sceneTimer2); _sceneTimer2=null; }
  if(_sceneTimer3){ clearTimeout(_sceneTimer3); _sceneTimer3=null; }
  const overlay = document.getElementById('scene-overlay');
  overlay.classList.remove('active');
  // 대기 중인 콜백이 있으면 즉시 실행 (다음 질문으로 넘어가기)
  if(_pendingCb){
    const cb = _pendingCb;
    _pendingCb = null;
    setTimeout(cb, 100);
  }
}

function showScene(imgKey, duration, cb){
  if(_sceneTimer1) clearTimeout(_sceneTimer1);
  if(_sceneTimer2) clearTimeout(_sceneTimer2);
  if(_sceneTimer3) clearTimeout(_sceneTimer3);
  _pendingCb = null;

  const overlay = document.getElementById('scene-overlay');
  const img     = document.getElementById('scene-img');

  if(!imgKey || !SCENE_IMGS[imgKey]){
    overlay.classList.remove('active');
    cb();
    return;
  }

  updateSceneReplayBtn(imgKey);
  overlay.classList.remove('active');
  img.src = SCENE_IMGS[imgKey];
  _pendingCb = cb; // 닫기 버튼 대비 콜백 저장

  _sceneTimer1 = setTimeout(()=>{
    overlay.classList.add('active');
    _sceneTimer2 = setTimeout(()=>{
      overlay.classList.remove('active');
      _pendingCb = null;
      _sceneTimer3 = setTimeout(cb, 600);
    }, duration);
  }, 16);
}

/* ════════════════════════════════════════
   QUESTIONS
════════════════════════════════════════ */
const Q = [
  {axis:'DN', num:'I',   scene:'— 길 앞에서 —', emoji:'🌲', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 16v-2.38C4 11.5 2.97 10.5 3 8c.03-2.72 1.49-6 4.5-6C9.37 2 10 3.8 10 5.5c0 3.11-2 5.66-2 8.68V16a2 2 0 1 1-4 0Z"/><path d="M20 20v-2.38c0-2.12 1.03-3.12 1-5.62-.03-2.72-1.49-6-4.5-6C14.63 6 14 7.8 14 9.5c0 3.11 2 5.66 2 8.68V20a2 2 0 1 0 4 0Z"/><path d="M16 17h4"/><path d="M4 13h4"/></svg>',
   sit:'눈앞에 두 갈래 길이 있다. 한쪽은 따스한 햇볕이 내리쬐는 숲길, 다른 쪽은 달빛조차 들지 않는 깊은 동굴.',
   text:'당신의 발걸음은 본능적으로 어디를 향하는가?',
   axlabel:'◆ 활동 시간', A:{ico:'🌞',txt:'햇볕이 드는 숲길 — 따스함이 당긴다',val:'D'}, B:{ico:'🌑',txt:'어두운 동굴 — 그 깊음이 편하다',val:'N'}},

  {axis:'DN', num:'II',  scene:'— 하루가 끝날 때 —', emoji:'🕯️', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2v2"/><path d="M14.837 16.385a6 6 0 1 1-7.223-7.222c.624-.147.97.66.715 1.248a4 4 0 0 0 5.26 5.259c.589-.255 1.396.09 1.248.715"/><path d="M16 12a4 4 0 0 0-4-4"/><path d="m19 5-1.256 1.256"/><path d="M20 12h2"/></svg>',
   sit:'끝이 보이지 않는 길을 계속 걷다보니 서서히 해가 지기 시작했다. 어둠이 내려앉을수록 당신은 어떤 기분이 드는가?',
   text:'당신이 두려워지는 시간은 언제인가?',
   axlabel:'◆ 활동 시간', A:{ico:'☀️',txt:'낮 — 아무래도 아침에 일어나서 뭘 해야 될지가 가장 두렵다',val:'D'}, B:{ico:'🌙',txt:'밤 — 어둠이 다가오면 왠지 무서워진다',val:'N'}},

  {axis:'DN', num:'III', scene:'— 아이디어가 찾아올 때 —', emoji:'💡', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 18V5"/><path d="M15 13a4.17 4.17 0 0 1-3-4 4.17 4.17 0 0 1-3 4"/><path d="M17.598 6.5A3 3 0 1 0 12 5a3 3 0 1 0-5.598 1.5"/><path d="M17.997 5.125a4 4 0 0 1 2.526 5.77"/><path d="M18 18a4 4 0 0 0 2-7.464"/><path d="M19.967 17.483A4 4 0 1 1 12 18a4 4 0 1 1-7.967-.517"/><path d="M6 18a4 4 0 0 1-2-7.464"/><path d="M6.003 5.125a4 4 0 0 0-2.526 5.77"/></svg>',
   sit:'문득 여기를 빠져나갈 좋은 수가 떠오른다. 기억을 더듬어보면 그 방법은...',
   text:'당신이 위기를 헤쳐나가는 방법은 무엇인가?',
   axlabel:'◆ 활동 시간', A:{ico:'☕',txt:'아침 — 땅을 파고 들어가서 아침까지 숨어있는다',val:'D'}, B:{ico:'🌃',txt:'새벽 — 두 손으로 잡힐 횃불을 만들어서 밤을 헤쳐나간다',val:'N'}},

  {axis:'CS', num:'IV',  scene:'— 첫인상 —', emoji:'🪞', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 7V5a2 2 0 0 1 2-2h2"/><path d="M17 3h2a2 2 0 0 1 2 2v2"/><path d="M21 17v2a2 2 0 0 1-2 2h-2"/><path d="M7 21H5a2 2 0 0 1-2-2v-2"/><path d="M8 14s1.5 2 4 2 4-2 4-2"/><path d="M9 9h.01"/><path d="M15 9h.01"/></svg>',
   sit:'마을을 발견했다. 처음 만난 이들이 당신을 보고 나눈 대화를 우연히 듣게 됐다.',
   text:'그들이 당신을 어떻게 묘사하고 있었는가?',
   axlabel:'◆ 외형', A:{ico:'🌸',txt:'"어, 이 사람 힘들어보여서 도와줘야 할 것 같아"',val:'C'}, B:{ico:'😶',txt:'"혼자서도 잘 헤쳐나갈 것 같아"',val:'S'}},

  {axis:'CS', num:'V',   scene:'— 당신이 화날 때 —', emoji:'🌋', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3"/><path d="M12 9v4"/><path d="M12 17h.01"/></svg>',
   sit:'마을에서 깡패가 당신을 건드렸다. 주변 공기가 변한다. 사람들이 느끼는 건...',
   text:'당신의 분노는 어떤 형태인가?',
   axlabel:'◆ 외형', A:{ico:'🥺',txt:'놀라서 눈물부터 나온다',val:'C'}, B:{ico:'🧊',txt:'아무 말 없이 공기가 얼어붙기 시작한다.',val:'S'}},

  {axis:'CS', num:'VI',  scene:'— 당신이 사는 공간 —', emoji:'🏚️', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M8.62 13.8A2.25 2.25 0 1 1 12 10.836a2.25 2.25 0 1 1 3.38 2.966l-2.626 2.856a.998.998 0 0 1-1.507 0z"/><path d="M3 10a2 2 0 0 1 .709-1.528l7-6a2 2 0 0 1 2.582 0l7 6A2 2 0 0 1 21 10v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/></svg>',
   sit:'깡패를 무사히 쫓아내니 힘이 빠져 기억을 되짚어 본다. 기억을 잃기 전, 나는 어디에서 살았을까?',
   text:'당신이 지금 가고 싶은 공간은?',
   axlabel:'◆ 외형', A:{ico:'🧸',txt:'따뜻하고 아늑한 방 — 인형, 쿠션, 포근한 색',val:'C'}, B:{ico:'🖤',txt:'어둡고 단조로운 방 — 오브제, 식물, 차가운 공기',val:'S'}},

  {axis:'TQ', num:'VII', scene:'— 낯선 이들 속에서 —', emoji:'🎭', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M8.8 20v-4.1l1.9.2a2.3 2.3 0 0 0 2.164-2.1V8.3A5.37 5.37 0 0 0 2 8.25c0 2.8.656 3.054 1 4.55a5.77 5.77 0 0 1 .029 2.758L2 20"/><path d="M19.8 17.8a7.5 7.5 0 0 0 .003-10.603"/><path d="M17 15a3.5 3.5 0 0 0-.025-4.975"/></svg>',
   sit:'생각을 하다 지쳐 잠이 들어버렸다. 일어나니 여관의 방. 내 방문 앞에 모르는 존재들이 모여 있다.',
   text:'당신은 그곳에서 무슨 행동을 할 것인가?',
   axlabel:'◆ 소통', A:{ico:'💬',txt:'어느새 방 밖으로 나가 내가 그들의 중심에서 이야기를 들려주고 있다',val:'T'}, B:{ico:'🎧',txt:'그들의 대화를 듣다가, 헛기침을 해서 그들을 떠나게 한다.',val:'Q'}},

  {axis:'TQ', num:'VIII',scene:'— 감정이 쌓였을 때 —', emoji:'🫀', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M11 6a13 13 0 0 0 8.4-2.8A1 1 0 0 1 21 4v12a1 1 0 0 1-1.6.8A13 13 0 0 0 11 14H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2z"/><path d="M6 14a12 12 0 0 0 2.4 7.2 2 2 0 0 0 3.2-2.4A8 8 0 0 1 10 14"/><path d="M8 6v8"/></svg>',
   sit:'그들이 나를 이름이 알려지지 않은 범죄자로 오해했다. 억울하다.',
   text:'그 감정을 당신은 어떻게 표현하는가?',
   axlabel:'◆ 소통', A:{ico:'🗣️',txt:'그 자리에서 바로 말로 터뜨려야 한다',val:'T'}, B:{ico:'🌀',txt:'속으로 삭이다가 나중에 정리해서 한마디 한다.',val:'Q'}},

  {axis:'TQ', num:'IX',  scene:'— 연락 —', emoji:'📱', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M2.992 16.342a2 2 0 0 1 .094 1.167l-1.065 3.29a1 1 0 0 0 1.236 1.168l3.413-.998a2 2 0 0 1 1.099.092 10 10 0 1 0-4.777-4.719"/><path d="M8 12h.01"/><path d="M12 12h.01"/><path d="M16 12h.01"/></svg>',
   sit:'당신은 결백을 주장하기 위해 사람들에게 알리기 시작했다.',
   text:'당신의 전달 방식은?',
   axlabel:'◆ 소통', A:{ico:'📝',txt:'종이에 장문으로 적어서 사람들에게 쥐어준다',val:'T'}, B:{ico:'👁️',txt:'글을 쓰지 않고 외친다.',val:'Q'}},

  {axis:'WB', num:'X',   scene:'— 발소리 —', emoji:'👣', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 13v1"/><path d="M17 2a1 1 0 0 1 1 1v4a3 3 0 0 1-.6 1.8l-.6.8A4 4 0 0 0 16 12v8a2 2 0 0 1-2 2H10a2 2 0 0 1-2-2v-8a4 4 0 0 0-.8-2.4l-.6-.8A3 3 0 0 1 6 7V3a1 1 0 0 1 1-1z"/><path d="M6 6h12"/></svg>',
   sit:'아직 오해가 풀리지 않은 상황, 뒤에서 기분 나쁜 발소리가 들린다. 점점 가까워지고 있다.',
   text:'당신의 본능은 어떻게 반응하는가?',
   axlabel:'◆ 행동', A:{ico:'🫥',txt:'재빠르게 도망쳐서 숨을 죽이고 숨는다 — 지나가길 기다린다',val:'W'}, B:{ico:'🔦',txt:'길에 떨어진 유리조각을 들고 뒤를 돌아 정체를 확인한다 — 직접 봐야 한다',val:'B'}},

  {axis:'WB', num:'XII', scene:'— 침범 —', emoji:'🌋', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 13c0 5-3.5 7.5-7.66 8.95a1 1 0 0 1-.67-.01C7.5 20.5 4 18 4 13V6a1 1 0 0 1 1-1c2 0 4.5-1.2 6.24-2.72a1.17 1.17 0 0 1 1.52 0C14.51 3.81 17 5 19 5a1 1 0 0 1 1 1z"/><path d="m14.5 9.5-5 5"/><path d="m9.5 9.5 5 5"/></svg>',
   sit:'다행히 지나가는 고양이였다. 하지만 저번에 만든 아지트로 돌아오자 이번에는 누군가 나의 공간을 들어와 헤집어 놓았다.',
   text:'당신은 어떻게 반응하는가?',
   axlabel:'◆ 행동', A:{ico:'😶',txt:'일단 참는다 — 나중에 혼자 분개한다',val:'W'}, B:{ico:'👁️‍🗨️',txt:'그 자리에서 바로 대응한다 — 넘어가지 않는다',val:'B'}},

  {axis:'WB', num:'XI',  scene:'— 분기점 —', emoji:'⚡', img:'<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v18"/><path d="m19 8 3 8a5 5 0 0 1-6 0z"/><path d="M3 7h1a17 17 0 0 0 8-2 17 17 0 0 0 8 2h1"/><path d="m5 8 3 8a5 5 0 0 1-6 0z"/><path d="M7 21h10"/></svg>',
   sit:'결국 마녀로 몰려 큰 결정 앞에 섰다. 되돌릴 수 없는 선택이다.',
   text:'당신은 어떻게 나아가는가?',
   axlabel:'◆ 행동', A:{ico:'😰',txt:'결과를 받아들일 수 없다. — 팔을 뿌리치고 반대 방향으로 달린다',val:'W'}, B:{ico:'🎲',txt:'결과를 받아들일 수 없다. — 자신의 결백을 주장한다',val:'B'}},
];

/* ════ PARTICLES ════ */
const PE=['✦','◆','✶','◇','✸','◈','✦','◆','✶','◇','✸','◈'];
const pw=document.getElementById('ptcl');
for(let i=0;i<20;i++){
  const d=document.createElement('div'); d.className='p';
  d.textContent=PE[i%PE.length];
  d.style.cssText=`left:${Math.random()*100}%;font-size:${.7+Math.random()*.8}rem;animation-duration:${10+Math.random()*14}s;animation-delay:${-Math.random()*12}s`;
  pw.appendChild(d);
}

/* ════ GAME STATE ════ */
let qi=0, sc={D:0,N:0,C:0,S:0,T:0,Q:0,W:0,B:0};
const AXES=[['D','N'],['C','S'],['T','Q'],['W','B']];
const DISPLAY_AXES=[['D','N'],['C','S'],['T','Q'],['W','B']];
const AXIS_LABELS={D:'낮형',N:'밤형',C:'귀여움',S:'으스스',T:'말많음',Q:'조용',W:'겁쟁이',B:'대담'};

/* ✅ 수정 3: 촛불 glow — 마우스 이동 시 glow 위치 추적 */
const candleGlow = document.getElementById('candle-glow');
let glowTimeout;
document.addEventListener('mousemove', (e) => {
  candleGlow.style.left = e.clientX + 'px';
  candleGlow.style.top  = e.clientY + 'px';
  candleGlow.style.opacity = '0.8';
  clearTimeout(glowTimeout);
  glowTimeout = setTimeout(() => { candleGlow.style.opacity = '0'; }, 2000);
});

/* ── crack layer ── */
function applyCrack(qIndex){
  const cl = document.getElementById('crack-layer');
  cl.classList.remove('crack1','crack2','crack3');
  if(qIndex >= 9)       cl.classList.add('crack3');
  else if(qIndex >= 6)  cl.classList.add('crack2');
  else if(qIndex >= 3)  cl.classList.add('crack1');
}

const DARK_STAGES=[
  {q:0, cls:''},
  {q:4, cls:'darkening'},
  {q:8, cls:'darker'},
];

function applyDark(qIndex){
  document.body.classList.remove('darkening','darker');
  for(let i=DARK_STAGES.length-1;i>=0;i--){
    if(qIndex>=DARK_STAGES[i].q && DARK_STAGES[i].cls){
      document.body.classList.add(DARK_STAGES[i].cls);
      break;
    }
  }
  applyCrack(qIndex);
}

function ss(id){
  document.querySelectorAll('.screen').forEach(e=>e.classList.remove('active'));
  const el=document.getElementById(id);
  el.classList.remove('active'); void el.offsetWidth; el.classList.add('active');
  el.scrollIntoView({behavior:'smooth',block:'start'});
}
function flash(){
  const f=document.getElementById('flash');
  f.classList.remove('doflash'); void f.offsetWidth; f.classList.add('doflash');
}
function startQuiz(){
  qi=0; sc={D:0,N:0,C:0,S:0,T:0,Q:0,W:0,B:0};
  history=[];
  document.body.classList.remove('darkening','darker');
  document.getElementById('crack-layer').classList.remove('crack1','crack2','crack3');
  initAtrack(); ss('sc-quiz'); showScene(SCENE_MAP[0], 2200, renderQ);
}

function initAtrack(){
  const el=document.getElementById('atrack'); el.innerHTML='';
  DISPLAY_AXES.forEach(()=>{
    const t=document.createElement('div'); t.className='atag';
    t.textContent='?';
    el.appendChild(t);
  });
}
function renderAtrack(){
  const el=document.getElementById('atrack');
  const tags=el.querySelectorAll('.atag');
  DISPLAY_AXES.forEach(([a,b],i)=>{
    const tot=sc[a]+sc[b];
    const lead=tot===0?null:(sc[a]>=sc[b]?a:b);
    if(tags[i]){
      tags[i].className='atag'+(lead?' on':'');
      tags[i].textContent=lead?AXIS_LABELS[lead]:'?';
    }
  });
}

function renderQ(){
  const q=Q[qi];
  applyDark(qi);
  document.getElementById('q-label').textContent=`QUESTION ${qi+1} / ${Q.length}`;
  document.getElementById('q-axis').textContent=q.axlabel;
  document.getElementById('qscene').textContent=q.scene;
  document.getElementById('qnum').textContent=q.num;
  document.getElementById('qemoji').style.display='none';
  const imgSlot = document.getElementById('qimgslot');
  if(q.img){
    imgSlot.innerHTML = q.img;
    imgSlot.style.display='flex';
  } else {
    imgSlot.innerHTML = '';
    imgSlot.style.display='flex';
  }
  document.getElementById('qtext').textContent=q.text;
  document.getElementById('pfill').style.width=`${(qi/Q.length)*100}%`;

  const sitEl=document.getElementById('qsituation');
  if(q.sit){
    sitEl.textContent=q.sit;
    sitEl.style.display='block';
  } else {
    sitEl.style.display='none';
  }

  const ch=document.getElementById('choices'); ch.innerHTML='';
  [[q.A,'A'],[q.B,'B']].forEach(([c,k],i)=>{
    const btn=document.createElement('button'); btn.className='choice';
    btn.innerHTML=`<span>${c.txt}</span>`;
    btn.style.cssText=`opacity:0;transform:translateX(-14px);transition:opacity .3s ease ${i*.1}s,transform .3s ease ${i*.1}s,background .2s,border-color .2s,padding .2s`;
    btn.onclick=()=>pick(btn,c.val);
    ch.appendChild(btn);
    setTimeout(()=>{btn.style.opacity='1';btn.style.transform='translateX(0)';},60);
  });
}

let history = [];
function pick(btn,val){
  if(document.querySelector('.choice.chosen')) return;
  btn.classList.add('chosen');
  history.push({qi, val, sc: {...sc}});
  sc[val]++; flash(); renderAtrack();
  setTimeout(()=>{
    const choicesEl = document.getElementById('choices');
    if(choicesEl) choicesEl.innerHTML = '';
    qi++;
    updateBackBtn();
    if(qi < Q.length){
      showScene(SCENE_MAP[qi], 2200, renderQ);
    } else {
      showScene('img13', 2600, triggerReveal);
    }
  }, 500);
}
function goBack(){
  if(history.length===0) return;
  const prev = history.pop();
  qi = prev.qi;
  Object.assign(sc, prev.sc);
  renderAtrack();
  updateBackBtn();
  renderQ();
}
function updateBackBtn(){
  const btn = document.getElementById('btn-back');
  if(btn) btn.style.display = history.length>0 ? '' : 'none';
}

let finalCode = null;

function triggerReveal(){
  finalCode = getNearestCode(computeCode());
  ss('sc-reveal');
  document.body.classList.remove('darkening','darker');
  document.getElementById('crack-layer').classList.remove('crack1','crack2','crack3');

  const msgs=[
    '당신의 진짜 모습이<br>깨어나고 있습니다',
    '기억이... 돌아오고 있어요',
    '당신은 처음부터<br>알고 있었던 것 같아요',
    '가면이 벗겨지고 있어요...',
  ];
  let mi=0;
  const msgEl=document.getElementById('reveal-msg');
  const emojiEl=document.getElementById('soul-emoji');
  const monsterKeys=Object.keys(M);

  const roulette=setInterval(()=>{
    const rk=monsterKeys[Math.floor(Math.random()*monsterKeys.length)];
    emojiEl.innerHTML = IMG[rk] ? `<img src="${IMG[rk]}" style="width:120px;height:120px;object-fit:contain;" alt="">` : M[rk].emoji;
  },90);

  const msgInterval=setInterval(()=>{
    mi=(mi+1)%msgs.length;
    msgEl.innerHTML=msgs[mi];
  },900);

  setTimeout(()=>{
    clearInterval(roulette);
    let speed=90, steps=0;
    const slowDown=setInterval(()=>{
      const rk=monsterKeys[Math.floor(Math.random()*monsterKeys.length)];
      emojiEl.innerHTML = IMG[rk] ? `<img src="${IMG[rk]}" style="width:120px;height:120px;object-fit:contain;" alt="">` : M[rk].emoji;
      speed+=40; steps++;
      if(steps>=5){
        clearInterval(slowDown);
        emojiEl.innerHTML = IMG[finalCode] ? `<img src="${IMG[finalCode]}" style="width:140px;height:140px;object-fit:contain;filter:drop-shadow(0 0 20px rgba(201,146,58,.7));" alt="">` : M[finalCode].emoji;
        emojiEl.style.animation='sealIn .7s cubic-bezier(.175,.885,.32,1.275) both';
      }
    },speed);
  },2200);

  setTimeout(()=>{
    const bf=document.getElementById('bigflash');
    bf.style.opacity='1';
    setTimeout(()=>{
      clearInterval(msgInterval);
      showResult();
      setTimeout(()=>{ bf.style.opacity='0'; },200);
    },400);
  },3100);
}

function computeCode(){
  return AXES.map(([a,b])=>{
    if(sc[a]>sc[b]) return a;
    if(sc[b]>sc[a]) return b;
    return Math.random()<.5?a:b;
  }).join('');
}

function getNearestCode(code){
  if(M[code]) return code;
  let best=null,bestDist=999;
  Object.keys(M).forEach(k=>{
    let dist=0;
    for(let i=0;i<k.length;i++) if(k[i]!==code[i]) dist++;
    if(dist<bestDist){bestDist=dist;best=k;}
  });
  return best;
}

function showResult(){
  const fw=document.getElementById('flip-wrap');
  if(fw) fw.classList.remove('flipped');
  document.getElementById('pfill').style.width='100%';
  renderResultData(finalCode, M[finalCode]);
  ss('sc-result');
  window.scrollTo({ top: 0, behavior: 'instant' });
  updateEncounterBtn(finalCode);
}

/* ── GAME URLs ── */
const GAME_URLS = {
  DCTW: [
    { label: '리그 오브 레전드', url: 'https://www.leagueoflegends.com/ko-kr/' },
    { label: '검은사막', url: 'https://www.kr.playblackdesert.com/ko-KR/Intro/tournament2026' },
  ],
  DCTB: [
    { label: 'Alice: Madness Returns', url: 'https://store.steampowered.com/app/19680/Alice_Madness_Returns/' },
    { label: 'BLACK SOULS II', url: 'https://store.steampowered.com/app/3855540/BLACK_SOULS_II/' },
  ],
  DCQW: [
    { label: 'Mandragora: Whispers of the Witch Tree', url: 'https://store.steampowered.com/app/1721060/Mandragora_Whispers_of_the_Witch_Tree/' },
    { label: 'Castlevania Advance Collection', url: 'https://store.steampowered.com/app/1552550/Castlevania_Advance_Collection/' },
  ],
  DCQB: [
    { label: 'BLACK SOULS II', url: 'https://store.steampowered.com/app/3855540/BLACK_SOULS_II/' },
    { label: 'Mimicry', url: 'https://store.steampowered.com/app/1804170/Mimicry/' },
  ],
  DSTW: [
    { label: 'Styx: Shards of Darkness', url: 'https://store.steampowered.com/app/355790/Styx_Shards_of_Darkness/' },
    { label: "Baldur's Gate 3", url: 'https://store.steampowered.com/app/1086940/Baldurs_Gate_3/' },
  ],
  DSTB: [
    { label: "8Doors: Arum's Afterlife Adventure", url: 'https://store.steampowered.com/app/668550/8Doors_Arums_Afterlife_Adventure/' },
    { label: 'DokeV', url: 'https://dokev.pearlabyss.com/ko/Main/Index' },
  ],
  DSQW: [
    { label: '미라 게임', url: 'https://store.steampowered.com/app/582160/_/' },
    { label: 'FOREWARNED', url: 'https://store.steampowered.com/app/1562420/FOREWARNED/' },
  ],
  DSQB: [
    { label: 'FATAL FRAME: Maiden of Black Water', url: 'https://store.steampowered.com/app/1732190/FATAL_FRAME__PROJECT_ZERO_Maiden_of_Black_Water/?l=koreana' },
    { label: 'Ghostwire: Tokyo', url: 'https://store.steampowered.com/app/1475810/Ghostwire_Tokyo/' },
  ],
  NCTW: [
    { label: 'Labyrinthine', url: 'https://store.steampowered.com/app/1302240/Labyrinthine/' },
    { label: 'The Witcher 3: Wild Hunt', url: 'https://store.steampowered.com/app/292030/The_Witcher_3_Wild_Hunt/' },
  ],
  NCTB: [
    { label: 'Gremlins, Inc.', url: 'https://store.steampowered.com/app/369990/Gremlins_Inc/' },
    { label: "Grimmlins' Tale", url: 'https://store.steampowered.com/app/1785520/Grimmlins_Tale/' },
  ],
  NCQW: [
    { label: 'Harry Potter: Hogwarts Mystery', url: 'https://play.google.com/store/apps/details?id=com.tinyco.potter' },
    { label: '호그와트 레거시', url: 'https://store.steampowered.com/app/990080/_/' },
  ],
  NCQB: [
    { label: 'Ghostwire: Tokyo', url: 'https://store.steampowered.com/app/1475810/Ghostwire_Tokyo/' },
    { label: '니오 2 Complete Edition', url: 'https://store.steampowered.com/app/1325200/2_Complete_Edition/' },
  ],
  NSTW: [
    { label: '처녀귀신 게임', url: 'https://store.steampowered.com/app/466130/_/?l=koreana' },
    { label: 'Seven Nights Ghost', url: 'https://store.steampowered.com/app/2382250/Seven_Nights_Ghost/' },
  ],
  NSTB: [
    { label: 'V Rising', url: 'https://store.steampowered.com/app/1604030/V_Rising/' },
    { label: 'Vampyr', url: 'https://store.steampowered.com/app/427290/Vampyr/' },
  ],
  NSQW: [
    { label: 'Boogeyman (VR)', url: 'https://store.steampowered.com/app/412770/Boogeyman/' },
    { label: 'The Boogie Man', url: 'https://store.steampowered.com/app/749840/The_Boogie_Man/' },
  ],
  NSQB: [
    { label: 'Slender: The Arrival', url: 'https://store.steampowered.com/app/252330/Slender_The_Arrival/' },
    { label: "Slender's Woods", url: 'https://slenders-woods.en.softonic.com/' },
  ],
};

function updateEncounterBtn(code) {
  const wrap = document.getElementById('encounter-wrap');
  if (!wrap) return;
  const links = GAME_URLS[code];
  const name  = (M[code] && M[code].name) ? M[code].name : code;
  if (!links || links.length === 0) {
    wrap.innerHTML = `<span class="encounter-btn disabled">⚔️ 게임 준비 중 · 곧 만나요</span>`;
    return;
  }
  const btns = links.map(g =>
    `<a class="encounter-btn" href="${g.url}" onclick="event.stopPropagation(); event.preventDefault(); window.open('${g.url}','_blank','noopener,noreferrer');" rel="noopener">
      <span class="enc-icon">⚔️</span><span>${g.label}</span>
    </a>`
  ).join('');
  wrap.innerHTML = `
    <div class="encounter-title">⚔️ ${name} 게임에서 만나기</div>
    <div class="encounter-list">${btns}</div>
  `;
}

function renderResultData(code,m){
  if(!m){ console.error('Monster not found for code:', code); return; }
  const rEmojiEl = document.getElementById('r-emoji');
  if(IMG[code]) {
    rEmojiEl.innerHTML = `<img src="${IMG[code]}" class="result-monster-img" style="filter:drop-shadow(0 0 40px rgba(201,146,58,.55));" alt="${m.name}">`;
  } else {
    rEmojiEl.textContent = m.emoji;
  }
  function setText(id, val){ const el=document.getElementById(id); if(el) el.textContent=val; }
  function setHTML(id, val){ const el=document.getElementById(id); if(el) el.innerHTML=val; }

  // 앞면
  setText('r-origin', m.origin);
  setText('r-name',   m.name);
  setText('r-aka',    m.aka);

  // 뒷면
  setText('r-origin-b', m.origin);
  setText('r-name-b',   m.name);
  setText('r-lore-b',   m.lore);
  setText('r-desc-b',   m.desc);

  // 코드 뱃지 (앞면)
  const cs=document.getElementById('r-code'); if(cs){ cs.innerHTML='';
  [...code].forEach((l,i)=>{
    const d=document.createElement('div'); d.className='rc';
    d.textContent=l; d.style.animationDelay=`${.1+i*.1}s`;
    cs.appendChild(d);
  }); }

  // 스탯 (뒷면만)
  const sgb=document.getElementById('r-stats-b'); if(sgb) sgb.innerHTML='';
  m.stats.forEach(s=>{
    if(sgb) sgb.innerHTML+=`<div class="flip-back-stat"><div class="flip-back-stat-l">${s.l}</div><div class="flip-back-stat-v">${s.v}</div></div>`;
  });

  setHTML('r-horror-b', `<span class="horror-scroll-title">✦ 어두운 진실 ✦</span>${m.horror}`);
  setHTML('r-compat-b', `<span class="compat-label">✦ 다른 괴물과의 인연 ✦</span>${m.compat}`);
}

let activeTooltip = null;
function removeTooltip(){
  if(activeTooltip){ activeTooltip.remove(); activeTooltip=null; }
}
function showAll(){
  const g=document.getElementById('allgrid'); g.innerHTML='';
  Object.entries(M).forEach(([code,m])=>{
    const isMe = code === finalCode;
    const d=document.createElement('div'); d.className='monster-tile'+(isMe?' me':'');
    d.innerHTML=`
      <div class="tile-emoji">${IMG[code] ? `<img src="${IMG[code]}" style="width:60px;height:60px;object-fit:contain;" alt="${m.name}">` : m.emoji}</div>
      <div class="tile-code">${code}</div>
      <div class="tile-name">${m.name}</div>
      <div style="font-size:.78rem;color:var(--dim);margin-top:.15rem">${m.origin}</div>
      ${isMe?'<div class="tile-me">✦ 나의 정체</div>':''}
    `;
    d.addEventListener('click', (e)=>{
      e.stopPropagation();
      removeTooltip();
      const tt = document.createElement('div');
      tt.className = 'tile-tooltip';
      tt.innerHTML = `<div class="tile-tooltip-name">${m.emoji} ${m.name}</div><div class="tile-tooltip-origin">${m.origin}</div><div class="tile-tooltip-desc">${m.desc}</div>`;
      activeTooltip = tt;
      const rect = d.getBoundingClientRect();
      const tx = Math.min(rect.left, window.innerWidth - 280);
      document.body.appendChild(tt);
      const ttH = tt.offsetHeight;
      const spaceBelow = window.innerHeight - rect.bottom;
      const ty = spaceBelow > ttH + 16
        ? rect.bottom + 8 + window.scrollY
        : rect.top - ttH - 8 + window.scrollY;
      tt.style.left = Math.max(8, tx) + 'px';
      tt.style.top = ty + 'px';
    });
    g.appendChild(d);
  });
  document.addEventListener('click', removeTooltip, {once:false});
  ss('sc-all');
}
function backAll(){ ss('sc-result'); }
/* ════════════════════════════════════════
   ARCHIVE
════════════════════════════════════════ */
const ARC_MONSTERS = [
  { code:'DCTW', name:'구미호',    nameEn:'Gumiho',           axes:['D','C','T','W'] },
  { code:'DCTB', name:'체셔캣',   nameEn:'Cheshire Cat',     axes:['D','C','T','B'] },
  { code:'DCQW', name:'만드라고라',nameEn:'Mandrake',         axes:['D','C','Q','W'] },
  { code:'DCQB', name:'미믹',     nameEn:'Mimic',            axes:['D','C','Q','B'] },
  { code:'DSTW', name:'고블린',   nameEn:'Goblin',           axes:['D','S','T','W'] },
  { code:'DSTB', name:'도깨비',   nameEn:'Dokkaebi',         axes:['D','S','T','B'] },
  { code:'DSQW', name:'미라',     nameEn:'Mummy',            axes:['D','S','Q','W'] },
  { code:'DSQB', name:'설녀',     nameEn:'Yuki-onna',        axes:['D','S','Q','B'] },
  { code:'NCTW', name:'픽시',     nameEn:'Pixie',            axes:['N','C','T','W'] },
  { code:'NCTB', name:'그렘린',   nameEn:'Gremlin',          axes:['N','C','T','B'] },
  { code:'NCQW', name:'도비',     nameEn:'Dobby',            axes:['N','C','Q','W'] },
  { code:'NCQB', name:'코다마',   nameEn:'Kodama',           axes:['N','C','Q','B'] },
  { code:'NSTW', name:'처녀귀신', nameEn:'Cheonyeo Gwishin', axes:['N','S','T','W'] },
  { code:'NSTB', name:'뱀파이어', nameEn:'Vampire',          axes:['N','S','T','B'] },
  { code:'NSQW', name:'부기맨',   nameEn:'Boogeyman',        axes:['N','S','Q','W'] },
  { code:'NSQB', name:'슬렌더맨', nameEn:'Slender Man',      axes:['N','S','Q','B'] },
];

const ARC_GAME_URLS = {
  DCTW: [
    { label:'리그 오브 레전드', note:'PC 온라인', icon:'🎮', url:'https://www.leagueoflegends.com/ko-kr/' },
    { label:'검은사막', note:'PC MMORPG', icon:'⚔️', url:'https://www.kr.playblackdesert.com/ko-KR/Intro/tournament2026' },
  ],
  DCTB: [
    { label:'Alice: Madness Returns', note:'PC · Steam', icon:'🃏', url:'https://store.steampowered.com/app/19680/Alice_Madness_Returns/' },
    { label:'BLACK SOULS II', note:'PC · Steam', icon:'💀', url:'https://store.steampowered.com/app/3855540/BLACK_SOULS_II/' },
  ],
  DCQW: [
    { label:'Mandragora: Whispers of the Witch Tree', note:'다크 판타지 액션 RPG · Steam', icon:'🌿', url:'https://store.steampowered.com/app/1721060/Mandragora_Whispers_of_the_Witch_Tree/' },
    { label:'Castlevania Advance Collection', note:'PC · Steam', icon:'🏰', url:'https://store.steampowered.com/app/1552550/Castlevania_Advance_Collection/' },
  ],
  DCQB: [
    { label:'BLACK SOULS II', note:'PC · Steam', icon:'💀', url:'https://store.steampowered.com/app/3855540/BLACK_SOULS_II/' },
    { label:'Mimicry', note:'PC · Steam', icon:'🎭', url:'https://store.steampowered.com/app/1804170/Mimicry/' },
  ],
  DSTW: [
    { label:'Styx: Shards of Darkness', note:'주인공 · PC · Steam', icon:'🗡️', url:'https://store.steampowered.com/app/355790/Styx_Shards_of_Darkness/' },
    { label:"Baldur's Gate 3", note:'PC · Steam', icon:'🎲', url:'https://store.steampowered.com/app/1086940/Baldurs_Gate_3/' },
  ],
  DSTB: [
    { label:"8Doors: Arum's Afterlife Adventure", note:'인디 · PC · Steam', icon:'🚪', url:'https://store.steampowered.com/app/668550/8Doors_Arums_Afterlife_Adventure/' },
    { label:'DokeV', note:'PC · Pearl Abyss', icon:'✨', url:'https://dokev.pearlabyss.com/ko/Main/Index' },
  ],
  DSQW: [
    { label:'미라 게임', note:'PC · Steam', icon:'🏺', url:'https://store.steampowered.com/app/582160/_/' },
    { label:'FOREWARNED', note:'PC · Steam', icon:'⚠️', url:'https://store.steampowered.com/app/1562420/FOREWARNED/' },
  ],
  DSQB: [
    { label:'FATAL FRAME: Maiden of Black Water', note:'PC · Steam', icon:'📷', url:'https://store.steampowered.com/app/1732190/FATAL_FRAME__PROJECT_ZERO_Maiden_of_Black_Water/?l=koreana' },
    { label:'Ghostwire: Tokyo', note:'PC · Steam', icon:'👻', url:'https://store.steampowered.com/app/1475810/Ghostwire_Tokyo/' },
  ],
  NCTW: [
    { label:'Labyrinthine', note:'PC · Steam', icon:'🌀', url:'https://store.steampowered.com/app/1302240/Labyrinthine/' },
    { label:'The Witcher 3: Wild Hunt', note:'PC · Steam', icon:'🐺', url:'https://store.steampowered.com/app/292030/The_Witcher_3_Wild_Hunt/' },
  ],
  NCTB: [
    { label:'Gremlins, Inc.', note:'전략 보드게임 · Steam', icon:'🎰', url:'https://store.steampowered.com/app/369990/Gremlins_Inc/' },
    { label:"Grimmlins' Tale", note:'최근 출시 · Steam', icon:'🔧', url:'https://store.steampowered.com/app/1785520/Grimmlins_Tale/' },
  ],
  NCQW: [
    { label:'Harry Potter: Hogwarts Mystery', note:'모바일 · Google Play', icon:'🧙', url:'https://play.google.com/store/apps/details?id=com.tinyco.potter' },
    { label:'호그와트 레거시', note:'간접 등장 · Steam', icon:'⚡', url:'https://store.steampowered.com/app/990080/_/' },
  ],
  NCQB: [
    { label:'Ghostwire: Tokyo', note:'수집 · Steam', icon:'🌲', url:'https://store.steampowered.com/app/1475810/Ghostwire_Tokyo/' },
    { label:'니오 2 Complete Edition', note:'PC · Steam', icon:'⛩️', url:'https://store.steampowered.com/app/1325200/2_Complete_Edition/' },
  ],
  NSTW: [
    { label:'처녀귀신 게임', note:'갑툭튀 · Steam', icon:'👘', url:'https://store.steampowered.com/app/466130/_/?l=koreana' },
    { label:'Seven Nights Ghost', note:'데이트 시뮬 · Steam', icon:'🌙', url:'https://store.steampowered.com/app/2382250/Seven_Nights_Ghost/' },
  ],
  NSTB: [
    { label:'V Rising', note:'PC · Steam', icon:'🩸', url:'https://store.steampowered.com/app/1604030/V_Rising/' },
    { label:'Vampyr', note:'PC · Steam', icon:'🦇', url:'https://store.steampowered.com/app/427290/Vampyr/' },
  ],
  NSQW: [
    { label:'Boogeyman', note:'VR 필요 · Steam', icon:'🥽', url:'https://store.steampowered.com/app/412770/Boogeyman/' },
    { label:'The Boogie Man', note:'스토리 · Steam', icon:'📖', url:'https://store.steampowered.com/app/749840/The_Boogie_Man/' },
  ],
  NSQB: [
    { label:'Slender: The Arrival', note:'PC · Steam', icon:'🕴️', url:'https://store.steampowered.com/app/252330/Slender_The_Arrival/' },
    { label:"Slender's Woods", note:'배포 사이트', icon:'🌲', url:'https://slenders-woods.en.softonic.com/' },
  ],
};

const ARC_AXIS_LABELS = {D:'낮',N:'밤',C:'귀여움',S:'으스스',T:'말많음',Q:'조용',W:'겁쟁이',B:'대담'};
const ARC_MONSTER_IMGS = {}; // 이미지 파일명은 나중에 채울 것
// 예: ARC_MONSTER_IMGS['DCTW'] = 'fox.png';

let _arcFilter = 'all';
let _arcOpenItems = new Set();
let _arcFrom = 'intro'; // 어디서 왔는지 ('intro' | 'result')

function showArchive(from){
  _arcFrom = from || 'intro';
  _arcFilter = 'all';
  _arcOpenItems.clear();
  // 필터 버튼 초기화
  document.querySelectorAll('.arc-filter-btn').forEach(b=>{
    b.classList.toggle('active', b.dataset.filter==='all');
  });
  // 돌아가기 버튼 텍스트
  const backBtn = document.getElementById('arc-back-btn');
  if(backBtn) backBtn.textContent = _arcFrom==='result' ? '← 결과로 돌아가기' : '← 테스트로 돌아가기';
  // 총 게임 수
  const total = Object.values(ARC_GAME_URLS).reduce((s,g)=>s+g.length,0);
  const totalEl = document.getElementById('arc-total-games');
  if(totalEl) totalEl.textContent = total;
  arcRender();
  ss('sc-archive');
}

function backFromArchive(){
  if(_arcFrom === 'result') ss('sc-result');
  else ss('sc-intro');
}

function arcRender(){
  const list = document.getElementById('arc-list');
  const filtered = _arcFilter==='all'
    ? ARC_MONSTERS
    : ARC_MONSTERS.filter(m=>m.axes.includes(_arcFilter));

  if(filtered.length===0){
    list.innerHTML='<div class="arc-empty">— 해당하는 몬스터가 없습니다 —</div>';
    return;
  }

  list.innerHTML = filtered.map((m,i)=>{
    const games = ARC_GAME_URLS[m.code]||[];
    const isOpen = _arcOpenItems.has(m.code);
    const imgSrc = ARC_MONSTER_IMGS[m.code] || (IMG && IMG[m.code]) || null;
    const thumbHtml = imgSrc
      ? `<img class="arc-monster-img" src="${imgSrc}" alt="${m.name}" loading="lazy">`
      : `<div class="arc-monster-img" style="font-size:2rem;display:flex;align-items:center;justify-content:center;">${M[m.code]?M[m.code].emoji:''}</div>`;

    const axisTags = m.axes.map(a=>`<span class="arc-axis-tag arc-tag-${a}">${ARC_AXIS_LABELS[a]}</span>`).join('');
    const gameCards = games.map(g=>`
      <a class="arc-game-card" href="${g.url}" target="_blank" rel="noopener" onclick="event.stopPropagation()">
        <div class="arc-game-icon">${g.icon||'🎮'}</div>
        <div class="arc-game-info">
          <div class="arc-game-title">${g.label}</div>
          <div class="arc-game-note">${g.note}</div>
        </div>
        <span class="arc-game-arrow">→</span>
      </a>`).join('');

    return `
      <div class="arc-item${isOpen?' open':''}" style="animation-delay:${i*.04}s" data-arc-code="${m.code}">
        <div class="arc-item-header" onclick="arcToggle('${m.code}')">
          ${thumbHtml}
          <div class="arc-item-info">
            <div class="arc-item-name">${m.name}</div>
            <div class="arc-item-name-en">${m.nameEn}</div>
            <div class="arc-item-code">${m.code}</div>
          </div>
          <div class="arc-item-meta">
            <span class="arc-game-badge"><b>${games.length}</b> GAMES</span>
            <svg class="arc-chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </div>
        </div>
        <div class="arc-item-body" style="max-height:${isOpen?'600px':'0'}">
          <div class="arc-item-body-inner">
            <div class="arc-axis-tags">${axisTags}</div>
            <div class="arc-game-list">${gameCards}</div>
          </div>
        </div>
      </div>`;
  }).join('');

  // 필터된 게임 수 업데이트
  const total = filtered.reduce((s,m)=>s+(ARC_GAME_URLS[m.code]||[]).length,0);
  const totalEl = document.getElementById('arc-total-games');
  if(totalEl) totalEl.textContent = total;
}

function arcToggle(code){
  if(_arcOpenItems.has(code)) _arcOpenItems.delete(code);
  else _arcOpenItems.add(code);
  const item = document.querySelector(`[data-arc-code="${code}"]`);
  if(!item) return;
  const body = item.querySelector('.arc-item-body');
  const isNowOpen = _arcOpenItems.has(code);
  item.classList.toggle('open', isNowOpen);
  body.style.maxHeight = isNowOpen ? '600px' : '0';
}

// 아카이브 필터 이벤트
document.querySelectorAll('.arc-filter-btn').forEach(btn=>{
  btn.addEventListener('click',()=>{
    document.querySelectorAll('.arc-filter-btn').forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    _arcFilter = btn.dataset.filter;
    _arcOpenItems.clear();
    arcRender();
  });
});

function restartQuiz(){
  _lastSceneKey = null;
  const btn = document.getElementById('btn-scene-replay');
  if(btn) btn.classList.remove('visible');
  finalCode = null;
  document.body.classList.remove('darkening','darker');
  document.getElementById('crack-layer').classList.remove('crack1','crack2','crack3');
  const emojiEl=document.getElementById('soul-emoji');
  if(emojiEl){ emojiEl.style.animation=''; }
  flash();
  setTimeout(()=>ss('sc-intro'),300);
}

/* ════════════════════════════════════════
   MONSTER DATA
════════════════════════════════════════ */
const M = {
  DCTW:{
    emoji:'🦊', name:'구미호', origin:'한국 민간설화',
    aka:'"아홉 꼬리를 가진 천년 묵은 여우 요괴"',
    lore:'수백 년을 살아야 인간으로 변신하는 능력을 얻는다. 간(肝)을 먹어 완전한 인간이 되려 한다. 조선시대 문헌 곳곳에 기록되어 있다.',
    desc:'낮에 활발하고 귀여우며 말이 끊이질 않아요. 화술로 모두를 사로잡지만 결정적 순간엔 겁이 나서 슬그머니 물러서죠. 화려함 뒤에 숨겨진 겁쟁이가 진짜 당신이에요.',
    stats:[{l:'활동 시간',v:'낮'},{l:'외형',v:'요염하게 귀여운'},{l:'소통',v:'화술의 달인'},{l:'행동',v:'속은 겁쟁이'}],
    horror:'당신이 처음 만난 사람을 단번에 사로잡는 그 능력 — 의도한 게 아니었더라도, 상대방의 무언가를 조금씩 가져가고 있어요.',
    compat:'✦ 픽시(NCTW)와 낮밤의 쌍둥이 — 둘 다 귀엽고 말많고 겁쟁이지만, 활동 시간이 달라요'
  },
  DCTB:{
    emoji:'😸', name:'체셔캣(Cheshire Cat)', origin:'루이스 캐럴 〈이상한 나라의 앨리스〉',
    aka:'"사라지면서도 웃음만 남기는 수수께끼 고양이"',
    lore:'1865년 출판. 나타났다 사라지며 철학적 모순을 던진다. "우리는 모두 여기서 미쳤어 — 그렇지 않으면 이곳에 있지 않을 거야"라는 말을 남긴다.',
    desc:'낮에 귀엽고 수다스럽지만 대담하게 제 할 말을 다 해요. 사라져도 웃음은 남기죠. 불편한 진실을 웃으며 던지는 것, 그게 당신의 방식이에요.',
    stats:[{l:'활동 시간',v:'낮 (어디서든)'},{l:'외형',v:'귀엽고 신비로운'},{l:'소통',v:'수다스러운 철학자'},{l:'행동',v:'대담하게 직진'}],
    horror:'당신이 웃으며 던진 그 한마디 — 상대방은 며칠 뒤에야 그 의미를 깨달아요.',
    compat:'✦ 그렘린(NCTB)과 낮밤 대담 콤비 — 둘 다 귀엽고 말많고 대담한 같은 유형이에요'
  },
  DCQW:{
    emoji:'🌱', name:'만드라고라(Mandrake)', origin:'유럽 중세 민간전승',
    aka:'"뽑히면 비명을 질러 사람을 죽인다는 인간 형태의 식물 괴물"',
    lore:'중세 약초서에 기록. 뿌리가 사람 형태를 닮았으며 뽑을 때 나는 비명에 닿으면 죽는다고 믿었다. 〈해리포터〉에도 등장한다.',
    desc:'낮에 귀엽고 조용하게 있지만, 건드리면 예상 밖의 반응을 보여요. 평소엔 내성적이고 겁이 많지만 한번 놀라면 주변까지 흔들리죠. 귀여운 외형 뒤의 숨겨진 파장이에요.',
    stats:[{l:'활동 시간',v:'낮 (땅 속)'},{l:'외형',v:'귀엽고 식물 같은'},{l:'소통',v:'조용, 가끔 폭발'},{l:'행동',v:'겁쟁이'}],
    horror:'당신이 조용히 있다가 갑자기 반응할 때 — 주변이 그 파장에 같이 흔들려버려요.',
    compat:'✦ 도비(NCQW)와 귀엽고 조용한 겁쟁이 동류 — 활동 시간만 달라요'
  },
  DCQB:{
    emoji:'📦', name:'미믹(Mimic)', origin:'서양 테이블탑 RPG 괴물',
    aka:'"보물상자로 위장해 모험가를 잡아먹는 괴물"',
    lore:'D&D 몬스터 매뉴얼 초판(1975)부터 등장. 주변 물체와 완벽히 동일한 형태로 변신한다. 근접하기 전까진 일반 상자와 구별 불가능하다.',
    desc:'낮에 귀엽고 조용하게 숨어 있어요. 먼저 다가오는 법 없이 기다리다가, 기회가 오면 대담하게 행동해요. 아무것도 아닌 척하는 게 가장 강력한 전략이에요.',
    stats:[{l:'활동 시간',v:'낮 (어디서든)'},{l:'외형',v:'귀엽게 위장한'},{l:'소통',v:'완전한 침묵'},{l:'행동',v:'대담한 기습'}],
    horror:'당신이 아무것도 아닌 척할 때 — 가장 가까이 다가온 사람이 가장 먼저 알아요.',
    compat:'✦ 코다마(NCQB)와 귀엽고 조용한 대담자 — 활동 시간만 달라요'
  },
  DSTW:{
    emoji:'👺', name:'고블린(Goblin)', origin:'유럽 민간전승',
    aka:'"못생기고 말많고 잔꾀 많은 소형 악귀"',
    lore:'중세 유럽 전역에 기록. 가정에 침입해 물건을 훔치거나 가축을 괴롭힌다. 겁쟁이지만 무리를 지으면 대담해진다. 지하와 숲 속에 산다.',
    desc:'낮에 으스스하지만 말이 어마어마하게 많아요. 허풍과 수다로 상황을 지배하려 하지만 진짜 위기가 오면 슬그머니 사라지죠. 시끄럽지만 도망가는 건 누구보다 빠른 타입이에요.',
    stats:[{l:'활동 시간',v:'낮·지하'},{l:'외형',v:'으스스하고 어수선'},{l:'소통',v:'쉬지 않는 수다'},{l:'행동',v:'허풍쟁이 겁쟁이'}],
    horror:'당신이 말로 상황을 압도할 때 — 아무도 실제로 뭘 결정했는지 모르는 채 끝나요.',
    compat:'✦ 처녀귀신(NSTW)과 으스스하고 말많은 겁쟁이 동류 — 활동 시간만 달라요'
  },
  DSTB:{
    emoji:'🔦', name:'도깨비', origin:'한국 민간설화',
    aka:'"방망이를 든 장난기 많은 한국의 요괴"',
    lore:'나쁜 귀신이 아니라 인간과 어울리기 좋아하는 존재. 씨름을 즐기고 술을 마신다. 도깨비불과 도깨비 방망이 등 기록이 삼국사기부터 등장한다.',
    desc:'낮에 으스스하지만 말이 많고 거리낌이 없어요. 무섭게 생겼는데 오히려 먼저 다가와서 말을 걸죠. 대담하게 치고 나가는 스타일, 상대가 놀라도 개의치 않아요.',
    stats:[{l:'활동 시간',v:'낮 (주로)'},{l:'외형',v:'으스스+익살'},{l:'소통',v:'거침없이 많음'},{l:'행동',v:'대담'}],
    horror:'당신이 웃으며 들이댈 때의 그 에너지 — 상대방은 무섭다가도 어느새 같이 웃고 있어요.',
    compat:'✦ 슬렌더맨(NSQB)과 으스스하고 대담한 동류 — 소통 방식만 달라요'
  },
  DSQW:{
    emoji:'⚱️', name:'미라(Mummy)', origin:'고대 이집트·세계 민간전승',
    aka:'"저주받은 파라오의 붕대를 감은 불사 존재"',
    lore:'고대 이집트 미라 문화에서 비롯. 19세기 영국 소설에서 저주 개념이 강화됐다. 투탕카멘 발굴(1922) 이후 "파라오의 저주" 전설이 전 세계로 퍼졌다.',
    desc:'낮에 으스스하게 조용히 있어요. 겁이 많은데 그게 티가 나서 더 무서운 타입이에요. 사실 그냥 아무것도 건드리지 않으면 아무 일도 안 일어나는데, 사람들이 먼저 겁내죠.',
    stats:[{l:'활동 시간',v:'낮 (무덤·박물관)'},{l:'외형',v:'으스스하게 고요한'},{l:'소통',v:'침묵'},{l:'행동',v:'겁쟁이 (건드리지 마세요)'}],
    horror:'당신이 아무것도 안 하고 있는데 — 주변 사람들이 알아서 경계하고 조심해요.',
    compat:'✦ 부기맨(NSQW)과 으스스하고 조용한 겁쟁이 동류 — 활동 시간만 달라요'
  },
  DSQB:{
    emoji:'❄️', name:'설녀(雪女)', origin:'일본 요괴 민간설화',
    aka:'"눈보라 속에 나타나는 창백한 여인 요괴"',
    lore:'고이즈미 야쿠모의 괴담집 〈괴담(怪談)〉에 기록. 눈 속에서 길 잃은 자의 숨결을 빨아들여 얼려 죽인다. 인간 남성과 결혼해 살기도 한다.',
    desc:'낮에 으스스하고 차갑게 조용해요. 먼저 말 걸지 않지만 원하는 게 생기면 망설임 없이 행동하죠. 차가움은 두려움이 아니라 집중이에요 — 대담하게, 그러나 조용히.',
    stats:[{l:'활동 시간',v:'낮 (눈 오는 날)'},{l:'외형',v:'으스스하게 아름다운'},{l:'소통',v:'필요할 때만'},{l:'행동',v:'대담하게 조용히'}],
    horror:'당신이 아무 말 없이 행동으로 결론을 낼 때 — 상대방은 이미 얼어버린 뒤예요.',
    compat:'✦ 슬렌더맨(NSQB)과 으스스하고 조용한 대담자 — 활동 시간만 달라요'
  },
  NCTW:{
    emoji:'🧚', name:'픽시(Pixie)', origin:'영국 켈트·콘월 민간전승',
    aka:'"숲 속에 사는 장난꾸러기 소인 요정"',
    lore:'콘월·데번 지방에서 전해지는 장난꾸러기 요정. 여행자를 길 잃게 하거나 집안 물건을 숨긴다. 뒤집어 입은 옷이 픽시를 막는다는 속설이 있다.',
    desc:'밤에 귀엽고 수다스럽게 나타나요. 장난치고 싶은 마음은 굴뚝같은데 막상 혼날 것 같으면 겁이 나서 도망가죠. 귀여운 장난 뒤에 숨은 겁쟁이가 진짜 당신이에요.',
    stats:[{l:'활동 시간',v:'밤·숲'},{l:'외형',v:'작고 귀여운'},{l:'소통',v:'쉴 새 없이 많음'},{l:'행동',v:'장난 후 도망'}],
    horror:'당신이 장난치고 도망갈 때 — 상대방이 웃는지 화났는지 확인하러 다시 돌아오는 그 발걸음이에요.',
    compat:'✦ 구미호(DCTW)와 낮밤의 쌍둥이 — 둘 다 귀엽고 말많고 겁쟁이예요'
  },
  NCTB:{
    emoji:'🔧', name:'그렘린(Gremlin)', origin:'영국 공군 도시전설 (2차 대전)',
    aka:'"기계를 고장 내는 말썽꾸러기 요정"',
    lore:'2차 세계대전 RAF 조종사들 사이에서 퍼진 전설. 비행기 오작동을 설명하기 위해 탄생했다. 로알드 달이 1943년 동화화했다.',
    desc:'밤에 귀엽지만 대담하게 뭔가를 건드려요. 말도 많고 이유도 많은데, 결국 하고 싶은 걸 하고야 말죠. 규칙보다 호기심이 항상 앞서는 타입이에요.',
    stats:[{l:'활동 시간',v:'밤·기계 근처'},{l:'외형',v:'귀엽고 이상한'},{l:'소통',v:'수다스럽고 논리적'},{l:'행동',v:'대담한 실험가'}],
    horror:'당신이 "그냥 한번만" 해보자고 할 때 — 그게 대형 사고의 시작이라는 걸 나중에야 알아요.',
    compat:'✦ 체셔캣(DCTB)과 낮밤 대담 콤비 — 둘 다 귀엽고 말많고 대담한 같은 유형이에요'
  },
  NCQW:{
    emoji:'🧦', name:'도비(Dobby)', origin:'J.K. 롤링 〈해리포터〉',
    aka:'"자유를 갈망하는 집요정"',
    lore:'해리포터 시리즈에 등장하는 집요정. 주인에게 복종하지만 자유를 꿈꾼다. 말포이 가문의 노예였다가 양말 한 짝으로 자유를 얻는다.',
    desc:'밤에 귀엽고 조용하게 주변을 돌봐요. 겁이 많아서 먼저 나서지 못하지만 소중한 사람을 위해서라면 몸을 던지는 타입이에요. 조용한 헌신이 진짜 당신이에요.',
    stats:[{l:'활동 시간',v:'밤'},{l:'외형',v:'작고 귀여운'},{l:'소통',v:'조용하지만 진심'},{l:'행동',v:'겁쟁이 (소중한 것엔 달라)'}],
    horror:'당신이 말없이 뒤에서 챙길 때 — 상대방은 나중에야 당신이 얼마나 많이 했는지 알게 돼요.',
    compat:'✦ 만드라고라(DCQW)와 귀엽고 조용한 겁쟁이 동류 — 활동 시간만 달라요'
  },
  NCQB:{
    emoji:'🌲', name:'코다마(木霊)', origin:'일본 민간설화',
    aka:'"나무에 깃드는 조용한 숲의 정령"',
    lore:'일본 전역에서 신성시된 나무 정령. 〈원령공주〉에서 작고 흰 존재로 묘사됐다. 코다마가 깃든 나무를 베면 재앙이 온다고 믿어 신목(神木)으로 표시한다.',
    desc:'밤에 귀엽고 조용하게 있어요. 말 없이 그냥 거기 있는 것만으로도 존재감이 있죠. 필요하다면 대담하게 움직이지만 설명하지 않아요. 침묵 속의 결단이에요.',
    stats:[{l:'활동 시간',v:'밤·숲'},{l:'외형',v:'귀엽고 신성한'},{l:'소통',v:'침묵'},{l:'행동',v:'대담하지만 조용히'}],
    horror:'당신이 아무 말 없이 그냥 거기 있을 때 — 상대방은 무언가 지켜보는 느낌을 받아요.',
    compat:'✦ 미믹(DCQB)과 귀엽고 조용한 대담자 — 활동 시간만 달라요'
  },
  NSTW:{
    emoji:'👘', name:'처녀귀신', origin:'한국 민간설화',
    aka:'"한을 품고 죽은 젊은 여성의 원혼"',
    lore:'억울하게 죽거나 원한이 맺혀 떠나지 못한 귀신. 흰 소복을 입고 긴 머리를 늘어뜨린다. 〈장화홍련전〉 등 조선 문학에 반복적으로 등장한다.',
    desc:'밤에 으스스하게 나타나지만 하고 싶은 말은 많아요. 한 맺힌 이야기를 털어놓고 싶은데 막상 겁이 나서 멈춰요. 그 억눌린 감정이 오래 쌓여서 더 무서운 거예요.',
    stats:[{l:'활동 시간',v:'밤'},{l:'외형',v:'으스스하고 슬픈'},{l:'소통',v:'쌓인 말이 많음'},{l:'행동',v:'겁쟁이'}],
    horror:'당신이 오래된 상처를 꺼낼 때 — 당신은 한을 품은 채 아직 그 자리에 머물러 있어요.',
    compat:'✦ 고블린(DSTW)과 으스스하고 말많은 겁쟁이 동류 — 활동 시간만 달라요'
  },
  NSTB:{
    emoji:'🧛', name:'뱀파이어(Vampire)', origin:'동유럽 슬라브 민간전승',
    aka:'"불사의 흡혈 귀족"',
    lore:'드라큘라의 원형. 브람 스토커 이전부터 발칸반도에 실제 매장 의식이 행해졌다. 은·마늘·십자가·흐르는 물에 약하다고 기록되어 있다.',
    desc:'밤에 으스스하지만 말이 많고 설득력이 있어요. 원하는 게 생기면 대담하게 밀어붙이죠. 무서운데 매력적인 모순 — 그게 당신이에요.',
    stats:[{l:'활동 시간',v:'밤'},{l:'외형',v:'으스스하고 우아한'},{l:'소통',v:'설득력 있는 웅변'},{l:'행동',v:'대담'}],
    horror:'당신이 누군가를 마음에 들어할 때의 그 집착 — 으스스하지만 절대 포기하지 않아요.',
    compat:'✦ 도깨비(DSTB)와 으스스하고 말많고 대담한 동류 — 활동 시간만 달라요'
  },
  NSQW:{
    emoji:'🌿', name:'부기맨(Boogeyman)', origin:'세계 공통 민간전승',
    aka:'"침대 밑이나 옷장 속에 숨어 있는 공포의 존재"',
    lore:'영어권뿐 아니라 전 세계 대부분의 문화에 유사한 존재가 기록되어 있다. 형태가 없거나 불분명하며, 어둠 속에 숨어 있다고 믿어졌다. 아이들을 겁주는 데 쓰였다.',
    desc:'밤에 으스스하게 조용히 숨어 있어요. 사실 본인도 겁이 많아서 들키면 어쩌나 걱정하고 있죠. 아무도 모르는 곳에서 혼자 두려움과 싸우는 타입이에요.',
    stats:[{l:'활동 시간',v:'밤·어둠 속'},{l:'외형',v:'극강의 으스스함'},{l:'소통',v:'완전한 침묵'},{l:'행동',v:'겁쟁이'}],
    horror:'당신이 어둠 속에 조용히 있을 때 — 상대방은 당신이 거기 있는지도 모르면서 무서워해요.',
    compat:'✦ 미라(DSQW)와 으스스하고 조용한 겁쟁이 동류 — 활동 시간만 달라요'
  },
  NSQB:{
    emoji:'🕴️', name:'슬렌더맨(Slender Man)', origin:'현대 인터넷 도시전설',
    aka:'"숲속에 나타나는 팔이 긴 정장 차림의 키 큰 존재"',
    lore:'2009년 Something Awful 포럼에서 탄생했지만 전 세계로 퍼져 실제 사건까지 일으킨 현대 괴담의 상징. 목격담이 축적되며 실제 민간전설처럼 진화했다.',
    desc:'밤에 으스스하고 조용해요. 겁 같은 건 없고, 그냥 있고 싶은 곳에 있어요. 말 없이 나타나고 말 없이 사라지죠. 가장 조용하고 가장 대담한 존재예요.',
    stats:[{l:'활동 시간',v:'밤·숲·학교'},{l:'외형',v:'극강의 으스스함'},{l:'소통',v:'완전한 침묵'},{l:'행동',v:'대담'}],
    horror:'당신이 멀리서 조용히 지켜보고만 있을 때 — 상대방은 이미 당신을 의식하기 시작했어요.',
    compat:'✦ 설녀(DSQB)와 으스스하고 조용한 대담자 — 활동 시간만 달라요'
  }
};
</script>
</body>
</html>
