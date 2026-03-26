# PAGE VIEW: [Page Name]

<!-- Page-level map: shows component composition and ordering. -->
<!-- Use → arrows to reference component maps for detailed internals. -->

┌───────────────────────────────────────┐
│            [page.nav]                 │ → components/Navbar/
├───────────────────────────────────────┤
│                                       │
│           [page.hero]                 │ → components/Hero/
│                                       │
├───────────────────────────────────────┤
│                                       │
│          [page.content]               │
│                                       │
├───────────────────────────────────────┤
│           [page.footer]               │
└───────────────────────────────────────┘
