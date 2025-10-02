# Quickstart Guide: Agenda Management Application

## Overview
This quickstart guide provides step-by-step validation scenarios to test the core functionality of the agenda management application. Each scenario corresponds to the acceptance criteria defined in the specification.

## Prerequisites
- Backend API server running on http://localhost:3001
- Frontend application running on http://localhost:3000
- Database initialized with schema
- Test data loaded (optional)

## Validation Scenarios

### Scenario 1: Event Creation with Time Slot Generation
**Test**: Verify automatic time slot generation for multi-day events

**Steps**:
1. **Open Event Creation Form**
   - Navigate to http://localhost:3000/events/new
   - Verify responsive layout on mobile (320px), tablet (768px), desktop (1024px)

2. **Create 3-Day Event**
   - Title: "TechConf 2025"
   - Description: "Annual technology conference"
   - Start Date: "2025-10-15"
   - End Date: "2025-10-17"
   - Click "Create Event"

3. **Verify Time Slot Generation**
   - Navigate to event agenda view
   - Confirm 30 time slots generated (10 per day, 8am-6pm)
   - Verify time slots display: 08:00-09:00, 09:00-10:00, ..., 17:00-18:00
   - Check responsive agenda layout across all breakpoints

**Expected Results**:
- Event created successfully with ID
- 30 hourly time slots auto-generated
- Time slots organized by day
- Mobile-first responsive design functional

### Scenario 2: Session Creation and Assignment
**Test**: Create session with speakers, track, and time slot assignment

**Steps**:
1. **Create Speaker First**
   - Navigate to /speakers/new
   - Name: "Jane Smith"
   - Job Title: "Senior Frontend Developer"
   - Company: "TechCorp Inc."
   - Bio: "Frontend expert with 8 years experience"
   - LinkedIn: "https://linkedin.com/in/janesmith"
   - Submit speaker form

2. **Create Track**
   - Navigate to /tracks/new
   - Name: "Frontend Development"
   - Description: "Frontend technologies and best practices"
   - Color: "#3B82F6"
   - Submit track form

3. **Create Session**
   - Navigate to /sessions/new
   - Title: "Building Responsive Web Apps"
   - Description: "Learn modern responsive design techniques"
   - Event: Select "TechConf 2025"
   - Date: "2025-10-15"
   - Time Slot: "09:00-10:00"
   - Track: "Frontend Development"
   - Speakers: Select "Jane Smith"
   - Tags: Add "javascript", "css", "responsive"
   - Submit session form

4. **Verify Session in Agenda**
   - Navigate to event agenda
   - Locate Oct 15, 09:00-10:00 slot
   - Verify session appears with track color
   - Check speaker details display
   - Verify tags are shown

**Expected Results**:
- Session created and assigned to correct time slot
- Speaker information displays with social links
- Track color coding applied
- Tags available for filtering

### Scenario 3: Agenda Filtering by Track
**Test**: Filter sessions by specific track

