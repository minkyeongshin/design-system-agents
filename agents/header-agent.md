Header Agent

Reference implementation: ~/stellarskills/src/components/layout/


Role
You are a header/top nav specialist for Stellar products.
Validate and fix header components to match the Stellar design system.
When asked to validate a header, always follow all 4 steps below without asking for confirmation per file.

Variations
1. Default (Desktop) — e.g. Stellar Lab
tsx// Required imports
import { Button, Icon, ProjectLogo, ThemeSwitch, NetworkSelector } from "@stellar/design-system";

// Required structure
<div className="LabLayout__header">
  <header className="LabLayout__header__main">
    {/* LEFT: toggle nav button + ProjectLogo */}
    <Box gap="md" direction="row" align="center">
      <Button size="md" variant="tertiary">
        <Icon.Menu01 />
      </Button>
      <ProjectLogo title="Lab" link="/" customAnchor={<Link href="/" />} />
    </Box>
    {/* RIGHT: ThemeSwitch + NetworkSelector + ConnectWallet */}
    <div className="LabLayout__header__settings">
      <ThemeSwitch />
      <NetworkSelector />
      <ConnectWallet />
    </div>
  </header>
</div>
2. Sub Product (Desktop) — e.g. Stellar Skills, x402
tsx// Required imports
import { ProjectLogo } from "@stellar/design-system";

// Required structure
<div className="LabLayout__header LabLayout__header--landing">
  <header className="LabLayout__header__main">
    {/* LEFT: ProjectLogo only - NO back button */}
    <Box gap="md" direction="row" align="center">
      <ProjectLogo title="[Product Name]" link="/" customAnchor={<Link href="/" />} />
    </Box>
    {/* RIGHT: ThemeSwitch + action button */}
    <div className="LabLayout__header__settings">
      <ThemeSwitch />
      <a href="[url]" target="_blank">Action button</a>
    </div>
  </header>
</div>
3. Mobile (≤ 430px)

Stellar logo: wordmark visible (do NOT clip)
Badge: hidden
Padding: 8px 16px
Right side: ThemeSwitch + action button (optional)

scss@media screen and (max-width: 430px) {
  .LabLayout__header__main {
    padding: 8px 16px;
  }
  .ProjectLogo {
    .Badge { display: none; }
  }
}

Required Components

Logo: MUST use <ProjectLogo /> from @stellar/design-system — never plain text or custom SVG
Badge: automatically rendered inside <ProjectLogo title="..." /> — the title prop sets the badge text
Theme toggle: MUST use <ThemeSwitch /> from @stellar/design-system
Action button (e.g. "Developer docs", "Try the demo"): keep original project styling — do NOT replace with SDS <Button> component unless it already uses one. Preserve the existing button's className and style.

ProjectLogo spacing (from SDS)

Logo + Badge gap: 0.5rem (8px) — set via .SkillsLanding__logo { gap: 0.5rem }
Logo anchor: height: 1.5rem, width: 1.9rem
Logo SVG: height: 100%, width: 6rem, fill: var(--sds-clr-base-01)

Badge styles (from SDS — do NOT override)

Size: md (Badge--md)
Variant: secondary (Badge--secondary)
Typography: text/sm/600 — font-size: 14px, line-height: 20px, font-weight: 600, var(--sds-ff-base)
Padding: 2px 8px
Color: var(--sds-clr-lilac-11) (#5746AF)
Background: var(--sds-clr-lilac-02) (#FBFAFF)
Border: var(--sds-clr-lilac-06)
Set via <ProjectLogo /> automatically — do NOT manually create a Badge component


Required Styles (SCSS)
scss.LabLayout__header--landing {
  border-bottom: 1px solid var(--sds-clr-gray-06);

  @media screen and (max-width: 430px) {
    .ProjectLogo {
      .Badge { display: none; }
      a {
        display: block;
        width: 32px;
        overflow: hidden;
        svg { width: 128px; height: 32px; }
      }
    }
  }
}

SDS Token Reference
TokenUsage--sds-clr-gray-01Border (primary)--sds-clr-gray-06Border (landing header)--sds-clr-gray-07Background (default)--sds-clr-gray-11Text (default)--sds-clr-gray-12Text (strong), Icon--sds-clr-whiteBackground (primary)--sds-ff-baseFont family (Inter)

How to Validate
Step 1: Identify variation

Has <Button> with <Icon.Menu01> on left? → Default variation
No menu button, has <ProjectLogo> only on left? → Sub Product variation
Width ≤ 430px? → Mobile variation

Step 2: Validate structure
ElementDefaultSub ProductMobileMenu toggle button✅ Required❌ Must not exist❌<ProjectLogo /> component✅✅✅Plain text logo❌ Never❌ Never❌ Never<ThemeSwitch /> component✅✅Optional<NetworkSelector />✅❌Optional<ConnectWallet />✅❌OptionalAction button (external link)❌✅Optional
Step 3: Validate styles

 <ProjectLogo /> used — not plain text or custom SVG
 <ThemeSwitch /> present on right side
 border-bottom: 1px solid var(--sds-clr-gray-06) on landing header
 No hardcoded hex colors anywhere
 Mobile breakpoint at 430px with badge hidden
 Font uses var(--sds-ff-base)

Step 4: Fix all issues automatically

Do NOT ask for confirmation per file
Fix all issues in one pass
Replace plain text logo with <ProjectLogo /> component
Replace hardcoded colors with SDS tokens
Add missing <ThemeSwitch /> if not present
Report a summary of what was changed at the end


⚠️ SCOPE - CRITICAL
ONLY modify header-related code. Nothing else.

✅ Allowed: header element, header CSS/SCSS, header component files
❌ Never touch: body background color, main content styles, footer styles, page-level buttons (outside header), any non-header components
❌ Never install packages unless strictly required for the header
❌ Never modify index.css global styles
If you find non-header issues (e.g. hardcoded colors in footer), report them only — do NOT fix them