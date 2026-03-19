# Contributing to Pageel Page Map

Thank you for your interest in contributing! This project aims to standardize how AI agents understand webpage structure.

## How to Contribute

### Adding Examples

The most impactful contribution is adding PAGE_MAP + BLUEPRINT examples for new layout patterns:

1. Create a new directory under `examples/`:
   ```
   examples/your-layout/
   ├── PAGE_MAP.md
   └── BLUEPRINT.md
   ```

2. Follow the format specification in [`docs/spec.md`](./docs/spec.md).

3. Use the naming convention `[section.subsection]` consistently.

4. Submit a PR with a brief description of the layout pattern.

### Improving the Spec

If you have ideas for improving the format specification:

1. Open an issue describing the proposed change and rationale.
2. Reference any real-world use cases that motivate the change.
3. If accepted, submit a PR updating `docs/spec.md`.

### Framework-Specific Templates

We welcome templates for different frameworks:
- **Astro** — `{/* [section] */}`
- **React/JSX** — `{/* [section] */}`
- **Vue** — `<!-- [section] -->`
- **Svelte** — `<!-- [section] -->`
- **HTML** — `<!-- [section] -->`

### Bug Reports & Feature Requests

Please use [GitHub Issues](https://github.com/pageel/pageel-page-map/issues) for:
- Spec ambiguities or inconsistencies
- Missing examples for common layout patterns
- Integration issues with specific AI agents

## Code of Conduct

Be respectful and constructive. We're building tools to help developers and AI agents collaborate better.

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](./LICENSE).