**Steps**:
1. **Setup Multiple Sessions**
   - Create additional track: "Backend Development" (#EF4444)
   - Create additional session in Backend track
   - Ensure sessions exist in both Frontend and Backend tracks

2. **Apply Track Filter**
   - Navigate to agenda view
   - Click "Filter by Track" dropdown
   - Select "Frontend Development"
   - Verify only Frontend sessions display

3. **Clear Filter**
   - Click "Clear Filters" or "All Tracks"
   - Verify all sessions display again

**Expected Results**:
- Filter shows only sessions from selected track
- Track color coding maintained during filtering
- Clear filter functionality works correctly

### Scenario 4: Speaker Profile Display
**Test**: View speaker details with social links

**Steps**:
1. **Access Speaker from Session**
   - Navigate to agenda view
   - Click on session with speaker "Jane Smith"
   - Click on speaker name/profile

2. **Verify Speaker Details**
   - Name, job title, company displayed
   - Bio text shows with markdown support
   - Profile image displays (if provided)
   - Social links are clickable and functional

3. **Test Social Link Navigation**
   - Click LinkedIn link
   - Verify link opens in new tab
   - Verify URL is correct

**Expected Results**:
- Complete speaker profile displays
- Social links functional and validated
- Professional information clearly presented

### Scenario 5: Tag-Based Session Search
**Test**: Filter sessions using tag system

**Steps**:
1. **Setup Tagged Sessions**
   - Ensure sessions have various tags: "javascript", "css", "python", "api"
   - Create sessions with overlapping and unique tags

2. **Search by Single Tag**
   - Use tag filter/search for "javascript"
   - Verify only sessions with "javascript" tag display

3. **Search by Multiple Tags**
   - Apply multiple tag filters
   - Verify sessions matching any selected tag appear

4. **Clear Tag Filters**
   - Remove all tag filters
   - Verify all sessions display

**Expected Results**:
- Tag filtering works accurately
- Multiple tag selection functions correctly
- Clear filters restores full session list

### Scenario 6: Responsive Agenda View
**Test**: Agenda display across different devices

**Steps**:
1. **Mobile View (320px)**
   - Open agenda on mobile device or resize browser
   - Verify agenda displays in mobile-optimized layout
   - Check session cards stack vertically
   - Ensure touch targets are minimum 44px
   - Test tap interactions on sessions

2. **Tablet View (768px)**
   - Resize to tablet width
   - Verify intermediate layout between mobile and desktop
   - Check session cards display appropriately

3. **Desktop View (1024px+)**
   - Full desktop view
   - Verify time slots display in grid format
   - Check parallel sessions show simultaneously
   - Verify track colors and visual organization

**Expected Results**:
- Responsive design works across all breakpoints
- Touch targets meet accessibility requirements
- Visual hierarchy maintained at all sizes

## Performance Validation

### Page Load Performance
**Test**: Verify performance meets constitutional requirements

**Steps**:
1. **Run Lighthouse Audit**
   - Open Chrome DevTools
   - Navigate to Lighthouse tab
   - Run performance audit on main agenda page
   - Verify scores >= 90 for both mobile and desktop

2. **Core Web Vitals Check**
   - LCP (Largest Contentful Paint) < 2.5s
   - FID (First Input Delay) < 100ms
   - CLS (Cumulative Layout Shift) < 0.1

**Expected Results**:
- Lighthouse performance score >= 90
- Core Web Vitals meet Google thresholds
- Page loads within 2 seconds
- Interactions respond within 500ms

## Accessibility Validation

### WCAG 2.1 AA Compliance
**Test**: Verify accessibility standards

**Steps**:
1. **Keyboard Navigation**
   - Use only keyboard (Tab, Enter, Arrow keys)
   - Navigate through entire agenda
   - Verify all interactive elements accessible
   - Check focus indicators are visible

2. **Screen Reader Testing**
   - Enable screen reader (NVDA, JAWS, or VoiceOver)
   - Navigate agenda structure
   - Verify semantic HTML announcements
   - Check ARIA labels on interactive elements

3. **Color Contrast Check**
   - Use accessibility tools to verify contrast ratios
   - Text contrast >= 4.5:1 for normal text
   - Large text contrast >= 3:1

**Expected Results**:
- Full keyboard accessibility
- Screen reader compatibility
- Color contrast compliance
- Semantic HTML structure

## Error Handling Validation

### Edge Cases
**Test**: System behavior with invalid inputs

**Steps**:
1. **Invalid Event Dates**
   - Try creating event with end date before start date
   - Verify appropriate error message

2. **Session Outside Event Range**
   - Attempt to schedule session outside event date range
   - Verify validation prevents creation

3. **Missing Required Fields**
   - Submit forms with missing required data
   - Verify error messages are clear and helpful

**Expected Results**:
- Input validation prevents invalid data
- Error messages are user-friendly
- System remains stable with invalid inputs

## Completion Checklist

- [ ] All 6 primary scenarios pass
- [ ] Performance requirements met (< 2s load, < 500ms interactions)
- [ ] Responsive design works across all breakpoints (320px, 768px, 1024px)
- [ ] Accessibility standards met (WCAG 2.1 AA)
- [ ] Error handling functions correctly
- [ ] PWA features functional (if implemented)
- [ ] Cross-browser compatibility verified

## Troubleshooting

### Common Issues
- **Time slots not generating**: Check event date validation and backend API
- **Sessions not filtering**: Verify API endpoints and frontend filter logic
- **Responsive layout issues**: Check CSS breakpoints and mobile-first implementation
- **Performance issues**: Review bundle size and optimization strategies
- **Accessibility failures**: Verify semantic HTML and ARIA implementation