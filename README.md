<html lang="zh">
<head>
  
  <link href="https://fonts.googleapis.com/css2?family=PT+Serif&display=swap" rel="stylesheet">
  <meta charset="UTF-8">
  <title>Teacher Awards 2025</title>
  <style>
  body {
    font-family: 'PT Serif', serif;
    background-color: #f0f2f5;
    padding: 30px;
    color: #202124;
  }
  h1 {
  color: #1a73e8;
  font-size: 30px;
  }
  
  h2 {
    font-size: 20px;
    line-height: 1.5;
    margin-bottom: 15px;
  }
  

  .form-container {
    width: 60%;
    margin: 0 auto;
    background: #fff;
    padding: 40px;
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  }

  .section-card {
    margin-bottom: 30px;
  }

  label {
  display: block;
  font-size: 18px; 
  margin-bottom: 18px;
  color: #202124;
  font-weight:bold;
}

input[type="text"],
select {
  font-size: 18px; 
  width: 100%;
  padding: 18px;
  border: 1px solid #dadce0;
  border-radius: 12px;
  margin-bottom: 18px;
  background-color: white;
}


  button {
    background-color: #1a73e8;
    color: white;
    font-size: 20px;
    padding: 14px 28px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    display: block;
    margin: 30px auto 0;
    transition: background-color 0.2s;
  }

  button:hover {
    background-color: #1765cc;
  }
</style>

