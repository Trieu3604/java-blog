---
title: "10 dự án nhỏ để luyện JavaScript"
date: 2025-02-11
slug: /du-an-nho-javascript/
description: 10 ý tưởng dự án nhỏ bằng JavaScript giúp học viên nắm vững ngôn ngữ nhanh hơn.
image: images/javascriptproject.png
caption: Dự án JavaScript nhỏ
draft: false
tags: ["JavaScript", "Dự án", "Thực hành"]
categories: ["Lập trình"]
---

## Giới thiệu

Bạn đã học xong cú pháp cơ bản của JavaScript nhưng vẫn chưa biết áp dụng kiến thức vào đâu? Đây là vấn đề mà rất nhiều người mới học lập trình gặp phải. Cách tốt nhất để củng cố kiến thức và nâng cao kỹ năng là **làm dự án thực tế**.

Trong bài viết này, tôi sẽ giới thiệu **10 dự án nhỏ** phù hợp cho người mới bắt đầu với JavaScript. Mỗi dự án sẽ giúp bạn rèn luyện các kỹ năng quan trọng như thao tác DOM, xử lý sự kiện, làm việc với API, và tư duy logic lập trình.

## Tại sao nên làm dự án nhỏ?

Trước khi đi vào chi tiết các dự án, hãy cùng tìm hiểu lý do tại sao việc làm dự án nhỏ lại quan trọng:

1. **Học qua thực hành**: Lý thuyết giúp bạn hiểu, nhưng thực hành giúp bạn nhớ lâu
2. **Xây dựng portfolio**: Các dự án này có thể đưa vào CV khi xin việc
3. **Phát hiện điểm yếu**: Khi code thực tế, bạn sẽ biết mình cần học thêm gì
4. **Tăng sự tự tin**: Mỗi dự án hoàn thành là một bước tiến lớn
5. **Rèn luyện tư duy**: Giải quyết vấn đề thực tế giúp bạn trở thành developer tốt hơn

## 10 dự án JavaScript cho người mới bắt đầu

### 1. Đồng hồ số (Digital Clock)

**Độ khó**: ⭐ Dễ  
**Thời gian**: 30-60 phút

**Mục tiêu học tập:**
- Làm việc với `Date` object
- Cập nhật DOM động
- Sử dụng `setInterval()`

**Tính năng gợi ý:**
- Hiển thị giờ, phút, giây real-time
- Thêm định dạng 12h/24h
- Hiển thị ngày tháng năm
- Thêm hiệu ứng animation

**Gợi ý code:**
```javascript
function updateClock() {
  const now = new Date();
  const hours = now.getHours().toString().padStart(2, '0');
  const minutes = now.getMinutes().toString().padStart(2, '0');
  const seconds = now.getSeconds().toString().padStart(2, '0');
  
  document.getElementById('clock').textContent = `${hours}:${minutes}:${seconds}`;
}

setInterval(updateClock, 1000);
updateClock(); // Gọi ngay lập tức
```

### 2. Máy tính cầm tay (Calculator)

**Độ khó**: ⭐⭐ Trung bình  
**Thời gian**: 2-3 giờ

**Mục tiêu học tập:**
- Xử lý sự kiện click
- Làm việc với string và number
- Logic tính toán
- Xử lý lỗi

**Tính năng gợi ý:**
- Các phép tính cơ bản (+, -, ×, ÷)
- Nút xóa (Clear, Backspace)
- Tính toán với số thập phân
- Hiển thị lỗi khi chia cho 0
- Lưu lịch sử tính toán

**Thử thách thêm:**
- Hỗ trợ phím tắt từ bàn phím
- Thêm phép tính nâng cao (%, √, x²)
- Responsive design

### 3. To-do List

**Độ khó**: ⭐⭐ Trung bình  
**Thời gian**: 2-4 giờ

**Mục tiêu học tập:**
- CRUD operations (Create, Read, Update, Delete)
- LocalStorage API
- Event delegation
- Array methods (filter, map, forEach)

**Tính năng gợi ý:**
- Thêm/xóa/sửa task
- Đánh dấu hoàn thành
- Lọc task (All, Active, Completed)
- Lưu dữ liệu vào LocalStorage
- Đếm số task còn lại

**Code mẫu LocalStorage:**
```javascript
// Lưu dữ liệu
function saveTodos(todos) {
  localStorage.setItem('todos', JSON.stringify(todos));
}

// Lấy dữ liệu
function loadTodos() {
  const todos = localStorage.getItem('todos');
  return todos ? JSON.parse(todos) : [];
}
```

### 4. App thời tiết (Weather App)

**Độ khó**: ⭐⭐⭐ Trung bình - Khó  
**Thời gian**: 3-5 giờ

