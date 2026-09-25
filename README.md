# 📚 Study Time Calculator & Exam Planner

A lightweight, responsive, and fully client-side web application designed to eliminate study overwhelm and help students organize their exam preparation efficiently. Built with performance and usability in mind, this tool offers an exam countdown engine, a daily study hour planner, an integrated Pomodoro session builder, and a reading time estimator.

👉 **Live Demo:** [Study Time Calculator on Global Tools Box](https://www.globaltoolsbox.online/2026/09/study-time-calculator.html)

---

## 🌟 Key Features

* **Exam Countdown & Study Hour Planner:** Calculates exact daily required study hours based on target exam dates, total chapters, and weekly availability.
* **Pomodoro Session Planner:** Automatically breaks down available study time into structured focus sessions and recovery break intervals.
* **Reading Time Estimator:** Predicts total reading duration for textbooks and study modules based on page count and reading speed (WPM).
* **Zero Dependencies & Fast Load:** Built using vanilla web technologies without heavy frameworks to ensure instant loading on low-bandwidth mobile networks.
* **Privacy Focused:** 100% client-side calculation. No personal study data or target dates are ever stored or transmitted to external servers.

---

## 🛠️ Tech Stack & Architecture

* **Frontend:** HTML5, Modern CSS3 (Flexbox/Grid, Responsive Layouts)
* **Scripting:** Pure JavaScript (ES6+)
* **Hosting:** Blogger Architecture with Cloudflare Worker optimization
* **Styling:** Custom lightweight CSS for clean, distraction-free UI

---

## 💡 How It Works

### 1. Daily Study Calculation Logic
The core calculation calculates the active study days available between the current date and the target exam date while accounting for planned days off per week:

```javascript
function calculateDailyHours(examDate, totalTopics, hoursPerTopic, studyDaysPerWeek) {
  const today = new Date();
  const targetDate = new Date(examDate);
  const diffTime = Math.abs(targetDate - today);
  const totalDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
  
  if (totalDays <= 0) return null;

  const totalHoursNeeded = totalTopics * hoursPerTopic;
  const activeStudyDays = Math.floor((totalDays / 7) * studyDaysPerWeek);
  
  const dailyHoursNeeded = (totalHoursNeeded / activeStudyDays).toFixed(1);
  return { totalDays, dailyHoursNeeded };
}
