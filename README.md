# sw-final
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FinStudy Pro | 금융 & 학업 관리 플랫폼</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#07091200;
  --bg2:#0C1020;
  --card:#10141E;
  --inp:#080C18;
  --br:#1A2035;
  --br2:#232B48;
  --blue:#4F7EF7;
  --bdim:rgba(79,126,247,.12);
  --grn:#22C55E;
  --gdim:rgba(34,197,94,.1);
  --red:#EF4444;
  --rdim:rgba(239,68,68,.1);
  --amb:#F59E0B;
  --tx:#E2E9F8;
  --td:#8892B0;
  --tf:#3A4560;
  --r:10px;
  --rs:6px;
}
html,body{height:100%;background:#070B18}
body{color:var(--tx);font-family:'Inter',-apple-system,sans-serif;font-size:14px;line-height:1.5}
::-webkit-scrollbar{width:4px;height:4px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--br2);border-radius:4px}
/* ---------- ATOMS ---------- */
.mono{font-family:'JetBrains Mono',monospace}
.up{color:var(--grn)}.dn{color:var(--red)}.bl{color:var(--blue)}.am{color:var(--amb)}
.dim{color:var(--td)}.fnt{color:var(--tf)}
.sm{font-size:12px}.xs{font-size:11px}.lg{font-size:16px}
.med{font-weight:500}.sem{font-weight:600}.bold{font-weight:700}
.flex{display:flex}.col{flex-direction:column}.items{align-items:center}
.between{justify-content:space-between}.center{justify-content:center}
.g1{gap:4px}.g2{gap:8px}.g3{gap:12px}.g4{gap:16px}
.f1{flex:1}.wrap{flex-wrap:wrap}.shrink0{flex-shrink:0}
.ml-a{margin-left:auto}
.w-full{width:100%}.block{display:block}
/* ---------- CARD / INPUT / BTN ---------- */
.card{background:var(--card);border:1px solid var(--br);border-radius:var(--r)}
.inp{width:100%;background:var(--inp);border:1px solid var(--br2);border-radius:var(--rs);
  color:var(--tx);padding:10px 14px;font-size:14px;font-family:inherit;outline:none;transition:border-color .15s}
.inp:focus{border-color:var(--blue)}
.inp::placeholder{color:var(--tf)}
select.inp{cursor:pointer}
.lbl{display:block;font-size:11px;font-weight:600;color:var(--td);
  margin-bottom:5px;text-transform:uppercase;letter-spacing:.05em}
.fg{margin-bottom:14px}
.ferr{font-size:12px;color:var(--red);margin-top:4px;display:none}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;
  padding:9px 16px;border-radius:var(--rs);font-size:14px;font-weight:500;
  cursor:pointer;border:none;transition:opacity .15s,transform .1s;font-family:inherit;white-space:nowrap}
.btn:active{transform:scale(.98)}
.btn-p{background:var(--blue);color:#fff}
.btn-p:hover{opacity:.9}
.btn-g{background:transparent;color:var(--td);border:1px solid var(--br2)}
.btn-g:hover{background:var(--br);color:var(--tx)}
.btn-d{background:var(--rdim);color:var(--red);border:1px solid rgba(239,68,68,.2)}
.btn-sm{padding:5px 10px;font-size:12px}
.btn-ico{padding:6px 9px}
.btn-full{width:100%}
/* ---------- SECTIONS ---------- */
.sec{display:none}
.sec.on{display:flex;flex-direction:column;min-height:100vh}
/* ---------- LOADING ---------- */
#ld{position:fixed;inset:0;background:#070B18;display:flex;flex-direction:column;
  align-items:center;justify-content:center;z-index:9999;gap:14px}
.spin{width:28px;height:28px;border:2px solid var(--br2);border-top-color:var(--blue);
  border-radius:50%;animation:spin .8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.logo-mk{width:52px;height:52px;background:var(--bdim);border:1px solid rgba(79,126,247,.3);
  border-radius:14px;display:flex;align-items:center;justify-content:center;
  font-size:22px;font-weight:700;color:var(--blue);font-family:'JetBrains Mono',monospace}
/* ---------- AUTH ---------- */
#sec-auth{align-items:center;justify-content:center;position:relative;overflow:hidden;
  background:radial-gradient(ellipse at 30% 20%,rgba(79,126,247,.06) 0%,transparent 60%),
  radial-gradient(ellipse at 70% 80%,rgba(34,197,94,.04) 0%,transparent 60%),#070B18}
#sec-auth::before{content:'';position:absolute;inset:0;
  background-image:linear-gradient(rgba(79,126,247,.03) 1px,transparent 1px),
    linear-gradient(90deg,rgba(79,126,247,.03) 1px,transparent 1px);
  background-size:48px 48px}
.auth-card{width:440px;max-width:95vw;background:var(--card);border:1px solid var(--br2);
  border-radius:16px;padding:32px;position:relative;z-index:1;
  box-shadow:0 24px 64px rgba(0,0,0,.5);animation:fup .4s ease}
.auth-tabs{display:flex;background:var(--inp);border-radius:var(--rs);padding:3px;margin-bottom:22px}
.atab{flex:1;padding:7px;text-align:center;font-size:13px;font-weight:500;border-radius:4px;
  cursor:pointer;color:var(--td);transition:all .15s;border:none;background:transparent}
.atab.on{background:var(--card);color:var(--tx);box-shadow:0 1px 4px rgba(0,0,0,.3)}
/* ---------- ONBOARDING ---------- */
#sec-ob{align-items:center;justify-content:center;padding:40px 20px;background:#070B18}
.ob-card{width:580px;max-width:95vw;background:var(--card);border:1px solid var(--br2);
  border-radius:16px;padding:32px;animation:fup .4s ease}
.steps{display:flex;gap:6px;margin-bottom:26px}
.sdot{width:8px;height:8px;border-radius:50%;background:var(--br2);transition:all .3s}
.sdot.on{background:var(--blue);width:20px;border-radius:4px}
.sdot.done{background:var(--grn)}
.pgrid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin:14px 0}
.popt{border:2px solid var(--br);border-radius:var(--r);padding:16px;cursor:pointer;
  transition:all .15s;text-align:center}
.popt:hover{border-color:rgba(79,126,247,.4)}
.popt.sel{border-color:var(--blue);background:var(--bdim)}
.popt .ico{font-size:28px;margin-bottom:8px}
.atags{display:flex;flex-wrap:wrap;gap:8px;margin:14px 0}
.atag{padding:6px 14px;border:1.5px solid var(--br2);border-radius:20px;font-size:13px;
  cursor:pointer;transition:all .15s;color:var(--td)}
.atag:hover{border-color:rgba(79,126,247,.4)}
.atag.sel{border-color:var(--blue);background:var(--bdim);color:var(--blue)}
/* ---------- APP LAYOUT ---------- */
#sec-app{flex-direction:row}
.sidebar{width:220px;flex-shrink:0;background:var(--bg2);border-right:1px solid var(--br);
  display:flex;flex-direction:column;height:100vh;position:sticky;top:0}
.sb-logo{padding:18px 16px;border-bottom:1px solid var(--br);display:flex;align-items:center;gap:10px}
.sb-nav{padding:10px 8px;flex:1}
.snl{font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:.08em;
  color:var(--tf);padding:4px 8px 8px}
.ni{display:flex;align-items:center;gap:10px;padding:9px 10px;border-radius:var(--rs);
  cursor:pointer;color:var(--td);transition:all .15s;font-size:13.5px;font-weight:500;
  margin-bottom:2px;user-select:none}