**Mục tiêu học tập:**
- Fetch API / Async/Await
- Làm việc với REST API
- Xử lý JSON data
- Error handling
- API key management

**Tính năng gợi ý:**
- Tìm kiếm thời tiết theo tên thành phố
- Hiển thị nhiệt độ, độ ẩm, tốc độ gió
- Icon thời tiết động
- Chuyển đổi °C/°F
- Dự báo 5-7 ngày

**API miễn phí:**
- OpenWeatherMap API
- WeatherAPI
- Weatherbit

**Ví dụ fetch data:**
```javascript
async function getWeather(city) {
  try {
    const apiKey = 'YOUR_API_KEY';
    const response = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`
    );
    
    if (!response.ok) throw new Error('City not found');
    
    const data = await response.json();
    displayWeather(data);
  } catch (error) {
    console.error('Error:', error);
    alert(error.message);
  }
}
```

### 5. Trò chơi đoán số (Number Guessing Game)

**Độ khó**: ⭐ Dễ  
**Thời gian**: 1-2 giờ

**Mục tiêu học tập:**
- Sử dụng `Math.random()`
- Điều kiện if/else
- Game logic
- DOM manipulation

**Tính năng gợi ý:**
- Tạo số ngẫu nhiên (1-100)
- Kiểm tra đoán cao/thấp/đúng
- Đếm số lần đoán
- Hệ thống điểm số
- Nút chơi lại

**Game flow:**
```javascript
let randomNumber = Math.floor(Math.random() * 100) + 1;
let attempts = 0;

function checkGuess(userGuess) {
  attempts++;
  
  if (userGuess === randomNumber) {
    return `Chính xác! Bạn đã đoán sau ${attempts} lần.`;
  } else if (userGuess < randomNumber) {
    return 'Quá thấp! Thử số lớn hơn.';
  } else {
    return 'Quá cao! Thử số nhỏ hơn.';
  }
}
```

### 6. Trình phát nhạc đơn giản (Music Player)

**Độ khó**: ⭐⭐ Trung bình  
**Thời gian**: 3-4 giờ

**Mục tiêu học tập:**
- HTML5 Audio API
- Play/Pause control
- Progress bar
- Event listeners

**Tính năng gợi ý:**
- Play, Pause, Next, Previous
- Progress bar và seek
- Volume control
- Hiển thị thời gian (current/duration)
- Playlist với nhiều bài hát

**Code cơ bản:**
```javascript
const audio = new Audio('song.mp3');

function togglePlay() {
  if (audio.paused) {
    audio.play();
  } else {
    audio.pause();
  }
}

audio.addEventListener('timeupdate', () => {
  const progress = (audio.currentTime / audio.duration) * 100;
  progressBar.style.width = progress + '%';
});
```

### 7. Ứng dụng Quiz (Quiz App)

**Độ khó**: ⭐⭐ Trung bình  
**Thời gian**: 3-5 giờ

**Mục tiêu học tập:**
- Array methods
- Object manipulation
- Score tracking
- Multi-page navigation

**Tính năng gợi ý:**
- Hiển thị câu hỏi và đáp án
- Kiểm tra đáp án đúng/sai
- Tính điểm
- Progress bar
- Kết quả cuối cùng với % đúng
- Nút làm lại

**Cấu trúc dữ liệu:**
```javascript
const quizData = [
  {
    question: "JavaScript là ngôn ngữ gì?",
    answers: {
      a: "Lập trình",
      b: "Markup",
      c: "Styling",
      d: "Database"
    },
    correct: "a"
  },
  // Thêm câu hỏi khác...
];
```

### 8. Bộ đếm ngược thời gian (Countdown Timer)

**Độ khó**: ⭐⭐ Trung bình  
**Thời gian**: 2-3 giờ

**Mục tiêu học tập:**
- Date và Time calculations
- setInterval/clearInterval
- Input validation
- Timer logic

**Tính năng gợi ý:**
- Đặt thời gian đếm ngược
- Start, Pause, Reset
- Hiển thị giờ:phút:giây
- Âm thanh khi hết giờ
- Lưu nhiều timer

**Logic đếm ngược:**
```javascript
function startCountdown(duration) {
  let timer = duration;
  
  const interval = setInterval(() => {
    const hours = Math.floor(timer / 3600);
    const minutes = Math.floor((timer % 3600) / 60);
    const seconds = timer % 60;
    
    display.textContent = `${hours}:${minutes}:${seconds}`;
    
    if (--timer < 0) {
      clearInterval(interval);
      alert('Hết giờ!');
    }
  }, 1000);
}
```

### 9. Form đăng ký có kiểm tra dữ liệu (Form Validation)

**Độ khó**: ⭐⭐ Trung bình  
**Thời gian**: 2-3 giờ

**Mục tiêu học tập:**
- Form handling
- Regular expressions (RegEx)
- Input validation
- Error messages
- UX/UI feedback

**Tính năng gợi ý:**
- Kiểm tra email hợp lệ
- Độ dài password (min 8 ký tự)
- Xác nhận password khớp
- Kiểm tra số điện thoại
- Hiển thị lỗi real-time
- Disable submit nếu không hợp lệ

**Validation examples:**
```javascript
function validateEmail(email) {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
}

