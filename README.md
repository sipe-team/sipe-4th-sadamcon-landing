# SIPE Interactive Landing Page

An interactive landing page built with Vue 3, TypeScript, and GSAP animations featuring:

## Features

- **Interactive SIPE Lego Blocks**: 3D animated letter blocks that form "SIPE"
- **Scroll-triggered Animations**: Smooth animations triggered by scrolling
- **Introduction Section**: Elegant content section with Lorem ipsum text
- **Floating Cards**: Interactive card components with photos, titles, and content
- **Responsive Design**: Works seamlessly across all device sizes

## Tech Stack

- **Vue 3** with Composition API
- **TypeScript** for type safety
- **Vite** for fast development and building
- **GSAP** for smooth animations
- **CSS Grid & Flexbox** for responsive layouts

## Getting Started

1. Install dependencies:
```bash
npm install
```

2. Start the development server:
```bash
npm run dev
```

3. Build for production:
```bash
npm run build
```

4. Preview the production build:
```bash
npm run preview
```

## Project Structure

```
src/
├── components/
│   ├── SipeBlocks.vue      # Interactive SIPE lego blocks
│   ├── IntroSection.vue    # Introduction content section
│   └── FloatingCards.vue   # Floating cards component
├── App.vue                 # Main application component
├── main.ts                 # Application entry point
└── style.css              # Global styles
```

## Animations

The project uses GSAP for smooth, performant animations:
- **Lego blocks**: 3D transforms with elastic easing
- **Scroll triggers**: Intersection Observer API for scroll-based animations
- **Hover effects**: Interactive scaling and rotation
- **Floating animations**: Continuous subtle movements

## Responsive Design

The landing page is fully responsive with:
- Mobile-first design approach
- Flexible grid layouts
- Optimized animations for mobile devices
- Custom scrollbar styling
