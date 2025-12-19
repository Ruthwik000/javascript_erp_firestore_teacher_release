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

### Current State
Both `app.js` and `report.js` are currently **manually obfuscated** using:
- Shortened variable names (`_0x`, `_cfg`, `_db`, `_el`, `_x`, `_c`, etc.)
- String array obfuscation for Firebase configuration
- Minified single-line functions
- Compact code structure

### Obfuscated Symbol Meanings (Development Reference)

**app.js symbols:**
- `_0x` - String array containing Firebase config parts
- `_cfg` - Firebase configuration object (assembled from `_0x`)
- `_db` - Firestore database instance
- `_auth` - Firebase authentication instance
- `_user` - Current authenticated user object
- `_secId` - Current teacher's assigned section ID
- `_secName` - Current teacher's assigned section name
- `_el` - DOM elements object (auth, main, signin, signout, email, secName, tests, refresh)
- `_init()` - Initialize app (get section and load tests)
- `_getSec()` - Get teacher's assigned section from Firestore
- `_loadTests()` - Load all tests for the teacher's section
- `_getRC(tid)` - Get result count for a test (tid = test ID)
- `_viewRes(tid, tname)` - View student results modal (tid = test ID, tname = test name)
- `_getStud()` - Get all students in the teacher's section
- `_calcScore(r)` - Calculate percentage score from result object (r = result)

**report.js symbols:**
- `_0x` - String array containing Firebase config parts
- `_c` - Firebase configuration object
- `_d` - Firestore database instance
- `_t` - Test ID from URL parameter
- `_s` - Student ID from URL parameter
- `_e` - DOM elements object
- `_l()` - Load and display report data
- `_g(c, f)` - Get document from collection (c = collection, f = field/ID)

