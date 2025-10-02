# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: contract tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have tests?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Single project**: `src/`, `tests/` at repository root
- **Web app**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` or `android/src/`
- Paths shown below assume single project - adjust based on plan.md structure

## Phase 3.1: Setup
- [ ] T001 Create project structure per implementation plan
- [ ] T002 Initialize [language] project with [framework] dependencies  
- [ ] T003 [P] Configure linting and formatting tools (ESLint, Prettier)
- [ ] T004 [P] Setup responsive design breakpoints and CSS framework
- [ ] T005 [P] Configure build tools for performance optimization (Vite/Webpack)
- [ ] T006 [P] Setup PWA manifest and service worker configuration
- [ ] T007 [P] Configure accessibility testing tools (axe-core, lighthouse-ci)

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**
- [ ] T008 [P] Contract test POST /api/users in tests/contract/test_users_post.py
- [ ] T009 [P] Contract test GET /api/users/{id} in tests/contract/test_users_get.py
- [ ] T010 [P] Integration test user registration in tests/integration/test_registration.py
- [ ] T011 [P] Integration test auth flow in tests/integration/test_auth.py
- [ ] T012 [P] Responsive design tests across breakpoints in tests/e2e/responsive.test.js
- [ ] T013 [P] Accessibility tests (WCAG 2.1 AA) in tests/a11y/accessibility.test.js
- [ ] T014 [P] Performance tests (Core Web Vitals) in tests/performance/lighthouse.test.js
- [ ] T015 [P] PWA functionality tests in tests/pwa/service-worker.test.js

## Phase 3.3: Core Implementation (ONLY after tests are failing)
- [ ] T016 [P] Responsive component library setup in frontend/src/components/
- [ ] T017 [P] User model in backend/src/models/user.py
- [ ] T018 [P] UserService CRUD in backend/src/services/user_service.py
- [ ] T019 [P] React components with mobile-first design in frontend/src/components/
- [ ] T020 POST /api/users endpoint in backend/src/api/
- [ ] T021 GET /api/users/{id} endpoint in backend/src/api/
- [ ] T022 Frontend form validation with accessibility support
- [ ] T023 Service worker implementation for offline functionality
- [ ] T024 Input validation and sanitization (client + server)
- [ ] T025 Error handling with user-friendly messages

## Phase 3.4: Integration
- [ ] T026 Connect UserService to DB with proper connection pooling
- [ ] T027 JWT-based auth middleware with refresh tokens
- [ ] T028 Structured logging with request tracing
- [ ] T029 Security headers (CSP, HSTS, CORS) configuration
- [ ] T030 Frontend-backend API integration with error boundaries
- [ ] T031 Progressive Web App integration (manifest, icons, themes)
- [ ] T032 Cross-browser compatibility testing and polyfills

## Phase 3.5: Polish
- [ ] T033 [P] Unit tests for validation in tests/unit/test_validation.py
- [ ] T034 [P] Component unit tests with React Testing Library
- [ ] T035 Performance optimization (bundle splitting, lazy loading)
- [ ] T036 Lighthouse audit and Core Web Vitals optimization
- [ ] T037 [P] Accessibility audit and ARIA label verification
- [ ] T038 [P] Update docs/api.md and component documentation
- [ ] T039 [P] Storybook documentation for component library
- [ ] T040 Cross-device testing (mobile, tablet, desktop)
- [ ] T041 Remove code duplication and optimize bundle size
- [ ] T042 Run manual-testing.md across all supported browsers

## Dependencies
- Setup (T001-T007) before tests (T008-T015)
- Tests (T008-T015) before implementation (T016-T025)  
- T017 blocks T018, T026
- T023 requires T004-T006 (PWA config)
- T027 blocks T029, T030
- Implementation before integration (T026-T032)
- Integration before polish (T033-T042)

## Parallel Example
```
# Launch T008-T015 together (all test files):
Task: "Contract test POST /api/users in tests/contract/test_users_post.py"
Task: "Contract test GET /api/users/{id} in tests/contract/test_users_get.py"  
Task: "Integration test registration in tests/integration/test_registration.py"
Task: "Integration test auth in tests/integration/test_auth.py"
Task: "Responsive design tests in tests/e2e/responsive.test.js"
Task: "Accessibility tests in tests/a11y/accessibility.test.js"
Task: "Performance tests in tests/performance/lighthouse.test.js"
Task: "PWA functionality tests in tests/pwa/service-worker.test.js"
```

## Notes
- [P] tasks = different files, no dependencies
- Verify tests fail before implementing
- Commit after each task
- Avoid: vague tasks, same file conflicts

## Task Generation Rules
*Applied during main() execution*

1. **From Contracts**:
   - Each contract file → contract test task [P]
   - Each endpoint → implementation task
   
2. **From Data Model**:
   - Each entity → model creation task [P]
   - Relationships → service layer tasks
   
3. **From User Stories**:
   - Each story → integration test [P]
   - Quickstart scenarios → validation tasks

4. **Ordering**:
   - Setup → Tests → Models → Services → Endpoints → Polish
   - Dependencies block parallel execution

## Validation Checklist
*GATE: Checked by main() before returning*

- [ ] All contracts have corresponding tests
- [ ] All entities have model tasks
- [ ] All tests come before implementation
- [ ] Parallel tasks truly independent
- [ ] Each task specifies exact file path
- [ ] No task modifies same file as another [P] task