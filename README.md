<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MD5 PROXTON | HITCLUB</title>

<style>
html,body{
margin:0;padding:0;width:100%;height:100%;
overflow:hidden;font-family:Segoe UI
}
#gameFrame{
position:fixed;top:0;left:0;
width:100%;height:100%;
border:none
}

/* ===== MD5 OVERLAY ===== */
#md5Overlay{
position:fixed;bottom:12px;right:12px;z-index:999999;
width:260px;background:#0a0a0a;color:#fff;
border:1px solid #333;border-radius:10px;
box-shadow:0 0 15px rgba(0,0,0,.8)
}
#md5Header{
padding:6px 10px;font-weight:bold;
color:#ffd700;font-size:13px;
display:flex;justify-content:space-between;
cursor:pointer
}
#md5Body{padding:8px}
#md5Overlay input{
width:100%;padding:6px;
background:#000;border:1px solid #444;
color:#ffd700;font-family:monospace;
border-radius:6px;font-size:12px
}
#md5Overlay button{
margin-top:6px;width:100%;
border:none;padding:6px;
background:linear-gradient(45deg,#b8860b,#ffd700);
font-weight:bold;border-radius:6px
}
.result{
display:flex;justify-content:space-between;
margin-top:6px;font-size:13px
}
.tai{color:#ff4757}
.xiu{color:#2e86de}
.status{
margin-top:5px;font-size:11px;
color:#aaa;text-align:center
}
</style>
</head>

<body>

<!-- HITCLUB -->
<iframe id="gameFrame"
src="https://v.hitclub.pro/?a=hitclub">
</iframe>

<!-- MD5 TOOL -->
<div id="md5Overlay">
    <div id="md5Header" onclick="toggleMD5()">MD5 PROXTON <span>−</span></div>
    <div id="md5Body">
        <input id="md5Input" placeholder="MD5">
        <button onclick="analyze()">PHÂN TÍCH</button>
        <div class="result">
            <span class="tai">TÀI: <b id="t">0%</b></span>
            <span class="xiu">XỈU: <b id="x">0%</b></span>
        </div>
        <div class="status" id="s">Chờ MD5</div>
    </div>
</div>

<script>
let hide=false,history=[];
function toggleMD5(){
    hide=!hide;
    md5Body.style.display=hide?"none":"block";
    md5Header.lastChild.textContent=hide?"+":"−";
}

function proxton(h){
    let w=0,hex="0123456789abcdef";
    for(let i=0;i<h.length;i++){
        w+=hex.indexOf(h[i].toLowerCase())*(i%2?0.8:1.5);
    }
    let t=w%100;
    return{t,x:100-t};
}

function streak(){
    if(!history.length) return{l:0,o:null};
    let o=history[history.length-1],l=1;
    for(let i=history.length-2;i>=0;i--){
        if(history[i]===o)l++;else break;
    }
    return{l,o};
}

function analyze(){
    let h=md5Input.value.trim();
    if(h.length<5) return;
    let r=proxton(h),st=streak();
    if(st.l>=3){
        if(st.o==="T")r.t+=5;
        if(st.o==="X")r.x+=5;
    }
    r.t=Math.min(99,Math.max(1,Math.round(r.t)));
    r.x=100-r.t;
    t.innerText=r.t+"%";
    x.innerText=r.x+"%";
    let side=r.t>r.x?"T":"X";
    history.push(side);
    if(history.length>50)history.shift();
    s.innerText=`Cầu ${st.o||"?"} (${st.l}) • ${side==="T"?"TÀI":"XỈU"}`;
}
</script>

</body>
</html>