.ni:hover{background:rgba(255,255,255,.05);color:var(--tx)}
.ni.on{background:var(--bdim);color:var(--blue)}
.ni-icon{width:18px;text-align:center;font-size:15px;flex-shrink:0}
.sb-foot{border-top:1px solid var(--br);padding:12px}
.uchip{display:flex;align-items:center;gap:10px;padding:8px;border-radius:var(--rs)}
.uav{width:32px;height:32px;border-radius:50%;background:var(--bdim);
  border:1px solid rgba(79,126,247,.3);display:flex;align-items:center;justify-content:center;
  font-size:13px;font-weight:600;color:var(--blue);flex-shrink:0}
.main-wrap{flex:1;display:flex;flex-direction:column;overflow:auto;min-width:0}
.topbar{height:56px;border-bottom:1px solid var(--br);display:flex;align-items:center;
  padding:0 24px;gap:16px;background:var(--bg2);position:sticky;top:0;z-index:50;flex-shrink:0}
.tkstrip{display:flex;gap:10px;margin-left:auto;overflow:hidden}
.tki{display:flex;align-items:center;gap:7px;padding:4px 10px;border-radius:6px;
  background:var(--inp);border:1px solid var(--br);min-width:0}
.tkn{font-size:10px;font-weight:700;color:var(--td);letter-spacing:.03em}
.tkp{font-size:12px;font-weight:500;font-family:'JetBrains Mono',monospace}
.tkc{font-size:10px;font-family:'JetBrains Mono',monospace}
.content{padding:22px;flex:1;overflow:auto}
/* ---------- VIEWS ---------- */
.view{display:none}.view.on{display:block}
/* ---------- MARKET CARDS ---------- */
.mrow{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:18px}
.mc{background:var(--card);border:1px solid var(--br);border-radius:var(--r);
  padding:14px 16px;cursor:pointer;transition:border-color .15s}
.mc:hover{border-color:rgba(79,126,247,.4)}
.mc.on{border-color:var(--blue);background:var(--bdim)}
.mc-lbl{font-size:11px;font-weight:600;text-transform:uppercase;letter-spacing:.05em;
  color:var(--td);margin-bottom:6px}
.mc-px{font-size:19px;font-weight:700;font-family:'JetBrains Mono',monospace}
.mc-ch{font-size:12px;font-family:'JetBrains Mono',monospace;margin-top:3px}
/* ---------- DASHBOARD GRID ---------- */
.dgrid{display:grid;grid-template-columns:1fr 370px;gap:18px}
.chart-sec{}
.chdr{display:flex;align-items:center;justify-content:space-between;padding:16px 20px;
  border-bottom:1px solid var(--br)}
.ibadges{display:flex;gap:7px}
.ib{font-size:11px;padding:2px 8px;border-radius:4px;font-family:'JetBrains Mono',monospace}
.ib.ma20{background:rgba(168,85,247,.15);color:#A855F7}
.ib.ma60{background:rgba(245,158,11,.15);color:var(--amb)}
.ib.rsi{background:rgba(79,126,247,.15);color:var(--blue)}
.cc{padding:14px 14px 6px;height:276px;position:relative}
.rc-lbl{font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:.08em;
  color:var(--tf);padding:8px 16px 0}
.rc{padding:4px 14px 14px;height:96px;position:relative;border-top:1px solid var(--br)}
/* ---------- PORTFOLIO ---------- */
.pf-hdr{display:flex;align-items:center;justify-content:space-between;padding:14px 18px;
  border-bottom:1px solid var(--br)}
.pf-sum{padding:14px 18px;border-bottom:1px solid var(--br)}
.pnl-g{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.pnl-c{background:var(--inp);border:1px solid var(--br);border-radius:var(--rs);padding:10px 12px}
.pnl-l{font-size:10px;text-transform:uppercase;letter-spacing:.06em;color:var(--tf);margin-bottom:3px}
.pnl-v{font-size:17px;font-weight:700;font-family:'JetBrains Mono',monospace}
.pf-list{max-height:200px;overflow-y:auto}
.hr{display:flex;align-items:center;padding:9px 14px;border-bottom:1px solid var(--br);gap:8px;
  transition:background .1s}
.hr:hover{background:rgba(255,255,255,.02)}
.h-sym{width:52px;font-size:12px;font-weight:700;font-family:'JetBrains Mono',monospace;color:var(--blue);flex-shrink:0}
.h-inf{flex:1;min-width:0}
.h-nm{font-size:12px;color:var(--td)}
.h-qty{font-size:11px;color:var(--tf);font-family:'JetBrains Mono',monospace}
.h-pnl{text-align:right;flex-shrink:0}
.h-val{font-size:13px;font-weight:600;font-family:'JetBrains Mono',monospace}
.h-pct{font-size:11px;font-family:'JetBrains Mono',monospace}
.add-pf{padding:14px 18px;border-top:1px solid var(--br)}
.add-g{display:grid;grid-template-columns:2fr 1fr 1fr;gap:8px;margin-bottom:8px}
/* ---------- TASKS ---------- */
.th{margin-bottom:18px}
.th-top{display:flex;align-items:center;gap:12px;margin-bottom:14px}
.pgbar{height:5px;background:var(--br);border-radius:3px;overflow:hidden}
.pgfill{height:100%;background:linear-gradient(90deg,var(--blue),var(--grn));
  border-radius:3px;transition:width .5s ease}
.pginfo{display:flex;justify-content:space-between;margin-bottom:4px}
.kboard{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;align-items:start}
.kcol{background:var(--card);border:1px solid var(--br);border-radius:var(--r);
  min-height:460px;display:flex;flex-direction:column;transition:border-color .2s}
.kcol.dov{border-color:rgba(79,126,247,.5);background:rgba(79,126,247,.03)}
.kch{display:flex;align-items:center;justify-content:space-between;padding:13px 16px;
  border-bottom:1px solid var(--br)}
.kct{display:flex;align-items:center;gap:8px;font-size:13px;font-weight:600}
.kdot{width:8px;height:8px;border-radius:50%}
.cct{font-size:11px;padding:2px 7px;background:var(--inp);border-radius:10px;color:var(--td);
  font-family:'JetBrains Mono',monospace}
.kcards{padding:8px;flex:1;min-height:60px;display:flex;flex-direction:column;gap:8px}
.tc{background:var(--inp);border:1px solid var(--br2);border-radius:var(--rs);padding:12px;
  cursor:grab;transition:box-shadow .15s,border-color .15s,opacity .15s;user-select:none}
.tc:hover{border-color:rgba(79,126,247,.35);box-shadow:0 4px 12px rgba(0,0,0,.3)}
.tc.dragging{opacity:.35;cursor:grabbing}
.tc-hdr{display:flex;align-items:flex-start;justify-content:space-between;gap:6px;margin-bottom:8px}
.tc-ttl{font-size:13px;font-weight:500;line-height:1.4;flex:1}
.tc-del{font-size:15px;color:var(--tf);cursor:pointer;padding:0 2px;line-height:1;
  opacity:0;transition:opacity .15s;border:none;background:none;flex-shrink:0}
.tc:hover .tc-del{opacity:1}
.tc-del:hover{color:var(--red)}
.tc-meta{display:flex;align-items:center;gap:5px;flex-wrap:wrap}
.tbdg{font-size:10px;padding:2px 7px;border-radius:4px;font-weight:600}
.bh{background:var(--rdim);color:var(--red)}
.bm{background:rgba(245,158,11,.12);color:var(--amb)}
.bl2{background:var(--gdim);color:var(--grn)}
.bcat{background:var(--bdim);color:var(--blue)}
.tdue{font-size:11px;color:var(--tf);display:flex;align-items:center;gap:3px;margin-top:6px}
.tdue.ov{color:var(--red)}
.mv-btn{display:flex;gap:4px;margin-top:8px}
/* ---------- MODAL ---------- */
.moverlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.65);z-index:100;
  align-items:center;justify-content:center}
