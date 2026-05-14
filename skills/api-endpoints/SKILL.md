---
description: Guides the creation of new API endpoints. Use when adding routes, handlers, or controllers to the project.
---

## Route File Location

Place all route files under `src/routes/`. Each resource gets its own file named after the resource in kebab-case (e.g., `src/routes/user-profiles.ts`). Register the router in `src/routes/index.ts`.

## Naming Conventions

- **Files:** kebab-case matching the resource (`orders.ts`, `order-items.ts`)
- **Router variables:** camelCase resource name + `Router` (`ordersRouter`, `orderItemsRouter`)
- **Handler functions:** verb + PascalCase resource (`getUser`, `createOrder`, `deleteSession`)
- **URL paths:** lowercase, plural, hyphen-separated (`/order-items`, `/user-profiles`)

## Error Handling Pattern

All errors must go through the centralized error handler. Throw typed errors inside handlers — do not send responses directly from catch blocks.

```ts
import { AppError } from '../errors/AppError';

export async function getUser(req: Request, res: Response, next: NextFunction) {
  try {
    const user = await userService.findById(req.params.id);
    if (!user) throw new AppError(404, 'User not found');
    res.json({ data: user });
  } catch (err) {
    next(err);
  }
}
```

## Response Shape

Every response must follow this envelope:

```json
{ "data": <payload> }
```

Errors are returned by the central handler in this shape:

```json
{ "error": { "status": 404, "message": "User not found" } }
```

Never return a bare object or array at the top level.

## What Must Be Present Before Committing

- [ ] Route file exists under `src/routes/` and is registered in `src/routes/index.ts`
- [ ] All handlers call `next(err)` on failure — no raw `res.status().json()` in catch blocks
- [ ] Every success response uses the `{ data: ... }` envelope
- [ ] Input validated at the boundary (query params, body, path params) before reaching service layer
- [ ] New route covered by at least one integration test
