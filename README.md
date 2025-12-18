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

### Development Workflow

**Option 1: Maintain Separate Development Files (Recommended)**

1. **Create unobfuscated versions**: Save readable code as:
   - `app.dev.js` - Main dashboard application
   - `report.dev.js` - Report page functionality
   
   Use descriptive names:
   - `firebaseConfig` instead of `_cfg` or `_c`
   - `database` instead of `_db`
   - `elements` instead of `_el`
   - `currentUser` instead of `_user`

2. **During development**:
   - Edit `app.dev.js` and `report.dev.js` with readable code
   - Update HTML files temporarily:
     ```html
     <!-- In index.html -->
     <script src="app.dev.js"></script>
     
     <!-- In report.html -->
     <script src="report.dev.js"></script>
     ```
   - Test all functionality

3. **Before deployment**:
   - Obfuscate both files (see methods below)
   - Restore HTML to use `app.js` and `report.js`
   - Test obfuscated versions

**Option 2: Use Git Branches**

```bash
# Development branch - readable code
git checkout -b development
# Keep app.js and report.js readable

# Production branch - obfuscated code
git checkout main
# Contains obfuscated versions
```

### Obfuscation Methods

**Manual Obfuscation (Current Method)**
- Rename variables to short names (`_0x`, `_cfg`, `_db`, `_el`)
- Split Firebase config into string arrays
- Remove whitespace and comments
- Combine statements on single lines

**Automated Obfuscation Tools**

1. **JavaScript Obfuscator (Online)**: https://obfuscator.io/
   - Paste your readable code
   - Settings: String Array Encoding, Control Flow Flattening
   - Copy output to respective file

2. **JavaScript Obfuscator (CLI)**:
   ```bash
   npm install -g javascript-obfuscator
   
   # Obfuscate main app
   javascript-obfuscator app.dev.js --output app.js \
     --compact true \
     --control-flow-flattening true \
     --string-array true
   
   # Obfuscate report page
   javascript-obfuscator report.dev.js --output report.js \
     --compact true \
     --control-flow-flattening true \
     --string-array true
   ```

3. **Terser (Minification)**:
   ```bash
   npm install -g terser
   terser app.dev.js -o app.js --compress --mangle
   terser report.dev.js -o report.js --compress --mangle
   ```

### Unobfuscating for Development

**To work on existing obfuscated code:**

1. **Restore from backup**: If you have `.dev.js` files, use those
2. **Manual deobfuscation**: 
   - Expand variable names to meaningful ones
   - Add proper indentation and line breaks
   - Add comments explaining logic
   - Reconstruct Firebase config object
3. **Use version control**: Check out development branch with readable code

**Important**: Never edit `app.js` or `report.js` directly if they're obfuscated. Always maintain readable versions for development.

### Files to Obfuscate
- `app.js` - Main teacher dashboard (authentication, test loading, results display)
- `report.js` - Student report page (detailed question-by-question results)