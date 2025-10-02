<!--
Sync Impact Report:
Version change: [Initial] → 1.0.0
Modified principles: All new principles for responsive web application
Added sections: Core Principles, Technical Standards, Quality Assurance
Removed sections: None
Templates requiring updates: 
✅ Constitution created for responsive web application
✅ Plan template - Constitution Check section updated with web app requirements  
✅ Spec template - Added web application specific clarification areas
✅ Tasks template - Updated with responsive design, PWA, and accessibility tasks
✅ Agent file template - No changes needed (auto-generated from plans)
Follow-up TODOs: 
- Create README.md with project overview and constitution reference
- Set up docs/ directory structure for runtime guidance
- Consider creating quickstart guide for developers
-->

# Event Management Web Application Constitution

## Core Principles

### I. Mobile-First Responsive Design (NON-NEGOTIABLE)
All user interfaces MUST be designed mobile-first with progressive enhancement for larger screens. Breakpoints MUST be defined at 320px (mobile), 768px (tablet), 1024px (desktop), and 1440px (large desktop). Every component MUST be tested and functional across all viewport sizes. Touch targets MUST be minimum 44px for accessibility compliance.

**Rationale**: Modern users access web applications primarily through mobile devices. A mobile-first approach ensures optimal user experience across all devices and improves accessibility.

### II. Performance-First Development
Web pages MUST achieve Lighthouse performance scores of 90+ for mobile and desktop. Core Web Vitals MUST meet Google's thresholds: LCP < 2.5s, FID < 100ms, CLS < 0.1. Bundle sizes MUST be optimized with code splitting, lazy loading, and tree shaking. Images MUST use modern formats (WebP, AVIF) with responsive sizing.

**Rationale**: Performance directly impacts user experience, SEO rankings, and conversion rates. Fast-loading applications improve user retention and accessibility for users on slower networks.

### III. Accessibility-First (WCAG 2.1 AA Compliance)
All features MUST meet WCAG 2.1 AA standards. Semantic HTML MUST be used for all content. ARIA labels and roles MUST be implemented where needed. Color contrast ratios MUST meet 4.5:1 for normal text and 3:1 for large text. Keyboard navigation MUST be fully functional throughout the application.

**Rationale**: Accessibility ensures the application is usable by everyone, including users with disabilities. It's a legal requirement in many jurisdictions and improves overall usability.

### IV. Component-Driven Architecture
User interfaces MUST be built using reusable, self-contained components. Each component MUST have clear props/interfaces, comprehensive documentation, and isolated styling. Components MUST be testable in isolation using tools like Storybook or similar. Design system consistency MUST be maintained across all components.

**Rationale**: Component-driven development promotes consistency, maintainability, and enables efficient collaboration between design and development teams.

### V. Progressive Web App Standards
The application MUST implement PWA features including service workers for offline functionality, web app manifest for installation, and push notifications where appropriate. Critical user flows MUST work offline with appropriate fallback messaging. App shell architecture MUST be implemented for instant loading.

**Rationale**: PWA features provide native app-like experiences while maintaining web accessibility and distribution advantages.

### VI. Security-First Implementation
All user inputs MUST be validated and sanitized on both client and server sides. HTTPS MUST be enforced with appropriate security headers (CSP, HSTS, etc.). Authentication MUST use secure, industry-standard methods (OAuth 2.0, JWT with proper rotation). Sensitive data MUST be encrypted at rest and in transit.

**Rationale**: Security protects user data and maintains trust. Web applications are frequent targets for attacks, making security a foundational requirement.

### VII. Test-Driven Development (NON-NEGOTIABLE)
All features MUST be developed using TDD methodology: Tests written → Requirements verified → Tests fail → Implementation → Tests pass. Unit tests MUST achieve 90%+ code coverage. Integration tests MUST cover critical user journeys. End-to-end tests MUST validate complete user flows across different devices and browsers.

**Rationale**: TDD ensures code quality, reduces bugs, and provides confidence in refactoring. Comprehensive testing is essential for maintaining quality in responsive web applications.

## Technical Standards

### Modern Web Technologies
- **Frontend Framework**: React, Vue.js, or Angular (latest stable versions)
- **CSS Framework**: Tailwind CSS, styled-components, or CSS-in-JS solutions
- **Build Tools**: Vite, Webpack 5+, or Parcel for optimized bundling
- **Browser Support**: Last 2 versions of major browsers (Chrome, Firefox, Safari, Edge)
- **HTTP/2**: MUST be implemented for improved performance
- **TypeScript**: MUST be used for type safety and improved developer experience

### Code Quality Standards
- **Linting**: ESLint with Prettier for consistent code formatting
- **Git Workflow**: Feature branches with pull request reviews
- **Documentation**: JSDoc comments for all public APIs and complex logic
- **Error Handling**: Comprehensive error boundaries and user-friendly error messages
- **Logging**: Structured logging for debugging and monitoring

## Quality Assurance

### Review Process
All code changes MUST undergo peer review focusing on:
- Responsive design implementation across breakpoints
- Performance impact assessment
- Accessibility compliance verification
- Security vulnerability checks
- Test coverage and quality validation

### Deployment Gates
- Automated testing pipeline MUST pass (unit, integration, e2e)
- Performance budgets MUST not be exceeded
- Accessibility audits MUST pass
- Security scans MUST show no high-severity issues
- Cross-browser compatibility MUST be verified

## Governance

This constitution supersedes all other development practices and guidelines. All pull requests and code reviews MUST verify compliance with these principles. Any complexity that violates these principles MUST be justified with detailed reasoning and approved by the team lead.

Amendments to this constitution require:
1. Documented proposal with rationale
2. Team consensus and approval
3. Migration plan for existing code
4. Update of all related templates and documentation

For runtime development guidance, refer to project-specific documentation in the `/docs` directory.

**Version**: 1.0.0 | **Ratified**: 2025-10-02 | **Last Amended**: 2025-10-02