.moverlay.on{display:flex}
.modal{background:var(--card);border:1px solid var(--br2);border-radius:14px;
  padding:24px;width:480px;max-width:95vw;animation:fup .25s ease}
.mhdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px}
.mcls{background:none;border:none;color:var(--td);font-size:22px;cursor:pointer;line-height:1;padding:2px}
.mcls:hover{color:var(--tx)}
.mfoot{display:flex;gap:8px;justify-content:flex-end;margin-top:18px}
/* ---------- EMPTY STATE ---------- */
.empty{display:flex;flex-direction:column;align-items:center;justify-content:center;
  padding:28px;color:var(--tf);text-align:center}
.empty .ei{font-size:28px;margin-bottom:6px;opacity:.5}
.empty .et{font-size:13px}
/* ---------- TOAST ---------- */
#toast{position:fixed;bottom:22px;right:22px;background:var(--card);border:1px solid var(--br2);
  border-radius:var(--rs);padding:9px 16px;font-size:13px;display:none;z-index:9999;
  box-shadow:0 8px 24px rgba(0,0,0,.4)}
/* ---------- ANIMATIONS ---------- */
@keyframes fup{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.fa{animation:fup .25s ease}
/* ---------- RESPONSIVE ---------- */
@media(max-width:1200px){.dgrid{grid-template-columns:1fr}.mrow{grid-template-columns:repeat(2,1fr)}}
@media(max-width:900px){.kboard{grid-template-columns:1fr}.sidebar{display:none}}
@media(max-width:620px){.mrow{grid-template-columns:1fr 1fr}.tkstrip{display:none}.content{padding:14px}.add-g{grid-template-columns:1fr 1fr}}
</style>
</head>
<body>
 
<!-- Loading -->
<div id="ld">
  <div class="logo-mk">FS</div>
  <div class="spin"></div>
  <p class="dim sm">초기화 중...</p>
</div>
 
<!-- Toast -->
<div id="toast"></div>
 
<!-- Task Modal -->
<div class="moverlay" id="task-modal">
  <div class="modal">
    <div class="mhdr">
      <h2 style="font-size:16px;font-weight:600">새 태스크 추가</h2>
      <button class="mcls" onclick="closeModal()">×</button>
    </div>
    <div class="fg">
      <label class="lbl">카테고리</label>
      <select class="inp" id="t-cat">
        <option value="기말고사">📚 기말고사</option>
        <option value="팀 프로젝트">👥 팀 프로젝트</option>
        <option value="과제">📝 과제</option>
        <option value="투자 리서치">📈 투자 리서치</option>
        <option value="기타">🔖 기타</option>
      </select>
    </div>
    <div class="fg">
      <label class="lbl">태스크 제목</label>
      <input type="text" class="inp" id="t-ttl" placeholder="예: 1강 PPT 요약, 레퍼런스 수집">
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px">
      <div class="fg">
        <label class="lbl">마감 기한</label>
        <input type="date" class="inp" id="t-due">
      </div>
      <div class="fg">
        <label class="lbl">우선순위</label>
        <select class="inp" id="t-pri">
          <option value="high">🔴 높음</option>
          <option value="mid" selected>🟡 중간</option>
          <option value="low">🟢 낮음</option>
        </select>
      </div>
    </div>
    <div class="mfoot">
      <button class="btn btn-g" onclick="closeModal()">취소</button>
      <button class="btn btn-p" onclick="submitTask()">추가하기</button>
    </div>
  </div>
</div>
 
<!-- ===== AUTH ===== -->
<div class="sec" id="sec-auth">
  <div class="auth-card">
    <div class="flex items g3" style="margin-bottom:26px">
      <div class="logo-mk">FS</div>
      <div>
        <div style="font-size:18px;font-weight:700">FinStudy Pro</div>
        <div class="sm dim">금융 & 학업 관리 플랫폼</div>
      </div>
    </div>
    <div class="auth-tabs">
      <button class="atab on" id="at-login" onclick="swTab('login')">로그인</button>
      <button class="atab" id="at-reg" onclick="swTab('reg')">회원가입</button>
    </div>
    <!-- Login -->
    <div id="f-login">
      <div class="fg"><label class="lbl">이메일</label>
        <input type="email" class="inp" id="l-em" placeholder="name@example.com"></div>
      <div class="fg"><label class="lbl">비밀번호</label>
        <input type="password" class="inp" id="l-pw" placeholder="••••••••">
        <div class="ferr" id="l-err">이메일 또는 비밀번호가 올바르지 않습니다.</div></div>
      <button class="btn btn-p btn-full" onclick="doLogin()" style="margin-top:4px">로그인</button>
      <button class="btn btn-g btn-full" onclick="demoLogin()" style="margin-top:8px">🎮 데모로 체험하기</button>
      <p class="sm dim" style="text-align:center;margin-top:14px">
        계정이 없으신가요? <a href="#" onclick="swTab('reg')" style="color:var(--blue)">회원가입</a></p>
    </div>
    <!-- Register -->
    <div id="f-reg" style="display:none">
      <div class="fg"><label class="lbl">이름</label>
        <input type="text" class="inp" id="r-nm" placeholder="홍길동"></div>
      <div class="fg"><label class="lbl">이메일</label>
        <input type="email" class="inp" id="r-em" placeholder="name@example.com"></div>
      <div class="fg"><label class="lbl">비밀번호 (영문+숫자+특수문자 8자 이상)</label>
        <input type="password" class="inp" id="r-pw" placeholder="Ex@mple1!">
        <div class="ferr" id="r-err"></div></div>
      <div class="fg"><label class="lbl">비밀번호 확인</label>
        <input type="password" class="inp" id="r-cf" placeholder="비밀번호 재입력"></div>
      <button class="btn btn-p btn-full" onclick="doReg()" style="margin-top:4px">회원가입</button>
    </div>
  </div>
</div>
 
<!-- ===== ONBOARDING ===== -->
<div class="sec" id="sec-ob">
  <div class="ob-card">
    <div class="steps">
      <div class="sdot on" id="sd0"></div>
      <div class="sdot" id="sd1"></div>
    </div>
    <div id="ob0">
      <h2 style="font-size:17px;margin-bottom:5px">투자 성향을 선택하세요</h2>
      <p class="sm dim" style="margin-bottom:16px">맞춤형 대시보드 구성을 위해 알려주세요</p>
      <div class="pgrid">
        <div class="popt" onclick="selRisk('stable')" id="r-stable">
          <div class="ico">🛡️</div>
          <div style="font-weight:600;margin-bottom:3px">안정형</div>
          <div class="sm dim">원금 보존 최우선<br>낮은 리스크 선호</div>
        </div>
        <div class="popt" onclick="selRisk('agg')" id="r-agg">
          <div class="ico">🚀</div>
          <div style="font-weight:600;margin-bottom:3px">공격투자형</div>
          <div class="sm dim">고수익 추구<br>리스크 감수 가능</div>
        </div>
      </div>
      <div style="text-align:right;margin-top:14px">
        <button class="btn btn-p" onclick="ob1()" id="ob0-next" disabled>다음 →</button>
      </div>
    </div>
    <div id="ob1" style="display:none">
      <h2 style="font-size:17px;margin-bottom:5px">관심 자산을 선택하세요</h2>
      <p class="sm dim" style="margin-bottom:12px">중복 선택 가능 · 나중에 변경 가능</p>
      <div class="atags">
        <div class="atag" onclick="togAsset(this)" data-a="국내주식">🇰🇷 국내주식</div>
        <div class="atag" onclick="togAsset(this)" data-a="해외주식">🌎 해외주식</div>
        <div class="atag" onclick="togAsset(this)" data-a="레버리지 ETP">⚡ 레버리지 ETP</div>
        <div class="atag" onclick="togAsset(this)" data-a="암호화폐">₿ 암호화폐</div>
        <div class="atag" onclick="togAsset(this)" data-a="채권/ETF">📊 채권/ETF</div>
        <div class="atag" onclick="togAsset(this)" data-a="선물/파생">🔮 선물/파생</div>
      </div>
      <div class="flex between" style="margin-top:18px">
        <button class="btn btn-g" onclick="ob0()">← 이전</button>
        <button class="btn btn-p" onclick="finOb()">시작하기 🚀</button>
      </div>
    </div>
  </div>
</div>
 
<!-- ===== MAIN APP ===== -->
<div class="sec" id="sec-app">
 
  <!-- Sidebar -->
  <div class="sidebar">
    <div class="sb-logo">
      <div class="logo-mk" style="width:38px;height:38px;font-size:16px;border-radius:10px">FS</div>
      <div style="font-size:14px;font-weight:700">FinStudy Pro</div>
    </div>
    <nav class="sb-nav">
      <div class="snl">메인</div>
      <div class="ni on" id="ni-db" onclick="swView('db')">
        <span class="ni-icon">📈</span><span>금융 대시보드</span>
      </div>
      <div class="ni" id="ni-tk" onclick="swView('tk')">
        <span class="ni-icon">📋</span><span>학업 태스크</span>
      </div>
      <div class="snl" style="margin-top:14px">포트폴리오</div>
      <div id="sb-pf" style="padding:4px 8px"></div>
    </nav>
    <div class="sb-foot">
      <div class="uchip">
        <div class="uav" id="uav">?</div>
        <div class="f1" style="min-width:0">
          <div style="font-size:13px;font-weight:500;overflow:hidden;text-overflow:ellipsis;white-space:nowrap" id="u-nm">-</div>
          <div class="xs dim" id="u-risk">-</div>
        </div>
        <button class="btn btn-g btn-sm btn-ico" onclick="doLogout()" title="로그아웃">↩</button>
      </div>
    </div>
  </div>
 
  <!-- Main content -->
  <div class="main-wrap">
    <div class="topbar">
      <div>
        <div style="font-size:15px;font-weight:600" id="vt">금융 대시보드</div>
        <div class="xs dim" id="vs">실시간 시장 데이터 · 모의 투자</div>
      </div>
      <div class="tkstrip" id="hdr-tk"></div>
    </div>
 
    <div class="content">
 
      <!-- DASHBOARD VIEW -->
      <div class="view on" id="v-db">
        <div class="mrow" id="m-cards"></div>
        <div class="dgrid">
          <!-- Chart -->
          <div class="card chart-sec">
            <div class="chdr">
              <div>
                <div style="font-size:15px;font-weight:600" id="ch-name">Bitcoin (BTC)</div>
                <div class="flex items g2" style="margin-top:3px">
                  <span class="mono bold" style="font-size:22px" id="ch-px">$0</span>
                  <span class="mono sm" id="ch-ch">+0.00%</span>
                </div>
              </div>
              <div class="ibadges">
                <span class="ib ma20">MA20</span>
                <span class="ib ma60">MA60</span>
                <span class="ib rsi">RSI14</span>
              </div>
            </div>
            <div class="cc"><canvas id="pxChart"></canvas></div>
            <div class="rc-lbl">RSI (14) — 과매수:70↑ 과매도:30↓</div>
            <div class="rc"><canvas id="rsiChart"></canvas></div>
          </div>
          <!-- Portfolio -->
          <div class="card" style="overflow:hidden">
            <div class="pf-hdr">
              <h3 style="font-size:14px;font-weight:600">📦 모의 포트폴리오</h3>
              <button class="btn btn-g btn-sm" onclick="showPfForm()">+ 추가</button>
            </div>
            <div class="pf-sum">
              <div class="pnl-g">
                <div class="pnl-c"><div class="pnl-l">평가금액</div><div class="pnl-v" id="pf-val">$0</div></div>
                <div class="pnl-c"><div class="pnl-l">손익 P&L</div><div class="pnl-v" id="pf-pnl">$0</div></div>
              </div>
            </div>
            <div class="pf-list" id="pf-list">
              <div class="empty"><div class="ei">📊</div><div class="et">자산을 추가해 수익률을 추적하세요</div></div>
            </div>
            <div class="add-pf" id="add-pf" style="display:none">
              <h3 style="font-size:13px;font-weight:600;margin-bottom:10px">자산 추가</h3>
              <div class="add-g">
                <div><label class="lbl">자산</label>
                  <select class="inp" id="h-ast">
                    <option value="BTC">BTC — Bitcoin</option>
                    <option value="ETH">ETH — Ethereum</option>
                    <option value="KOSPI">KOSPI — 코스피</option>
                    <option value="SP500">SPX — S&P 500</option>
                    <option value="TQQQ">TQQQ — Lev ETF</option>
                    <option value="SOXL">SOXL — Lev ETF</option>
                  </select></div>
                <div><label class="lbl">매수가</label>
                  <input type="number" class="inp" id="h-px" placeholder="0"></div>
                <div><label class="lbl">수량</label>
                  <input type="number" class="inp" id="h-qty" placeholder="0"></div>
              </div>
              <div class="flex g2" style="justify-content:flex-end">
                <button class="btn btn-g btn-sm" onclick="hidePfForm()">취소</button>
                <button class="btn btn-p btn-sm" onclick="addHolding()">추가</button>
              </div>
            </div>
          </div>
        </div>
      </div>
 
      <!-- TASKS VIEW -->
      <div class="view" id="v-tk">
        <div class="th">
          <div class="th-top">
            <div class="f1">
              <h2 style="font-size:17px">📋 학업 & 프로젝트 관리</h2>
              <p class="sm dim" style="margin-top:2px">칸반 보드로 학습 진행 현황을 추적하세요</p>
            </div>
            <button class="btn btn-p" onclick="openModal()">+ 태스크 추가</button>
          </div>
          <div class="pginfo">
            <span class="sm">전체 진행률</span>
            <span class="sm dim" id="pg-txt">0 / 0 완료</span>
          </div>
          <div class="pgbar"><div class="pgfill" id="pgfill" style="width:0%"></div></div>
        </div>
        <div class="kboard" id="kboard">
          <div class="kcol" id="col-todo" ondragover="dov(event)" ondrop="dop(event,'todo')" ondragleave="dlv(event)">
            <div class="kch">
              <div class="kct"><span class="kdot" style="background:#94A3B8"></span>할 일</div>
              <span class="cct" id="cnt-todo">0</span>
            </div>
            <div class="kcards" id="cards-todo"></div>
          </div>
          <div class="kcol" id="col-inp" ondragover="dov(event)" ondrop="dop(event,'inp')" ondragleave="dlv(event)">
            <div class="kch">
              <div class="kct"><span class="kdot" style="background:#4F7EF7"></span>진행 중</div>
              <span class="cct" id="cnt-inp">0</span>
            </div>
            <div class="kcards" id="cards-inp"></div>
          </div>
          <div class="kcol" id="col-done" ondragover="dov(event)" ondrop="dop(event,'done')" ondragleave="dlv(event)">
            <div class="kch">
              <div class="kct"><span class="kdot" style="background:#22C55E"></span>완료</div>
              <span class="cct" id="cnt-done">0</span>
            </div>
            <div class="kcards" id="cards-done"></div>
          </div>
        </div>
      </div>
 
    </div>
  </div>
</div>
 
<script>
// =============================================
// STATE
// =============================================
const A = {
  user:null, pref:{risk:null,assets:[]}, view:'db',
  assets:{
    BTC:  {name:'Bitcoin',  sym:'BTC',  unit:'$',  base:67200, vol:.018, px:[], type:'crypto'},
    ETH:  {name:'Ethereum', sym:'ETH',  unit:'$',  base:3480,  vol:.022, px:[], type:'crypto'},
    KOSPI:{name:'KOSPI',    sym:'KOSPI',unit:'',   base:2680,  vol:.008, px:[], type:'index'},
    SP500:{name:'S&P 500',  sym:'SPX',  unit:'',   base:5310,  vol:.007, px:[], type:'index'},
    TQQQ: {name:'TQQQ',     sym:'TQQQ', unit:'$',  base:68.5,  vol:.028, px:[], type:'etf'},
    SOXL: {name:'SOXL',     sym:'SOXL', unit:'$',  base:44.2,  vol:.032, px:[], type:'etf'},
  },
  sel:'BTC', pf:[], tasks:[], pxCh:null, rsiCh:null, drag:null, iv:null
};
 
// =============================================
// STORAGE
// =============================================
const sv=(k,v)=>{try{localStorage.setItem('fsp_'+k,JSON.stringify(v))}catch(e){}};
const ld=(k,d=null)=>{try{const v=localStorage.getItem('fsp_'+k);return v!==null?JSON.parse(v):d}catch(e){return d}};
 
// =============================================
// HELPERS
// =============================================
function showSec(id){document.querySelectorAll('.sec').forEach(s=>s.classList.remove('on'));document.getElementById(id).classList.add('on')}
function toast(msg,ms=2600){const t=document.getElementById('toast');t.textContent=msg;t.style.display='block';clearTimeout(t._t);t._t=setTimeout(()=>t.style.display='none',ms)}
function fmt(n,d=2){if(n===null||n===undefined||isNaN(n))return'—';return n.toLocaleString('en-US',{minimumFractionDigits:d,maximumFractionDigits:d})}
function fmtPx(k,p){const a=A.assets[k];const u=a?.unit||'';if(Math.abs(p)>=10000)return u+fmt(p,0);if(Math.abs(p)>=100)return u+fmt(p,1);return u+fmt(p,2)}
function fmtCh(p){return(p>=0?'+':'')+p.toFixed(2)+'%'}
function colOf(v){return v>=0?'var(--grn)':'var(--red)'}
function esc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;')}
 
// =============================================
// AUTH
// =============================================
function swTab(t){
  ['login','reg'].forEach(n=>{
    document.getElementById('at-'+n).classList.toggle('on',n===t);
    document.getElementById('f-'+n).style.display=n===t?'block':'none';
  });
  ['l-err','r-err'].forEach(id=>{const e=document.getElementById(id);if(e)e.style.display='none'});
}
 
function doLogin(){
  const em=document.getElementById('l-em').value.trim();
  const pw=document.getElementById('l-pw').value;
  const err=document.getElementById('l-err');
  if(!em||!pw){err.textContent='이메일과 비밀번호를 입력하세요.';err.style.display='block';return}
  const users=ld('users',{});
  const u=users[em];
  if(!u||u.pw!==btoa(pw)){err.textContent='이메일 또는 비밀번호가 올바르지 않습니다.';err.style.display='block';return}
  err.style.display='none';
  loginUser(u);
}
 
function doReg(){
  const nm=document.getElementById('r-nm').value.trim();
  const em=document.getElementById('r-em').value.trim();
  const pw=document.getElementById('r-pw').value;
  const cf=document.getElementById('r-cf').value;
  const err=document.getElementById('r-err');
  const emRx=/^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  const pwRx=/^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&^]).{8,}$/;
  if(!nm){err.textContent='이름을 입력하세요.';err.style.display='block';return}
  if(!emRx.test(em)){err.textContent='유효한 이메일을 입력하세요.';err.style.display='block';return}
  if(!pwRx.test(pw)){err.textContent='비밀번호: 영문+숫자+특수문자(@$!%*#?&^) 포함 8자 이상';err.style.display='block';return}
  if(pw!==cf){err.textContent='비밀번호가 일치하지 않습니다.';err.style.display='block';return}
  const users=ld('users',{});
  if(users[em]){err.textContent='이미 가입된 이메일입니다.';err.style.display='block';return}
  const u={name:nm,email:em,pw:btoa(pw),ob:false};
  users[em]=u;sv('users',users);
  err.style.display='none';
  loginUser(u);
}
 