function validatePassword(password) {
  return password.length >= 8;
}

function validateForm() {
  const email = document.getElementById('email').value;
  const password = document.getElementById('password').value;
  
  if (!validateEmail(email)) {
    showError('email', 'Email không hợp lệ');
    return false;
  }
  
  if (!validatePassword(password)) {
    showError('password', 'Password phải có ít nhất 8 ký tự');
    return false;
  }
  
  return true;
}
```

### 10. Gallery ảnh với filter (Image Gallery)

**Độ khó**: ⭐⭐ Trung bình  
**Thời gian**: 3-4 giờ

**Mục tiêu học tập:**
- CSS Grid/Flexbox
- Filter và Sort
- Lightbox/Modal
- Animation

**Tính năng gợi ý:**
- Hiển thị grid ảnh
- Filter theo category
- Search box
- Click để xem full size (Lightbox)
- Next/Previous trong lightbox
- Lazy loading

**Filter logic:**
```javascript
const images = [
  { url: 'image1.jpg', category: 'nature' },
  { url: 'image2.jpg', category: 'city' },
  { url: 'image3.jpg', category: 'nature' },
  // ...
];

function filterImages(category) {
  const filtered = category === 'all' 
    ? images 
    : images.filter(img => img.category === category);
  
  displayImages(filtered);
}
```

## Lộ trình thực hiện

Để học hiệu quả, bạn nên theo lộ trình sau:

1. **Bắt đầu từ dễ đến khó**: Làm dự án 1, 5 trước để làm quen
2. **Hoàn thành một dự án trước khi chuyển sang dự án khác**
3. **Không copy code**: Tự code và tham khảo khi bí
4. **Thêm tính năng riêng**: Sáng tạo và custom theo ý tưởng của bạn
5. **Deploy lên web**: Sử dụng GitHub Pages, Netlify, hoặc Vercel
6. **Xin feedback**: Chia sẻ với cộng đồng và học hỏi

## Tips khi làm dự án

### 1. Break down thành tasks nhỏ
Đừng cố làm hết mọi thứ cùng lúc. Ví dụ với To-do List:
- [ ] Tạo HTML structure
- [ ] Style với CSS
- [ ] Thêm task mới
- [ ] Xóa task
- [ ] Đánh dấu hoàn thành
- [ ] Lưu vào LocalStorage

### 2. Google là bạn tốt nhất
Gặp lỗi? Search trên Google với từ khóa cụ thể. Các nguồn hữu ích:
- MDN Web Docs
- Stack Overflow
- JavaScript.info
- W3Schools

### 3. Console.log() is your friend
Debug bằng cách in ra giá trị biến:
```javascript
console.log('Current value:', myVariable);
console.log('Function called with:', argument);
```

### 4. Version control với Git
Commit code thường xuyên để dễ quay lại khi có lỗi:
```bash
git add .
git commit -m "Add delete functionality"
```

### 5. Responsive design
Luôn test trên mobile, tablet, desktop. Sử dụng:
- Media queries
- Flexbox/Grid
- Mobile-first approach

## Tài nguyên hữu ích

### Thiết kế UI/UX
- **Figma Community**: Tìm design inspiration
- **Dribbble**: Xem các design đẹp
- **Color Hunt**: Phối màu đẹp

### Icons và images
- **Font Awesome**: Icon miễn phí
- **Unsplash**: Ảnh chất lượng cao
- **Flaticon**: Icon đa dạng

### Hosting miễn phí
- **GitHub Pages**: Đơn giản, nhanh
- **Netlify**: Auto deploy từ Git
- **Vercel**: Tốt cho React/Next.js

## Kết luận

Làm dự án là cách tốt nhất để học JavaScript. 10 dự án trên sẽ giúp bạn:

✅ Hiểu sâu về JavaScript  
✅ Làm quen với DOM manipulation  
✅ Thực hành với API  
✅ Xây dựng portfolio  
✅ Tự tin hơn khi code  

**Bắt đầu ngay hôm nay!** Chọn một dự án đơn giản, mở code editor lên và bắt tay vào làm. Đừng ngại sai, vì mỗi lỗi bạn gặp là một bài học quý giá.

Chúc bạn coding vui vẻ! 🚀

---

**Bạn đã làm dự án JavaScript nào chưa?** Hãy chia sẻ trải nghiệm của bạn trong phần comment nhé!
