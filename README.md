# Teacher Dashboard

## Overview
Web application for teachers to view student test results and share reports via WhatsApp.

## Features
- Google Sign-In authentication
- Automatically loads teacher's assigned section
- View all tests for the section
- See student results for each test
- View detailed student reports (question-by-question)
- Share individual student reports via WhatsApp
- Color-coded results (green=correct, red=wrong)

## Setup
1. Open `index.html` in a web browser
2. Sign in with Google (must use email assigned by school admin)
3. View tests and student results
4. Click "View Report" to see detailed results
5. Click WhatsApp button to share report with student

## Firebase Collections Used
- `teacherAssignments` - Gets teacher's section assignment
- `tests` - Loads tests filtered by sectionId
- `results` - Student test results (Q1, Q2, Q3... with "R" for correct)
- `students` - Student information including phone numbers

## Data Structure
```javascript
// results collection
{
  studentId: "6913169058b48a6faafae246",
  testId: "692ea97189dd07363f2fef38",
  Q1: "R",  // R = correct answer
  Q2: "2",  // number = wrong answer (option selected)
  Q3: "R",
  // ... more questions
}
```

## Report Page
- `report.html` - Standalone page showing detailed test results
- URL format: `report.html?testId=XXX&studentId=YYY`
- Shows all questions with student answers vs correct answers
- Can be printed or shared

## Code Obfuscation
The JavaScript code is minified and obfuscated to prevent easy reverse-engineering.