function loginUser(u){
  A.user=u;sv('session',u.email);
  A.tasks=ld('tasks_'+u.email,[]);
  A.pf=ld('pf_'+u.email,[]);
  if(!u.ob){showSec('sec-ob')}
  else{A.pref=ld('pref_'+u.email,{risk:'agg',assets:[]});startApp()}
}
 
function doLogout(){
  clearInterval(A.iv);A.user=null;A.pxCh=null;A.rsiCh=null;
  sv('session',null);showSec('sec-auth');
  document.getElementById('l-em').value='';document.getElementById('l-pw').value='';
}
 
// =============================================
// DEMO LOGIN
// =============================================
function demoLogin(){
  const TODAY=new Date().toISOString().split('T')[0];
  const d7=new Date();d7.setDate(d7.getDate()+7);const d7s=d7.toISOString().split('T')[0];
  const d14=new Date();d14.setDate(d14.getDate()+14);const d14s=d14.toISOString().split('T')[0];
  const d3=new Date();d3.setDate(d3.getDate()+3);const d3s=d3.toISOString().split('T')[0];
  const past=new Date();past.setDate(past.getDate()-2);const pasts=past.toISOString().split('T')[0];
 
  const users=ld('users',{});
  const DEMO_EMAIL='demo@finstudy.pro';
  if(!users[DEMO_EMAIL]){
    users[DEMO_EMAIL]={name:'데모 유저',email:DEMO_EMAIL,pw:btoa('Demo123!@'),ob:true};
    sv('users',users);
  }
  sv('pref_'+DEMO_EMAIL,{risk:'agg',assets:['암호화폐','레버리지 ETP','해외주식']});
  sv('pf_'+DEMO_EMAIL,[
    {id:1001,asset:'BTC',name:'Bitcoin',buyPx:52000,qty:0.5},
    {id:1002,asset:'ETH',name:'Ethereum',buyPx:2200,qty:3},
    {id:1003,asset:'TQQQ',name:'TQQQ',buyPx:55,qty:10},
  ]);
  sv('tasks_'+DEMO_EMAIL,[
    {id:2001,title:'기말고사 핵심 개념 정리',cat:'기말고사',due:d7s,pri:'high',st:'inp'},
    {id:2002,title:'팀 프로젝트 레퍼런스 수집',cat:'팀 프로젝트',due:d3s,pri:'high',st:'done'},
    {id:2003,title:'1강 PPT 요약 노트',cat:'과제',due:d14s,pri:'mid',st:'todo'},
    {id:2004,title:'BTC Stoch RSI 전략 백테스트',cat:'투자 리서치',due:d7s,pri:'mid',st:'todo'},
    {id:2005,title:'팀 미팅 발표 자료 준비',cat:'팀 프로젝트',due:pasts,pri:'high',st:'done'},
    {id:2006,title:'소논문 초안 작성',cat:'과제',due:d14s,pri:'low',st:'todo'},
  ]);
  loginUser(users[DEMO_EMAIL]);
}
 
