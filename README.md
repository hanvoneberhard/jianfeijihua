这是为您量身定制的可打卡减肥追踪网页，已适配手机，方便您随时记录每日任务完成情况。
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
  <title>倒班减肥打卡 · 全季前台计划</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Helvetica, Arial, sans-serif;
      background: #f5f7fa;
      padding: 16px;
      color: #1e293b;
    }
    .container {
      max-width: 500px;
      margin: 0 auto;
    }
    h1 {
      font-size: 1.8rem;
      font-weight: 700;
      margin-bottom: 4px;
      color: #0f172a;
      text-align: center;
    }
    .subtitle {
      text-align: center;
      font-size: 0.9rem;
      color: #64748b;
      margin-bottom: 24px;
      line-height: 1.4;
    }
    .week-nav {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }
    .week-nav button {
      background: white;
      border: 1px solid #e2e8f0;
      padding: 8px 16px;
      border-radius: 30px;
      font-size: 0.9rem;
      font-weight: 500;
      color: #334155;
      cursor: pointer;
      box-shadow: 0 1px 3px rgba(0,0,0,0.04);
      transition: all 0.2s;
    }
    .week-nav button:active {
      background: #f1f5f9;
      transform: scale(0.97);
    }
    .week-range {
      font-weight: 600;
      color: #0f172a;
      font-size: 0.95rem;
      background: white;
      padding: 6px 16px;
      border-radius: 30px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.05);
    }
    .day-card {
      background: white;
      border-radius: 20px;
      padding: 18px 16px;
      margin-bottom: 16px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.04);
      transition: all 0.2s;
    }
    .day-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 14px;
    }
    .day-date {
      font-weight: 700;
      font-size: 1.2rem;
      color: #0f172a;
    }
    .shift-badge {
      font-size: 0.8rem;
      font-weight: 600;
      padding: 4px 12px;
      border-radius: 20px;
      background: #f1f5f9;
      color: #475569;
    }
    .shift-badge.night {
      background: #e0e7ff;
      color: #3730a3;
    }
    .shift-badge.rest {
      background: #dcfce7;
      color: #166534;
    }
    .shift-badge.morning {
      background: #fef9c3;
      color: #854d0e;
    }
    .task-list {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    .task-item {
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .task-item input[type="checkbox"] {
      appearance: none;
      -webkit-appearance: none;
      width: 22px;
      height: 22px;
      border: 2px solid #cbd5e1;
      border-radius: 6px;
      background: white;
      cursor: pointer;
      flex-shrink: 0;
      transition: all 0.15s;
      position: relative;
    }
    .task-item input[type="checkbox"]:checked {
      background: #16a34a;
      border-color: #16a34a;
    }
    .task-item input[type="checkbox"]:checked::after {
      content: "";
      position: absolute;
      left: 6px;
      top: 2px;
      width: 6px;
      height: 11px;
      border: solid white;
      border-width: 0 2px 2px 0;
      transform: rotate(45deg);
    }
    .task-item label {
      font-size: 0.95rem;
      color: #334155;
      line-height: 1.4;
      flex: 1;
      cursor: pointer;
    }
    .task-item.completed label {
      text-decoration: line-through;
      color: #94a3b8;
    }
    .divider {
      border: none;
      border-top: 1px dashed #e2e8f0;
      margin: 12px 0 8px;
    }
    .section-title {
      font-size: 0.8rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      color: #64748b;
      margin-bottom: 4px;
    }
    .progress {
      font-size: 0.8rem;
      color: #475569;
      margin-top: 10px;
      text-align: right;
      font-weight: 500;
    }
    .reset-btn {
      display: block;
      width: 100%;
      margin: 24px 0 10px;
      padding: 12px;
      background: white;
      border: 1px solid #fecaca;
      color: #b91c1c;
      font-weight: 600;
      border-radius: 30px;
      font-size: 0.95rem;
      cursor: pointer;
      transition: 0.2s;
    }
    .reset-btn:active {
      background: #fee2e2;
    }
    .tip {
      font-size: 0.75rem;
      color: #94a3b8;
      text-align: center;
      margin-top: 8px;
    }
  </style>
</head>
<body>
<div class="container">
  <h1>🥗 分格盘打卡</h1>
  <div class="subtitle">全季前台 · 倒班减脂计划<br>皮肤安全优先 · 金属餐盘量化</div>

  <div class="week-nav">
    <button id="prevWeekBtn">◀ 上一周</button>
    <span class="week-range" id="weekRange">8月10日 - 8月16日</span>
    <button id="nextWeekBtn">下一周 ▶</button>
  </div>

  <div id="cardsContainer"></div>

  <button class="reset-btn" id="resetBtn">🗑️ 重置本周所有打卡记录</button>
  <div class="tip">数据保存在手机浏览器中，无上传</div>
</div>

<script>
  (function() {
    // ---------- 班次定义 ----------
    const SHIFT = {
      MORNING: '早班 (8-20)',
      NIGHT: '夜班 (20-次日8)',
      REST_AFTER_NIGHT: '休息 (下夜班)',
      REST_FULL: '休息 (全天)'
    };

    // 4天循环顺序: 早班, 夜班, 休息(下夜班), 休息(全天)
    const CYCLE = [SHIFT.MORNING, SHIFT.NIGHT, SHIFT.REST_AFTER_NIGHT, SHIFT.REST_FULL];

    // 起始日: 2026-08-10 是夜班 (按用户说明)
    const START_DATE = new Date(2026, 7, 10); // 月份从0开始，7是八月
    const START_SHIFT_INDEX = 1; // CYCLE[1] = 夜班

    // 默认显示第一周 (8月10日 - 8月16日)
    let currentWeekStart = new Date(START_DATE);
    const DAYS_IN_WEEK = 7;

    // 存储前缀
    const STORAGE_PREFIX = 'fitplan_';

    // ---------- 根据日期获取班次 ----------
    function getShiftForDate(date) {
      const diffTime = date.getTime() - START_DATE.getTime();
      const diffDays = Math.floor(diffTime / (1000 * 60 * 60 * 24));
      const index = (START_SHIFT_INDEX + diffDays) % CYCLE.length;
      const adjustedIndex = index < 0 ? index + CYCLE.length : index;
      return CYCLE[adjustedIndex];
    }

    // ---------- 生成日期范围内的任务列表 ----------
    function generateTasksForDate(dateStr, shift) {
      const tasks = [];
      
      // 通用饮食任务
      tasks.push({ id: 'breakfast', label: '🍳 早餐：1蛋+主食+无糖豆浆/牛奶', category: '饮食' });
      tasks.push({ id: 'lunch', label: '🥙 午餐 (11:00) 分格盘：½蔬菜,¼蛋白,¼主食 · 涮油', category: '饮食' });
      tasks.push({ id: 'dinner', label: '🍛 晚餐 (15:30-16:30) 分格盘打餐 · 涮油', category: '饮食' });
      tasks.push({ id: 'water', label: '💧 饮水 ≥ 2升 (站班间隙勤喝)', category: '饮食' });
      
      // 饮酒管理
      tasks.push({ id: 'alcohol', label: '🍷 饮酒控制：未喝 / 若喝则选干红且晚餐主食减半', category: '习惯' });

      // 吸烟与情绪
      tasks.push({ id: 'smoke_delay', label: '🚬 推迟第一支烟时间 (尽量延迟)', category: '习惯' });
      tasks.push({ id: 'emotion', label: '🧠 情绪进食急救：使用15分钟缓冲法', category: '习惯' });

      // 运动相关 (根据班次)
      if (shift === SHIFT.MORNING) {
        tasks.push({ id: 'move_morning', label: '🧍 工作间隙：腹肌收紧+提踵 (多次)', category: '运动' });
        tasks.push({ id: 'smoke_sport', label: '🚭 运动前后2小时不吸烟 (无专门运动也注意)', category: '习惯' });
      } else if (shift === SHIFT.NIGHT) {
        tasks.push({ id: 'move_night', label: '🚶 夜班前轻量运动：快走30分/椭圆机20-30分 (下午,晚餐前)', category: '运动' });
        tasks.push({ id: 'smoke_sport', label: '🚭 运动前后2小时绝对不吸烟', category: '习惯' });
      } else if (shift === SHIFT.REST_AFTER_NIGHT) {
        tasks.push({ id: 'rest_sleep', label: '😴 充分休息睡觉，温和拉伸 (避免皮肤牵拉)', category: '运动' });
      } else if (shift === SHIFT.REST_FULL) {
        tasks.push({ id: 'train_warmup', label: '🔄 热身：椭圆机/卧式单车5分钟', category: '运动' });
        tasks.push({ id: 'train_strength', label: '🏋️ 力量训练 (垫毛巾)：鸟狗式·死虫式·臀桥·跪姿推拉', category: '运动' });
        tasks.push({ id: 'train_cardio', label: '🏊 有氧：游泳20-30分钟 或 快走40分钟 (泳后冲洗润肤)', category: '运动' });
        tasks.push({ id: 'smoke_sport', label: '🚭 运动前后2小时绝对不吸烟', category: '习惯' });
      }

      return tasks;
    }

    // ---------- 获取一周的日期范围 ----------
    function getWeekDates(startDate) {
      const dates = [];
      const start = new Date(startDate);
      for (let i = 0; i < DAYS_IN_WEEK; i++) {
        const d = new Date(start);
        d.setDate(start.getDate() + i);
        dates.push(d);
      }
      return dates;
    }

    // 格式化日期为 YYYY-MM-DD
    function formatDateStr(date) {
      const year = date.getFullYear();
      const month = String(date.getMonth() + 1).padStart(2, '0');
      const day = String(date.getDate()).padStart(2, '0');
      return `${year}-${month}-${day}`;
    }

    // 格式化显示日期 (如 8月10日 周一)
    function formatDisplayDate(date) {
      const month = date.getMonth() + 1;
      const day = date.getDate();
      const weekdays = ['周日', '周一', '周二', '周三', '周四', '周五', '周六'];
      const weekday = weekdays[date.getDay()];
      return `${month}月${day}日 ${weekday}`;
    }

    // ---------- 本地存储操作 ----------
    function getStorageKey(dateStr, taskId) {
      return STORAGE_PREFIX + dateStr + '_' + taskId;
    }

    function loadCheckState(dateStr, taskId) {
      return localStorage.getItem(getStorageKey(dateStr, taskId)) === 'true';
    }

    function saveCheckState(dateStr, taskId, checked) {
      localStorage.setItem(getStorageKey(dateStr, taskId), checked);
    }

    function clearWeekData(dates) {
      dates.forEach(date => {
        const dateStr = formatDateStr(date);
        const shift = getShiftForDate(date);
        const tasks = generateTasksForDate(dateStr, shift);
        tasks.forEach(task => {
          localStorage.removeItem(getStorageKey(dateStr, task.id));
        });
      });
    }

    // ---------- 渲染卡片 ----------
    function renderCards(weekStart) {
      const container = document.getElementById('cardsContainer');
      const dates = getWeekDates(weekStart);
      let html = '';

      dates.forEach(date => {
        const dateStr = formatDateStr(date);
        const shift = getShiftForDate(date);
        const tasks = generateTasksForDate(dateStr, shift);
        
        let shiftClass = '';
        if (shift.includes('夜班')) shiftClass = 'night';
        else if (shift.includes('休息')) shiftClass = 'rest';
        else if (shift.includes('早班')) shiftClass = 'morning';

        let tasksHtml = '';
        let totalTasks = tasks.length;
        
        // 按类别分组显示
        const categories = ['饮食', '运动', '习惯'];
        categories.forEach(cat => {
          const catTasks = tasks.filter(t => t.category === cat);
          if (catTasks.length === 0) return;
          tasksHtml += `<div class="section-title">${cat}</div>`;
          catTasks.forEach(task => {
            const checked = loadCheckState(dateStr, task.id);
            const completedClass = checked ? 'completed' : '';
            tasksHtml += `
              <div class="task-item ${completedClass}">
                <input type="checkbox" id="${dateStr}_${task.id}" data-date="${dateStr}" data-task="${task.id}" ${checked ? 'checked' : ''}>
                <label for="${dateStr}_${task.id}">${task.label}</label>
              </div>
            `;
          });
          if (cat !== categories[categories.length-1]) {
            tasksHtml += '<hr class="divider">';
          }
        });

        // 计算已完成数量
        let completedCount = 0;
        tasks.forEach(task => {
          if (loadCheckState(dateStr, task.id)) completedCount++;
        });
        const progressPercent = totalTasks > 0 ? Math.round((completedCount / totalTasks) * 100) : 0;

        html += `
          <div class="day-card">
            <div class="day-header">
              <span class="day-date">${formatDisplayDate(date)}</span>
              <span class="shift-badge ${shiftClass}">${shift}</span>
            </div>
            <div class="task-list">
              ${tasksHtml}
            </div>
            <div class="progress">✅ ${completedCount}/${totalTasks} · ${progressPercent}%</div>
          </div>
        `;
      });

      container.innerHTML = html;

      // 更新周范围显示
      const endDate = new Date(weekStart);
      endDate.setDate(weekStart.getDate() + 6);
      document.getElementById('weekRange').textContent = 
        `${formatDisplayDate(weekStart).split(' ')[0]} - ${formatDisplayDate(endDate).split(' ')[0]}`;
    }

    // ---------- 绑定事件 ----------
    function attachEvents() {
      const container = document.getElementById('cardsContainer');
      container.addEventListener('change', function(e) {
        if (e.target.tagName === 'INPUT' && e.target.type === 'checkbox') {
          const dateStr = e.target.dataset.date;
          const taskId = e.target.dataset.task;
          const checked = e.target.checked;
          saveCheckState(dateStr, taskId, checked);
          
          // 更新任务项的完成样式和进度
          const taskItem = e.target.closest('.task-item');
          if (taskItem) {
            if (checked) {
              taskItem.classList.add('completed');
            } else {
              taskItem.classList.remove('completed');
            }
          }
          // 更新该卡片进度
          updateCardProgress(dateStr);
        }
      });
    }

    function updateCardProgress(dateStr) {
      const cards = document.querySelectorAll('.day-card');
      cards.forEach(card => {
        const inputs = card.querySelectorAll('input[type="checkbox"]');
        let total = 0, completed = 0;
        inputs.forEach(inp => {
          if (inp.dataset.date === dateStr || !dateStr) {
            total++;
            if (inp.checked) completed++;
          }
        });
        if (total > 0) {
          const percent = Math.round((completed / total) * 100);
          const progressEl = card.querySelector('.progress');
          if (progressEl) {
            progressEl.textContent = `✅ ${completed}/${total} · ${percent}%`;
          }
        }
      });
    }

    // 周切换
    function changeWeek(offset) {
      const newStart = new Date(currentWeekStart);
      newStart.setDate(currentWeekStart.getDate() + offset * DAYS_IN_WEEK);
      currentWeekStart = newStart;
      renderCards(currentWeekStart);
    }

    // 重置本周
    function resetCurrentWeek() {
      const dates = getWeekDates(currentWeekStart);
      if (confirm('确定要清除本周所有打卡记录吗？此操作不可恢复。')) {
        clearWeekData(dates);
        renderCards(currentWeekStart);
      }
    }

    // ---------- 初始化 ----------
    function init() {
      renderCards(currentWeekStart);
      attachEvents();

      document.getElementById('prevWeekBtn').addEventListener('click', () => changeWeek(-1));
      document.getElementById('nextWeekBtn').addEventListener('click', () => changeWeek(1));
      document.getElementById('resetBtn').addEventListener('click', resetCurrentWeek);
    }

    // 页面加载启动
    window.addEventListener('DOMContentLoaded', init);
  })();
</script>
</body>
</html>
```
