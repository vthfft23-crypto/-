<!doctype html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>محمد… لازم تعرف شي</title>
  <style>
    body{
      margin:0;
      font-family: Arial, sans-serif;
      height:100vh;
      overflow:hidden;
      display:flex;
      justify-content:center;
      align-items:center;

      /* خلفية متحركة */
      background: linear-gradient(135deg, #ff8fb3, #ffd6e5, #ffbfd3, #ff9fc2);
      background-size: 400% 400%;
      animation: bgMove 12s ease-in-out infinite;
    }

    @keyframes bgMove {
      0%{ background-position: 0% 50%; }
      50%{ background-position: 100% 50%; }
      100%{ background-position: 0% 50%; }
    }

    .box{
      background:white;
      width:340px;
      padding:24px;
      border-radius:20px;
      text-align:center;
      box-shadow:0 10px 30px rgba(0,0,0,0.15);
      animation: pop 0.4s ease;
      position:relative;
      z-index:10;
    }
    @keyframes pop{
      from{transform:scale(0.7);opacity:0}
      to{transform:scale(1);opacity:1}
    }

    h1{margin:0 0 14px;font-size:22px;color:#222}
    p{color:#555;margin-bottom:18px}

    .heart-btn{
      padding:12px;
      border:0;
      background:#ff4f7a;
      color:white;
      border-radius:50%;
      font-size:15px;
      cursor:pointer;
      margin:10px;
      width:68px;
      height:68px;
      display:flex;
      justify-content:center;
      align-items:center;
      box-shadow:0 6px 15px rgba(255,79,122,0.4);
      transition:0.2s;
    }
    .heart-btn:hover{
      transform:scale(1.12);
    }

    #msg{
      margin-top:20px;
      font-size:22px;
      color:#333;
      min-height:50px;
      white-space:pre-wrap;
    }

    .cursor{
      display:inline-block;
      width:8px;
      height:22px;
      background:#333;
      animation:blink 1s steps(2) infinite;
    }
    @keyframes blink{50%{opacity:0}}

    /* القلوب المتحركة */
    .float-heart{
      position:fixed;
      bottom:-30px;
      color:#ff4f7a;
      font-size:22px;
      animation:float 3s ease-out forwards;
      opacity:0.8;
      pointer-events:none;
    }

    @keyframes float{
      0%{transform:translateY(0) scale(0.8);opacity:0.8}
      100%{transform:translateY(-220px) scale(1.5);opacity:0}
    }
  </style>
</head>
<body>
  <div class="box">
    <h1>إلى محمد…</h1>
    <p>أكو شي لازم تعرفه.</p>

    <button class="heart-btn" onclick="reveal()">هي شنو؟</button>
    <button class="heart-btn" onclick="reveal()">ماريد اعرف</button>

    <div id="msg"></div>
  </div>

  <!-- صوت جميل -->
  <audio id="loveSound">
    <source src="https://files.catbox.moe/5xk0l3.mp3" type="audio/mpeg">
  </audio>

  <script>
    const text = "محمد اني احبك";

    function reveal(){
      const msg = document.getElementById("msg");
      const sound = document.getElementById("loveSound");

      msg.textContent = "";
      let i = 0;

      // تشغيل الصوت
      sound.currentTime = 0;
      sound.play();

      // كتابة تدريجية
      const cursor = document.createElement("span");
      cursor.className = "cursor";
      msg.appendChild(cursor);

      function type(){
        if(i < text.length){
          cursor.insertAdjacentText("beforebegin", text[i]);
          i++;
          spawnHeart(); // قلب يطلع مع كل حرف
          setTimeout(type, 70);
        } else {
          cursor.remove();
        }
      }
      type();
    }

    // إنشاء القلوب المتحركة
    function spawnHeart(){
      const heart = document.createElement("div");
      heart.className = "float-heart";
      heart.textContent = "❤️";

      const x = Math.random() * window.innerWidth;
      heart.style.left = x + "px";

      document.body.appendChild(heart);

      setTimeout(()=> heart.remove(), 3000);
    }
  </script>
</body>
</html>