// =============================================
// ONBOARDING
// =============================================
let obStep=0;
function selRisk(t){
  A.pref.risk=t;
  document.getElementById('r-stable').classList.toggle('sel',t==='stable');
  document.getElementById('r-agg').classList.toggle('sel',t==='agg');
  document.getElementById('ob0-next').disabled=false;
}
function togAsset(el){
  const a=el.dataset.a;el.classList.toggle('sel');
  if(el.classList.contains('sel')){if(!A.pref.assets.includes(a))A.pref.assets.push(a)}
  else{A.pref.assets=A.pref.assets.filter(x=>x!==a)}
}
function ob1(){
  document.getElementById('ob0').style.display='none';
  document.getElementById('ob1').style.display='block';
  document.getElementById('sd0').classList.remove('on');document.getElementById('sd0').classList.add('done');
  document.getElementById('sd1').classList.add('on');obStep=1;
}
function ob0(){
  document.getElementById('ob1').style.display='none';
  document.getElementById('ob0').style.display='block';
  document.getElementById('sd1').classList.remove('on');
  document.getElementById('sd0').classList.remove('done');document.getElementById('sd0').classList.add('on');obStep=0;
}
function finOb(){
  if(!A.pref.assets.length){toast('⚠️ 관심 자산을 1개 이상 선택하세요.');return}
  const users=ld('users',{});users[A.user.email].ob=true;sv('users',users);
  sv('pref_'+A.user.email,A.pref);startApp();
}
 
