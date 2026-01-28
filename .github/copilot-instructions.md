# Dentallabor Kobelt — AI Coding Instructions

## Project Overview
Single-page marketing website for a German dental lab (Zahntechnik). Built as static HTML with Tailwind CSS and Formspree for contact form submissions. Targets dentists and patients in the Nuremberg region.

**Domain**: dentallabor-kobelt.de  
**Key Goal**: Showcase digital + analog dental services professionally  
**Main Component**: [index.html](index.html) (842 lines, fully self-contained)

---

## Architecture & Content Structure

### Single-Page Layout (Anchor-Based Navigation)
The site uses CSS anchor IDs for smooth scrolling navigation:
- `#start` – Hero section with value prop ("Wir schenken Ihr Lächeln zurück")
- `#ueber-uns` – About craftsman Erdenejargal Kobelt (17+ years experience)
- `#leistungen` – Services overview (splits into #digitale-leistungen & #analoge-leistungen)
- `#team` – Team & lab equipment details
- `#kontakt` – Contact form + map

**Navigation Pattern**: Desktop nav uses dropdown for Leistungen; mobile menu (toggle via `#menuBtn`) mirrors links.

### Service Categories (Dual Workflow)
The business emphasizes **Digital (CAD/CAM, 3D-Druck) + Analog (Traditional Handwerk)** balance:

**Digital Services** (9 collapsible `<details>` cards):
- Digitale Dienstleistungen, CAD/CAM-Zahnersatz, 3D-Druck, Herausnehmbarer Zahnersatz, Schienen & KFO, Provisorische Versorgungen, Implantologische Leistungen, Ästhetische Arbeiten

**Analog Services** (9 collapsible `<details>` cards):
- Klassische Modellherstellung, Festsitzender Zahnersatz, Herausnehmbarer Zahnersatz, Kombinierter Zahnersatz, Implantatbezogene Arbeiten, Schienen, Provisorien, Ästhetische Laborarbeiten, Manuelle Zusatzleistungen

Each card uses `<details>` with list items (bulleted by `.flex gap-2` + pseudo-element dots). Services are **NOT dynamically loaded** — all content is hardcoded.

---

## Design System & Styling

### Brand Colors (Tailwind Custom Config)
- **`brand: '#2B3549'`** – Dark blue-gray (primary text)
- **`brandSoft: '#F5F5F4'`** – Off-white (backgrounds, highlights)
- **`brandGold: '#D6B977'`** – Light gold (hover states)
- **`brandGoldDark: '#B89A5A'`** – Dark gold (CTA buttons, accents)
- **`brandGray: '#8A8F98'`** – Medium gray (secondary text)

### Key CSS Patterns
- **Sticky header**: `sticky top-0 z-20 bg-white/80 backdrop-blur` with glass effect
- **Gradient sections**: Hero uses `from-[#F5F5F4] via-[#EFE8DA] to-[#E1D6C2]`
- **Cards**: Rounded corners (`rounded-2xl`, `rounded-3xl`), soft borders (`border-slate-100/80`), subtle shadows
- **Animations**: Uses AOS (Animate On Scroll) library — `data-aos="fade-right"`, `fade-left`, `fade-up`
- **Mobile-first**: `hidden md:flex` for desktop nav, hamburger button on mobile

### Typography
- Font: Inter (Google Fonts, weights 300–700)
- Sizes: `text-3xl`/`md:text-4xl` for h1, `text-lg`/`md:text-xl` for section h4
- Hierarchy: Uppercase labels use `tracking-[0.25em]` for accent styling

---

## Form Integration

### Contact Form (Formspree)
- **Action**: `https://formspree.io/f/xwpyzawp`
- **Method**: POST with FormData (fetch API, not traditional form submission)
- **Fields**: name, email, praxis (optional), message
- **Feedback**: Client-side JS alerts on success/failure; form resets on successful submission
- **No backend required** — Formspree handles email delivery

**Handler Location**: Bottom of `index.html` in `<script>` tag (event listener on `.contact-form`)

---

## Development & Editing Conventions

### When Adding/Updating Content:
1. **Service Cards**: Edit the `<details>` list items — do NOT change structure (maintain consistency between Digital/Analog sections)
2. **Color References**: Use Tailwind class names (e.g., `text-brandGoldDark`) instead of hardcoding hex values
3. **External Assets**: Keep images in `/images/` folder; reference with relative paths (`images/logo.jpg`)
4. **Meta Tags**: Update `<meta>` tags in `<head>` for SEO (description, og:*, twitter:*) when content changes
5. **Smooth Scrolling**: Always add `id` attributes to new sections for anchor navigation

### AOS Animation Setup:
- Add `data-aos="fade-right"` (or fade-left/fade-up) to elements needing animation
- AOS is initialized once at footer with `duration: 700`, `easing: 'ease-out-cubic'`, `once: true`
- Do NOT reinitialize AOS if you add new animated elements (library auto-detects)

### Mobile Responsiveness:
- Use Tailwind's responsive prefixes: `md:` (768px+), `lg:` (1024px+)
- Test hamburger menu toggle functionality when modifying nav structure
- Ensure `max-w-6xl` constraint applied to all main sections for consistent gutters

---

## Key Files & Imports
- **[index.html](index.html)** – Single source of truth (Tailwind CDN, AOS CDN, custom config inline)
- **[CNAME](CNAME)** – DNS record: `dentallabor-kobelt.de`
- **[images/](images/)** – `logo.jpg`, `meister.png`, `Wt6CIH7t1f9SOb3g46K28.png` (lab/hero photo)
- No build step, no framework — purely static HTML + CDN

---

## Common Edits
- **Change service list**: Find the `<details>` card, modify `<li>` items
- **Update contact info**: Search "Steuerwald-Landmann-Straße" section
- **Modify colors**: Update Tailwind config object in `<head>` script tag
- **Add new section**: Follow existing pattern: section ID, `max-w-6xl` wrapper, responsive grid, AOS animations
- **Fix responsive issues**: Adjust Tailwind prefixes (`md:`, `lg:`) or padding (`px-4`, `py-20`)

---

## Quality Checklist for Changes
✓ All links navigate to correct anchor IDs  
✓ Images load (use relative paths, not absolute URLs)  
✓ Contact form submits without errors (test Formspree integration)  
✓ Mobile menu opens/closes correctly  
✓ Color contrast meets WCAG standards (especially `text-brandGold` on light backgrounds)  
✓ No hardcoded hex colors — use brand variable names  
✓ German language & tone consistent with brand voice  
✓ AOS animations trigger on scroll (test by opening DevTools)
