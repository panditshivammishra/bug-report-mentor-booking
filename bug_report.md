# Bug Report: Mentor Booking Flow — UI Modal Issue

---

## Q1. What Went Wrong?

1. **View Profile not opening the sidebar** — On clicking **View Profile** in the mentor listing, the sidebar was not opening.

2. **Book 1:1 Session not opening the modal** — On clicking **Book 1:1 Session**, the modal was not opening where the user selects the type of mentorship they want to go with and proceeds with bookings.

3. **User unable to book mentorship** — Because of the above errors, the user was not able to book a mentorship session.

---

## Q2. Why It Went Wrong?

### Bug: Swapped Modal Rendering Conditions in `layout.tsx`

A developer swapped the controlling flags for two modals in `layout.tsx` / `HomeClient.tsx`.

#### ❌ Incorrect (what the developer wrote):

```tsx
{showModal ? <MentorDetailedProfile /> : null}
{openSheet ? <QueryModal /> : null}
```

#### ✅ Correct (what it should be):

```tsx
{openSheet ? <MentorDetailedProfile /> : null}
{showModal ? <QueryModal /> : null}
```

### Explanation

| Flag | Intended Component | Incorrectly Rendered |
|---|---|---|
| `openSheet` | `MentorDetailedProfile` (sidebar) | `QueryModal` |
| `showModal` | `QueryModal` (booking modal) | `MentorDetailedProfile` |

Because `showModal` was used to control `MentorDetailedProfile` and `openSheet` was used to control `QueryModal`, both components rendered under the wrong conditions — causing neither to appear when triggered by the user.


# Learnings & ToDos

1. **Test properly before merging** — Always test all flows thoroughly before merging to ensure nothing is broken.

2. **Understand AI-generated code before committing** — If we are using AI to write code, always try to understand the generated changes and check that they are not altering an already existing flow.



# Was the PR peer reviewed before making to prod?



# Could this have been tested better?