// =============================================
// MARKET DATA
// =============================================
function genPx(base,n,vol){
  const px=[base];
  for(let i=1;i<n;i++){
    const t=(Math.random()-.485)*vol;
    px.push(Math.max(px[i-1]*(1+t),base*.4));
  }
  return px;
}
 
function initMkt(){
  const N=65;
  for(const[k,a]of Object.entries(A.assets)){
    a.px=genPx(a.base,N,a.vol);
    a.cur=a.px[a.px.length-1];
    a.chg=(a.cur/a.px[0]-1)*100;
  }
}
 
function tickMkt(){
  for(const[k,a]of Object.entries(A.assets)){
    const t=(Math.random()-.487)*a.vol*.6;
    a.cur=Math.max(a.cur*(1+t),a.base*.3);
    a.px.push(a.cur);
    if(a.px.length>90)a.px.shift();
    a.chg=(a.cur/a.px[0]-1)*100;
  }
  renderMktCards();renderHdrTk();updChartData();renderPf();renderSbPf();
}
 
function getLabels(n){
  const L=[];const now=new Date();
  for(let i=n-1;i>=0;i--){const d=new Date(now);d.setDate(d.getDate()-i);L.push(`${d.getMonth()+1}/${d.getDate()}`)}
  return L;
}
 
// =============================================
// TECHNICAL INDICATORS
// =============================================
function calcMA(px,p){
  return px.map((_,i)=>{
    if(i<p-1)return null;
    return px.slice(i-p+1,i+1).reduce((a,b)=>a+b,0)/p;
  });
}
 
function calcRSI(px,p=14){
  if(px.length<p+1)return px.map(()=>50);
  const rsi=new Array(p).fill(null);
  const g=[],l=[];
  for(let i=1;i<px.length;i++){const d=px[i]-px[i-1];g.push(d>0?d:0);l.push(d<0?Math.abs(d):0)}
  let ag=g.slice(0,p).reduce((a,b)=>a+b,0)/p;
  let al=l.slice(0,p).reduce((a,b)=>a+b,0)/p;
  rsi.push(al===0?100:100-100/(1+ag/al));
  for(let i=p;i<g.length;i++){
    ag=(ag*(p-1)+g[i])/p;al=(al*(p-1)+l[i])/p;
    rsi.push(al===0?100:100-100/(1+ag/al));
  }
  return rsi;
}
 
// =============================================
// CHARTS
// =============================================
const CD={
  responsive:true,maintainAspectRatio:false,
  animation:{duration:200},
  plugins:{legend:{display:false},tooltip:{
    mode:'index',intersect:false,
    backgroundColor:'rgba(16,20,30,.95)',borderColor:'#1A2035',borderWidth:1,
    titleColor:'#8892B0',bodyColor:'#E2E9F8',padding:10,
    titleFont:{family:"'JetBrains Mono',monospace",size:11},
    bodyFont:{family:"'JetBrains Mono',monospace",size:12}
  }},
  scales:{
    x:{grid:{color:'rgba(255,255,255,.04)'},border:{color:'rgba(255,255,255,.06)'},
      ticks:{color:'#3A4560',font:{size:10,family:"'JetBrains Mono',monospace"},maxTicksLimit:8}},
    y:{grid:{color:'rgba(255,255,255,.04)'},border:{color:'rgba(255,255,255,.06)'},
      ticks:{color:'#3A4560',font:{size:10,family:"'JetBrains Mono',monospace"},maxTicksLimit:6}}
  }
};
 
function initCharts(){
  if(A.pxCh)A.pxCh.destroy();
  if(A.rsiCh)A.rsiCh.destroy();
  const a=A.assets[A.sel];
  const px=a.px;const L=getLabels(px.length);
  const ma20=calcMA(px,20);const ma60=calcMA(px,60);const rsi=calcRSI(px);
  const c1=document.getElementById('pxChart').getContext('2d');
  const gr=c1.createLinearGradient(0,0,0,260);
  gr.addColorStop(0,'rgba(79,126,247,.16)');gr.addColorStop(1,'rgba(79,126,247,0)');
  A.pxCh=new Chart(c1,{
    type:'line',
    data:{labels:L,datasets:[
      {label:'Price',data:px,borderColor:'#4F7EF7',borderWidth:2,fill:true,backgroundColor:gr,pointRadius:0,tension:.3},
      {label:'MA20', data:ma20,borderColor:'#A855F7',borderWidth:1.5,borderDash:[5,4],fill:false,pointRadius:0,tension:.3},
      {label:'MA60', data:ma60,borderColor:'#F59E0B',borderWidth:1.5,borderDash:[5,4],fill:false,pointRadius:0,tension:.3},
    ]},
    options:{...CD,scales:{...CD.scales,y:{...CD.scales.y,ticks:{...CD.scales.y.ticks,
      callback:(v)=>{const u=A.assets[A.sel].unit;if(v>=1000)return u+(v/1000).toFixed(1)+'k';return u+v.toFixed(0)}
    }}}}
  });
  const c2=document.getElementById('rsiChart').getContext('2d');
  const RSIzonePlugin={id:'rz',afterDraw(ch){
    const{ctx,chartArea:{left,right,top,bottom},scales:{y}}=ch;
    const ob=y.getPixelForValue(70);const os=y.getPixelForValue(30);
    ctx.save();
    ctx.fillStyle='rgba(239,68,68,.06)';ctx.fillRect(left,top,right-left,ob-top);
    ctx.fillStyle='rgba(34,197,94,.06)';ctx.fillRect(left,os,right-left,bottom-os);
    ctx.strokeStyle='rgba(239,68,68,.28)';ctx.lineWidth=1;ctx.setLineDash([5,4]);
    ctx.beginPath();ctx.moveTo(left,ob);ctx.lineTo(right,ob);ctx.stroke();
    ctx.strokeStyle='rgba(34,197,94,.28)';
    ctx.beginPath();ctx.moveTo(left,os);ctx.lineTo(right,os);ctx.stroke();
    ctx.restore();
  }};
  A.rsiCh=new Chart(c2,{
    type:'line',
    data:{labels:L,datasets:[{label:'RSI',data:rsi,borderColor:'#4F7EF7',borderWidth:1.5,fill:false,pointRadius:0,tension:.3}]},
    options:{...CD,plugins:{...CD.plugins},scales:{
      x:{...CD.scales.x,display:false},
      y:{...CD.scales.y,min:0,max:100,ticks:{...CD.scales.y.ticks,maxTicksLimit:4}}
    }},
    plugins:[RSIzonePlugin]
  });
  updChartHdr();
}
 
