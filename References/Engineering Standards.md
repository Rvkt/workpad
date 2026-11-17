# Engineering Standards

Part of [[Flutter Roadmap - Index|Senior Flutter Developer Roadmap]]. Apply these standards throughout the roadmap, especially in [[Phase 6 - Code Quality, CI-CD and Senior Engineering]].

## Code Quality

- [ ] Keep business logic outside widgets.
- [ ] Avoid unnecessary abstractions.
- [ ] Prefer immutable state.
- [ ] Use meaningful naming.
- [ ] Avoid oversized widgets and providers.
- [ ] Handle asynchronous failures explicitly.
- [ ] Keep dependencies injectable.
- [ ] Avoid circular dependencies.

## Testing

- [ ] Test business-critical logic.
- [ ] Test repository behavior.
- [ ] Test asynchronous states.
- [ ] Test network failures.
- [ ] Test authentication flows.
- [ ] Test important user journeys.
- [ ] Keep tests deterministic.
- [ ] Avoid depending on live external APIs in unit tests.

## Performance

- [ ] Profile before optimizing.
- [ ] Avoid unnecessary widget rebuilds.
- [ ] Use lazy rendering for large collections.
- [ ] Dispose resources correctly.
- [ ] Avoid blocking the UI isolate.
- [ ] Optimize images and expensive computations.
- [ ] Measure actual performance improvements.

## Security

- [ ] Never hardcode secrets.
- [ ] Avoid logging sensitive information.
- [ ] Protect authentication sessions.
- [ ] Handle token refresh safely.
- [ ] Validate untrusted inputs.
- [ ] Review third-party dependencies.
- [ ] Apply platform-specific security controls.