</head>
<body>
  <div class="form-container">
    <h1>Teacher Awards 2025: The Yik Chiao Teacher Star Poll</h1>
    <h2>你心目中的“教师之星”是谁？⭐<br>
      是那个讲课超有梗、考试还会偷偷提示的“神助攻老师”？<br>
      还是每天像福尔摩斯一样盯作业、却又偷偷关心你的“刀子嘴豆腐心老师”？👀<br><br>
      【益侨教师之星】票选正式开始啦！<br>
      用你宝贵的一票，向你最爱的老师送上最闪亮的荣誉～✨<br><br>
      📌 规则简单：<br>
      - 每人只能投一次票哦（公平公正，老师不许贿选！）<br>
      - 按照你真实的感受选择就对了，老师不会生气，真的！<br>
      - 给每个老师一票，不要重复选！让票选更神圣！<br><br>
      快来投票吧🏆
    </h2>

    <form id="voteForm">
      <div class="section-card">
        <label>中文姓名：</label>
        <input type="text" name="name" required>
      </div>

      <div class="section-card">
        <label>班级：</label>
        <select name="class" required>
          <option value="">请选择班级</option>
          <option value="1R">1R</option>
          <option value="2R">2R</option>
          <option value="3R">3R</option>
          <option value="4R">4R</option>
          <option value="4Y">4Y</option>
          <option value="5R">5R</option>
          <option value="6R">6R</option>
          <option value="6Y">6Y</option>
        </select>
      </div>

      <div id="awardFields"></div>

      <button type="submit">提交</button>
    </form>
  </div>

  <script>const teachers = [
  'En. Lim Kim Leong 林金龙校长',
  'Pn. Ooi Suat Hoon 黄莉纷副校长',
  'Cik Tam Swee Lian 谭锐涟副校长',
  'Pn. Tan Huay Yen 陈惠媛副校长',
  'Pn. Wong Siew Yik 王秀玉师',
  'Pn. Teo Guat Keow 张月娇师',
  'Pn. Lee Pei Feng 李佩芬师',
  'Cik See Kai Jun 徐凯君师',
  'Cik Tung Pei Yee 陈佩仪师',
  'Cik Cheok Li Ching 石敏静师',
  'Pn. Hong Chai Leng 方采灵师',
  'Pn. Lee Fee Chin 李慧琴师',
  'Pn. Lam Mei Wei 蓝美蔚师',
  'Cik Ainnur Zahirah',
  'Cik Connie Law Siao Ying 刘筱莹师',
  'Pn. Lee Li Khim "李丽琴师',
  'Cik Nurdini Qistina',
  'Cik Teh Yi Suan 郑艺璇师',
  'Pn. Hanizatul Akma',
  'Pn. Wong Chiau Siang 黄蛟鄕师'
];


    const awards = [
      "最有爱心老师 · Most Caring Teacher",
      "最阳光灿烂老师 · Most Cheerful Teacher",
      "最严格有爱的老师 · Strict but Loving Teacher",
      "最有创意老师 · Most Creative Teacher",
      "最搞笑老师 · Most Entertaining Teacher",
      "最有耐心老师 · Most Patient Teacher",
      "最有型老师 · Most Stylish Teacher",
      "最具启发性老师 · Most Inspirational Teacher",
      "最亲民最配合的老师 · Most Approachable Teacher",
      "最勤奋老师 · Most Hardworking Teacher",
      "最冷静沉稳老师 · Most Calm & Composed Teacher",
      "最关怀学生老师 · Most Student-Caring Teacher",
      "最有纪律的老师 · Most Disciplined Teacher",
      "最会用科技的老师 · Most Tech-Savvy Teacher",
      "最有拼劲老师 · Most Spirited Teacher",
      "最可爱活泼老师 · Most Adorable and Energetic Teacher",
      "最有文采老师 · Best Rhymer or Poet Teacher",
      "最幽默又聪明老师 · Funniest but Smartest Teacher",
      "最活跃课外活动老师 · Most Active in Co-curricular Teacher",
      "学校领航之星 · Star of School Drive & Direction"
    ];

    const selected = new Map();

    function renderOptions(currentIndex) {
      return teachers.filter(t => {
        for (const [key, val] of selected) {
          if (key !== currentIndex && val === t) return false;
        }
        return true;
      });
    }

    function createAwardSelect(index, awardName) {
      const section = document.createElement("div");
      section.className = "section-card";

      const label = document.createElement("label");
      label.textContent = awardName;

      const select = document.createElement("select");
      select.name = `award${index}`;
      select.dataset.index = index;
      select.required = true;

      const render = () => {
        const currentValue = selected.get(index) || "";
        const options = renderOptions(index);
        select.innerHTML = '<option value="">请选择老师</option>';
        options.forEach(teacher => {
          const option = document.createElement("option");
          option.value = teacher;
          option.textContent = teacher;
          if (teacher === currentValue) option.selected = true;
          select.appendChild(option);
        });
      };

      select.addEventListener("change", () => {
        selected.set(index, select.value);
        document.querySelectorAll("select[data-index]").forEach(sel => {
          const i = Number(sel.dataset.index);
          renderOptions(i).forEach((teacher) => {
            if (![...sel.options].some(o => o.value === teacher)) {
              const option = document.createElement("option");
              option.value = teacher;
              option.textContent = teacher;
              sel.appendChild(option);
            }
          });
          [...sel.options].forEach(option => {
            if (
              option.value &&
              !renderOptions(i).includes(option.value) &&
              sel.value !== option.value
            ) {
              option.remove();
            }
          });
        });
      });

      render();
      section.appendChild(label);
      section.appendChild(select);
      return section;
    }

    window.addEventListener("DOMContentLoaded", () => {
      const container = document.getElementById("awardFields");
      awards.forEach((award, i) => {
        const section = createAwardSelect(i, award);
        container.appendChild(section);
      });
    });
  </script>
</body>
</html>
<script>
  document.getElementById("voteForm").addEventListener("submit", function(e) {
    e.preventDefault();

    const form = e.target;
    const formData = new FormData(form);

    const awards = [];
    for (let i = 0; i < 20; i++) {
      awards.push(formData.get("award" + i));
    }

    const data = {
      name: formData.get("name"),
      class: formData.get("class"),
      awards: awards
    };

    fetch("https://script.google.com/macros/s/AKfycbzIrxlOFLqN6daaS_padE5MAtyir9wC5Ikz1MWGf8y9B8id_t3XagPBFSkKT_QqL7XGnA/exec", {
      method: "POST",
      body: JSON.stringify(data),
      headers: {
        "Content-Type": "application/json"
      }
    }).then(res => res.json())
      .then(result => {
        if (result.status === "success") {
          alert("投票成功，感谢你的参与！");
          form.reset();
        } else {
          alert("提交失败，请稍后再试！");
        }
      }).catch(err => {
        alert("网络错误，提交失败！");
        console.error(err);
      });
  });
</script>