function updChartData(){
  if(!A.pxCh||!A.rsiCh)return;
  const a=A.assets[A.sel];const px=a.px;const L=getLabels(px.length);
  const ma20=calcMA(px,20);const ma60=calcMA(px,60);const rsi=calcRSI(px);
  A.pxCh.data.labels=L;A.pxCh.data.datasets[0].data=px;
  A.pxCh.data.datasets[1].data=ma20;A.pxCh.data.datasets[2].data=ma60;
  A.rsiCh.data.labels=L;A.rsiCh.data.datasets[0].data=rsi;
  A.pxCh.update('none');A.rsiCh.update('none');updChartHdr();
}
 
function updChartHdr(){
  const a=A.assets[A.sel];
  document.getElementById('ch-name').textContent=`${a.name} (${a.sym})`;
  document.getElementById('ch-px').textContent=fmtPx(A.sel,a.cur);
  const chEl=document.getElementById('ch-ch');
  chEl.textContent=fmtCh(a.chg);chEl.style.color=colOf(a.chg);
}
 
// =============================================
// MARKET UI
// =============================================
function renderMktCards(){
  const el=document.getElementById('m-cards');
  const keys=['BTC','ETH','KOSPI','SP500'];
  el.innerHTML=keys.map(k=>{
    const a=A.assets[k];const up=a.chg>=0;
    return`<div class="mc${k===A.sel?' on':''}" data-k="${k}" onclick="selAsset('${k}')">
      <div class="mc-lbl">${a.name}</div>
      <div class="mc-px">${fmtPx(k,a.cur)}</div>
      <div class="mc-ch" style="color:${colOf(a.chg)}">${fmtCh(a.chg)}</div>
    </div>`;
  }).join('');
}
 
function renderHdrTk(){
  const el=document.getElementById('hdr-tk');
  const keys=['BTC','ETH','KOSPI','SP500'];
  el.innerHTML=keys.map(k=>{
    const a=A.assets[k];return`<div class="tki">
      <span class="tkn">${a.sym}</span>
      <span class="tkp" style="color:${colOf(a.chg)}">${fmtPx(k,a.cur)}</span>
      <span class="tkc" style="color:${colOf(a.chg)}">${fmtCh(a.chg)}</span>
    </div>`;
  }).join('');
}
 
function selAsset(k){
  A.sel=k;
  document.querySelectorAll('.mc').forEach(c=>c.classList.toggle('on',c.dataset.k===k));
  updChartData();
}
 
// =============================================
// PORTFOLIO
// =============================================
function showPfForm(){document.getElementById('add-pf').style.display='block'}
function hidePfForm(){
  document.getElementById('add-pf').style.display='none';
  document.getElementById('h-px').value='';document.getElementById('h-qty').value='';
}
function addHolding(){
  const ast=document.getElementById('h-ast').value;
  const px=parseFloat(document.getElementById('h-px').value);
  const qty=parseFloat(document.getElementById('h-qty').value);
  if(!px||!qty||px<=0||qty<=0){toast('⚠️ 매수가와 수량을 입력하세요.');return}
  A.pf.push({id:Date.now(),asset:ast,name:A.assets[ast].name,buyPx:px,qty});
  sv('pf_'+A.user.email,A.pf);hidePfForm();renderPf();toast('✅ 포트폴리오에 추가되었습니다.');
}
function rmHolding(id){
  A.pf=A.pf.filter(h=>h.id!==id);sv('pf_'+A.user.email,A.pf);renderPf();
}
function renderPf(){
  const el=document.getElementById('pf-list');
  if(!A.pf.length){
    el.innerHTML='<div class="empty"><div class="ei">📊</div><div class="et">자산을 추가해 수익률을 추적하세요</div></div>';
    document.getElementById('pf-val').textContent='$0';document.getElementById('pf-pnl').textContent='$0';
    document.getElementById('pf-pnl').style.color='';return;
  }
  let tv=0,tc=0;
  el.innerHTML=A.pf.map(h=>{
    const a=A.assets[h.asset];if(!a)return'';
    const val=a.cur*h.qty;const cost=h.buyPx*h.qty;
    const pnl=val-cost;const pct=(pnl/cost)*100;
    tv+=val;tc+=cost;
    return`<div class="hr">
      <div class="h-sym">${h.asset}</div>
      <div class="h-inf"><div class="h-nm">${h.name}</div><div class="h-qty">${h.qty} × ${a.unit}${fmt(h.buyPx)}</div></div>
      <div class="h-pnl">
        <div class="h-val" style="color:${colOf(pnl)}">${a.unit}${fmt(val,val>=1000?0:2)}</div>
        <div class="h-pct" style="color:${colOf(pnl)}">${pnl>=0?'+':''}${fmt(pct)}%</div>
      </div>
      <button class="btn btn-d btn-sm btn-ico" onclick="rmHolding(${h.id})" style="margin-left:4px">×</button>
    </div>`;
  }).join('');
  const tpnl=tv-tc;const tpct=tc>0?(tpnl/tc)*100:0;
  document.getElementById('pf-val').textContent='$'+fmt(tv,0);
  const pnlEl=document.getElementById('pf-pnl');
  pnlEl.textContent=(tpnl>=0?'+$':'-$')+fmt(Math.abs(tpnl),0)+' ('+fmt(tpct,1)+'%)';
  pnlEl.style.color=colOf(tpnl);
  renderSbPf();
}
function renderSbPf(){
  const el=document.getElementById('sb-pf');
  if(!A.pf.length){el.innerHTML='<div class="fnt xs" style="padding:4px 8px">포트폴리오 없음</div>';return}
  let tv=0,tc=0;
  A.pf.forEach(h=>{const a=A.assets[h.asset];if(a){tv+=a.cur*h.qty;tc+=h.buyPx*h.qty}});
  const pnl=tv-tc;
  el.innerHTML=`<div style="padding:4px 8px">
    <div style="font-size:10px;color:var(--tf);margin-bottom:2px">총 평가금액</div>
    <div class="mono sem" style="font-size:13px">$${fmt(tv,0)}</div>
    <div class="mono xs" style="color:${colOf(pnl)};margin-top:1px">${pnl>=0?'+':''}$${fmt(pnl,0)} P&L</div>
  </div>`;
}
 
