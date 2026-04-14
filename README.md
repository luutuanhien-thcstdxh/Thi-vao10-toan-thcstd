<!DOCTYPE html>
<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>YoungTest - Công cụ Giao đề Online</title>
    <link
      href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&display=swap"
      rel="stylesheet"
    />
    <link
      href="https://fonts.googleapis.com/css2?family=Rowdies:wght@300;400;700&display=swap"
      rel="stylesheet"
    />
    <style>
      body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 20px;
        background: white;
        display: flex;
        align-items: center;
        justify-content: center;
        max-height: 100vh;
        overflow: hidden;
      }
      .container {
        width: 480px;
        padding: 20px;
        background: linear-gradient(to bottom, #dcefd1, #549654);
        border-radius: 10px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        box-sizing: border-box;
      }
      .header {
        text-align: center;
        font-size: 32px;
        font-weight: bold;
        font-family: "Rowdies", cursive;
        color: #2e5f30;
      }
      .subtitle {
        text-align: end;
        padding-right: 20%;
        font-style: italic;
        color: #5b895b;
        font-size: 24px;
        font-family: "Dancing Script", cursive;
        margin-bottom: 5px;
      }
      .main-content {
        display: flex;
        align-items: center;
        justify-content: space-between;
      }
      .phone {
        width: 180px;
      }
      .features {
        width: 50%;
      }
      .features div {
        background: white;
        margin: 10px 0;
        padding: 12px;
        border-radius: 8px;
        display: flex;
        align-items: center;
        box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
        font-size: 16px;
      }
      .video-section {
        margin-top: 10px;
        display: flex;
        justify-content: space-between;
      }
      iframe {
        box-sizing: border-box;
        padding: 5px;
        background: white;
        height: 22vh;
        border-radius: 8px;
      }
      .students-img {
        box-sizing: border-box;
        padding: 5px;
        background: white;
        height: 22vh;
        border-radius: 8px;
      }
      .url a {
        padding: 6px;
        padding-top: 0px;
        display: flex;
        text-decoration: none;
        align-items: center;
        justify-content: end;
        font-size: 24px;
        color: #ffffff;
        font-family: "Rowdies", cursive;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="header">Công cụ Giao đề</div>
      <div class="subtitle">Online</div>
      <div class="main-content">
        <img src="https://i.postimg.cc/j24z3QGY/phone.png" class="phone" />
        <div class="features">
          <div>✅ Bạn là Giáo viên</div>
          <div>📌 Bạn cần một công cụ</div>
          <div>📖 Giao đề Online 2025</div>
          <div>🎯 Đến học sinh của mình</div>
        </div>
      </div>
      <div class="url">
        <a href="https://youngtest.vn/">www.youngtest.vn</a>
      </div>
      <div class="video-section">
        <iframe
          src="https://www.youtube.com/embed/eYTsHjTa1t4?si=HiqabeY-pZlBXdHI"
          allowfullscreen
        ></iframe>
        <img src="https://i.postimg.cc/vHx3DGjB/a2.jpg" class="students-img" />
      </div>
    </div>
  </body>
</html>
