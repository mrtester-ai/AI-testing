# Web UI Testing (Reference)

**Owner:** `web-api-and-integration-testing`.

## Functional Behavior

Validate relevant: navigation · forms · buttons · links · validation · search · sorting · filtering · pagination · state transitions · modals · notifications · error messages · success messages.

## UI States

Initial · loading · empty · populated · success · error · retry · disabled · read-only · expired session.

## Repeated User Actions

Double click · repeated submission · refresh · back · forward · multiple tabs · reopen · re-login.

Verify repeated actions do not create duplicate or inconsistent transactions.

## Responsive Behavior

Validate supported desktop / tablet / mobile / viewports / orientation. Check for cut-off content, overlap, overflow, hidden controls, broken navigation, unusable layouts.

## Browser Compatibility

Test supported browser combinations based on product requirements (e.g. Chrome, Edge, Safari, Firefox). Do not imply support for a browser unless the requirements define it.

## Accessibility

Where relevant validate: keyboard navigation · tab order · visible focus · accessible names · form labels · error identification · semantic controls · zoom behavior · text scaling · color contrast. Use the agreed standard (e.g. WCAG) when defined.

## Browser Developer Tools

**Console:** JavaScript errors · unhandled exceptions · failed resources · security warnings. A console error is evidence, not necessarily the root cause.

**Network:** request URL · method · status · request/response headers · request/response body · timing · redirects · failed requests.

**Storage:** cookies · session storage · local storage. Do not disclose sensitive authentication information.
