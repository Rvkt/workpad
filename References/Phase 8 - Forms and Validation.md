# Phase 8 — Forms and Validation

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]]. Previous: [[Phase 7 - Authentication and Session Lifecycle]]. Next: [[Phase 9 - Feature Development]].

**Objective:** Standardize form handling across the application.

### Tasks

- Install React Hook Form.
- Install Zod and the React Hook Form resolver.
- Create reusable form inputs.
- Define schemas for each form.
- Validate data before submission.
- Map backend field errors to form fields.
- Handle submission loading states.
- Prevent accidental duplicate submissions.
- Implement keyboard and focus behavior.
- Handle accessibility labels and validation messages.

### Example schema

```
import { z } from 'zod';

export const loginSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
});

export type LoginInput = z.infer<typeof loginSchema>;
```

Adjust validation rules to match the backend contract. Client-side validation improves UX but does not replace backend validation.

### Exit criteria

- Forms have typed values.
- Validation errors are clear.
- Backend errors are displayed correctly.
- Submission states are handled consistently.

**Deliverable:** Reusable form infrastructure.