// =============================================
// TASKS
// =============================================
function openModal(){
  document.getElementById('t-due').value=new Date().toISOString().split('T')[0];
  document.getElementById('t-ttl').value='';
  document.getElementById('task-modal').classList.add('on');
  setTimeout(()=>document.getElementById('t-ttl').focus(),100);
}
function closeModal(){document.getElementById('task-modal').classList.remove('on')}
function submitTask(){
  const ttl=document.getElementById('t-ttl').value.trim();
  if(!ttl){toast('⚠️ 태스크 제목을 입력하세요.');return}
  A.tasks.push({
    id:Date.now(),title:ttl,
    cat:document.getElementById('t-cat').value,
    due:document.getElementById('t-due').value,
    pri:document.getElementById('t-pri').value,
    st:'todo'
  });
  sv('tasks_'+A.user.email,A.tasks);closeModal();renderKanban();toast('✅ 태스크가 추가되었습니다.');
}
function delTask(id){A.tasks=A.tasks.filter(t=>t.id!==id);sv('tasks_'+A.user.email,A.tasks);renderKanban()}
function mvTask(id,st){
  const t=A.tasks.find(t=>t.id===id);if(!t)return;
  t.st=st;sv('tasks_'+A.user.email,A.tasks);renderKanban();
  const lbl={todo:'할 일',inp:'진행 중',done:'완료'};toast(`✓ "${t.title}" → ${lbl[st]}`);
}
 
function renderKanban(){
  const cols={todo:[],inp:[],done:[]};
  A.tasks.forEach(t=>{if(cols[t.st])cols[t.st].push(t);else cols.todo.push(t)});
  const po={high:0,mid:1,low:2};
  Object.entries(cols).forEach(([st,tasks])=>{
    tasks.sort((a,b)=>(po[a.pri]||1)-(po[b.pri]||1));
    const el=document.getElementById('cards-'+st);
    document.getElementById('cnt-'+st).textContent=tasks.length;
    if(!tasks.length){el.innerHTML='<div class="empty" style="padding:20px"><div class="ei" style="font-size:20px">📭</div><div class="et">드래그하여 이동</div></div>';return}
    el.innerHTML=tasks.map(t=>mkCard(t,st)).join('');
  });
  updProg();
}
 
function mkCard(t,st){
  const pl={high:'높음',mid:'중간',low:'낮음'};
  const pc={high:'bh',mid:'bm',low:'bl2'};
  const today=new Date().toISOString().split('T')[0];
  const ov=t.due&&t.due<today&&t.st!=='done';
  const dueHtml=t.due?`<div class="tdue${ov?' ov':''}">
    ${ov?'⚠️':'📅'} ${(()=>{const d=new Date(t.due);return`${d.getMonth()+1}/${d.getDate()}`})()}
  </div>`:'';
  const nextSt={todo:'inp',inp:'done',done:'todo'};
  const nextLbl={todo:'▶ 시작',inp:'✅ 완료',done:'↩ 되돌리기'};
  return`<div class="tc" draggable="true" data-id="${t.id}"
    ondragstart="dstart(event)" ondragend="dend(event)">
    <div class="tc-hdr">
      <div class="tc-ttl">${esc(t.title)}</div>
      <button class="tc-del" onclick="delTask(${t.id})">×</button>
    </div>
    <div class="tc-meta">
      <span class="tbdg ${pc[t.pri]}">${pl[t.pri]}</span>
      <span class="tbdg bcat">${esc(t.cat)}</span>
    </div>
    ${dueHtml}
    <div class="mv-btn">
      <button class="btn btn-g btn-sm" style="font-size:11px;padding:3px 8px" onclick="mvTask(${t.id},'${nextSt[st]}')">${nextLbl[st]}</button>
    </div>
  </div>`;
}
 
function updProg(){
  const tot=A.tasks.length;const done=A.tasks.filter(t=>t.st==='done').length;
  const pct=tot>0?(done/tot)*100:0;
  document.getElementById('pgfill').style.width=pct+'%';
  document.getElementById('pg-txt').textContent=`${done} / ${tot} 완료`;
}
 
// =============================================
// DRAG & DROP
// =============================================
function dstart(e){
  const c=e.currentTarget;A.drag=parseInt(c.dataset.id);
  c.classList.add('dragging');e.dataTransfer.effectAllowed='move';
  e.dataTransfer.setData('text/plain',c.dataset.id);
}
function dend(e){e.currentTarget.classList.remove('dragging');document.querySelectorAll('.kcol').forEach(c=>c.classList.remove('dov'))}
function dov(e){e.preventDefault();e.dataTransfer.dropEffect='move';e.currentTarget.classList.add('dov')}
function dlv(e){if(!e.currentTarget.contains(e.relatedTarget))e.currentTarget.classList.remove('dov')}
function dop(e,st){
  e.preventDefault();e.currentTarget.classList.remove('dov');
  const id=A.drag||parseInt(e.dataTransfer.getData('text/plain'));
  if(!id)return;
  const t=A.tasks.find(t=>t.id===id);
  if(!t||t.st===st)return;
  t.st=st;sv('tasks_'+A.user.email,A.tasks);renderKanban();
  const lbl={todo:'할 일',inp:'진행 중',done:'완료'};toast(`✓ "${t.title}" → ${lbl[st]}`);
}
 
// =============================================
// NAVIGATION
// =============================================
function swView(v){
  A.view=v;
  document.querySelectorAll('.view').forEach(x=>x.classList.remove('on'));
  document.getElementById('v-'+v).classList.add('on');
  document.querySelectorAll('.ni').forEach(x=>x.classList.remove('on'));
  document.getElementById('ni-'+v).classList.add('on');
  const info={db:['금융 대시보드','실시간 시장 데이터 · 모의 투자'],tk:['학업 태스크 관리','칸반 보드로 학습 진행 현황 관리']};
  document.getElementById('vt').textContent=info[v][0];document.getElementById('vs').textContent=info[v][1];
  if(v==='db')setTimeout(()=>{if(A.pxCh)updChartData();else initCharts()},50);
}
 
// =============================================
// APP INIT
// =============================================
function startApp(){
  const u=A.user;
  document.getElementById('uav').textContent=(u.name||u.email)[0].toUpperCase();
  document.getElementById('u-nm').textContent=u.name||u.email;
  document.getElementById('u-risk').textContent=A.pref.risk==='stable'?'🛡️ 안정형':'🚀 공격투자형';
  showSec('sec-app');
  initMkt();renderMktCards();renderHdrTk();renderPf();renderKanban();
  setTimeout(initCharts,120);
  A.iv=setInterval(tickMkt,3000);
}
 
// =============================================
// BOOT
// =============================================
window.addEventListener('DOMContentLoaded',()=>{
  setTimeout(()=>{
    document.getElementById('ld').style.display='none';
    const em=ld('session');
    if(em){const u=ld('users',{})[em];if(u){loginUser(u);return}}
    showSec('sec-auth');
  },700);
});
 
document.addEventListener('keydown',e=>{
  if(e.key!=='Enter')return;
  if(document.getElementById('sec-auth').classList.contains('on')){
    if(document.getElementById('f-login').style.display!=='none')doLogin();else doReg();
  }
  if(document.getElementById('task-modal').classList.contains('on'))submitTask();
});
</script>
</body>
</html>
