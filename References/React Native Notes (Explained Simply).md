Part of [[React Native Roadmap - Index|React Native Mastery Roadmap]].

# React Native Notes (Explained Simply)

These are plain-English study notes to go along with the roadmap checklist. The checklist tells you *what* to do. This file explains *what it actually means* and *why it matters*, in simple words.

---

## Phase 1: Project Initialization

Before you can build an app, you need a working "workshop" set up on your computer. That's what this phase is about: installing the right tools so you can actually write and run React Native code.

Node.js is a program that lets your computer run JavaScript outside of a web browser — almost all the tools you'll use (like Expo) are built on it. Expo is a toolkit that makes building React Native apps much easier: it handles a lot of the painful native Android/iOS setup for you, so you can focus on writing your app. Android Studio is needed because it comes with the Android emulator (a fake Android phone that runs on your computer) and the Android SDK (a set of tools and libraries needed to build and run Android apps).

The reason you test on Android, iOS, and web right away, instead of waiting, is simple: React Native apps are supposed to run on all three from one shared codebase. If something is broken on one platform, you want to know on day one, not after you've built fifty screens.

By the end of this phase, you should just be able to start the app and see it running — that's the whole goal, nothing fancy yet.

---

## Phase 2: TypeScript, Code Quality and Project Structure

This phase is about organizing your house before you move furniture in. If you start writing features without a plan for where things go, your code turns into a mess very quickly.

TypeScript is JavaScript with an added safety net: it lets you say "this variable should always be a number" or "this function always returns a list of users," and it will warn you before you even run the code if you break that rule. "Strict mode" just means turning that safety net up to maximum — it catches more mistakes, which saves you time later even though it feels stricter upfront.

ESLint and code formatters are tools that automatically check your code style and fix small issues (like inconsistent spacing) so that everyone's code looks the same, and so obvious mistakes get caught automatically instead of being found by a human later.

The folder structure (screens, features, services, stores, etc.) is just an agreement on "where things live." For example, "services" holds code that talks to the internet, "stores" holds shared app data, and "features" holds the actual pieces of your product (like a login feature or a profile feature). Having this agreement means that when you open any React Native project built this way, you already know where to look for things.

---

## Phase 3: Navigation and Application Shell

Navigation is simply how a user moves between screens — tapping a button to go from the home screen to a profile screen, for example. Expo Router is the tool used here to manage that movement, and it works similarly to how websites use URLs: each screen can have its own "address."

An "application shell" is the surrounding structure of your app — the parts that stay the same no matter which screen you're on, like a header, or the logic that decides "should this user see the login screen or the main app?" Think of it like the frame of a house: the rooms (screens) change, but the frame holds it all together.

"Route groups" just means organizing your screens into folders like "auth" (login, register) and "app" (dashboard, settings), so logged-out users and logged-in users see different sets of screens. This matters because you don't want someone who isn't logged in to accidentally land on a page meant only for logged-in users.

On web, things behave a bit differently than on mobile — people expect the browser's back button and refreshing the page to work properly, so this phase also makes sure those "web-like" behaviors don't break.

---

## Phase 4: UI Foundation and Design System

"UI" means user interface — basically everything the user sees and taps: buttons, text boxes, loading spinners. Instead of building a new button from scratch every time you need one, this phase is about building a small set of reusable pieces (a button component, a text input component, etc.) that you use everywhere in the app.

A "design system" is just a consistent set of rules for how things look — what colors to use, how much spacing to leave between elements, what font sizes to use. Having these as reusable "tokens" (named values like `primary-color` or `spacing-medium`) means if you want to change your brand color later, you change it in one place instead of hunting through every screen.

You also build standard ways to show common situations: a loading spinner while something is being fetched, an "empty state" message when there's no data yet (like "You have no messages"), and an "error state" when something goes wrong. Building these once, early, means every feature you build later can just reuse them instead of reinventing them badly each time.

Accessibility here means making sure people using screen readers, larger text, or keyboard navigation can still use your app properly — it's not an afterthought, it's part of building the components correctly from the start.

---

## Phase 5: API Client and Backend Contract

Your app's data (user accounts, products, messages, etc.) typically doesn't live inside the app itself — it lives on a server, and your app asks that server for data over the internet. An "API" (Application Programming Interface) is just the agreed-upon way your app and the server talk to each other — like a shared language.

This phase is about building one central place in your code that handles all that talking, instead of scattering network calls everywhere. Axios is a popular tool (a library) that makes sending these internet requests easier than doing it by hand.

A "backend contract" means agreeing with whoever built the server on things like: what format errors come back in, how pages of data are split up ("pagination"), and how login tokens are checked. If your app doesn't know what shape the server's responses come in, it can't reliably read them.

"Timeouts" mean giving up on a request if the server takes too long to respond, so your app doesn't freeze forever waiting. And it's important to remember that any checks you do in the app (like "is this password long enough?") are just for a better user experience — the real security check must always happen on the server, because a sneaky user could bypass your app entirely and talk to the server directly.

---

## Phase 6: State Management (React Native)

"State" is just a fancy word for "data your app is currently holding onto" — things like the list of products you fetched, whether a menu is open, or what the user typed into a form. The tricky part in any app is figuring out *where* each piece of data should live and *who's responsible* for keeping it up to date.

This phase splits state into two main buckets. First, "server state" — data that actually comes from the backend, like a list of orders. TanStack Query is a tool specifically built to fetch, cache, and refresh this kind of data, including handling loading spinners and errors for you automatically. Second, "client state" — data that only exists in the app itself and isn't tied to the server, like "is dark mode turned on" or "which tab is currently selected." Zustand is a small, simple tool for storing this kind of shared data.

The reason to keep these separate is that mixing them up causes bugs: if you manually copy server data into your own state, it can get out of sync with what's actually on the server. The rule of thumb taught here is: if it came from an API, let TanStack Query own it; if it's just UI preference or app-only data, let Zustand own it.

"Cache invalidation" sounds technical, but it just means: after you change something (like updating your profile), you tell the app "hey, go re-fetch that data because it's now outdated." Without this, your app could show stale, wrong information.

---

## Phase 7: Authentication and Session Lifecycle

Authentication is the process of proving who you are — usually by logging in with an email and password. A "session" is the period of time after you log in during which the app remembers you're logged in, so you don't have to log in again every time you open a screen.

The core idea of a "token" is: instead of sending your password every single time you want to do something, the server gives you a special temporary pass (a token) after you log in once, and the app shows that pass on every request afterward. An "access token" is the short-lived pass used day-to-day, and a "refresh token" is a longer-lived pass used to get a new access token once the old one expires — similar to a temporary visitor badge that needs renewing.

"Secure storage" matters because tokens are sensitive — if someone steals them, they can pretend to be you. So instead of storing them in plain, easily readable storage, the app uses special secure storage built into the phone or browser.

This phase also deals with messy real-world situations: what happens if the token expires while the user is in the middle of using the app (you need to quietly refresh it), what happens if multiple requests try to refresh the token at the same time (you need to prevent them from racing each other and causing bugs), and what happens when a user logs out (you must clear out any data in the app that belonged only to them, so the next person who logs in on the same device doesn't see leftover data).

---

## Phase 8: Forms and Validation

Forms are anywhere a user types something in — login forms, sign-up forms, settings screens. "Validation" means checking that what they typed makes sense before you try to submit it — like making sure an email field actually looks like an email, or a password is long enough.

React Hook Form is a tool that manages all the typing, tracking, and submitting logic of a form so you don't have to hand-write it every time. Zod is a tool for describing what "valid" data looks like (a "schema") — for example, "this field must be text, must look like an email, and must not be empty." Combining the two means your form automatically knows how to validate itself against that description.

A key idea repeated throughout this phase: validating on the app side is just for a nicer, faster experience for the user (instant feedback instead of waiting for the server). It never replaces the server doing its own validation, because the server can never fully trust what the app sends it.

This phase also covers smaller but important details: showing errors that come back from the server next to the right input field, disabling the submit button while a request is in progress (so people don't accidentally submit the same form twice), and making sure form inputs work well with on-screen keyboards on mobile.

---

## Phase 9: Feature Development

Once the foundation (navigation, UI components, API layer, state management, auth, forms) is built, this is where you actually build the real parts of the app — the specific screens and functionality the product needs, like a product catalog, a messaging screen, or a checkout flow.

The key advice here is to build "vertical slices" — meaning, take one single feature and build it completely from start to finish (from talking to the server, to showing it on screen, to handling errors) before moving to the next feature. This is better than building a little bit of every feature at once, because a fully finished feature proves your whole system actually works end-to-end, while ten half-finished features prove nothing and are hard to track.

Each feature typically needs its own small set of files: the API calls specific to that feature, the TypeScript types describing its data, the hooks that fetch/update its data, and the actual screens and components. Keeping each feature's code grouped together (instead of scattering it across generic shared folders) makes it much easier to find, update, or remove a feature later without breaking unrelated parts of the app.

---

## Phase 10: Testing (React Native)

Testing means writing code whose only job is to check that your other code works correctly — automatically, without you manually clicking through the app every time you make a change.

There are different "levels" of tests, like zooming in and out with a camera. Unit tests check the smallest pieces — a single function, like "does this function correctly format a date?" Component tests check a single screen piece, like "does this button show a loading spinner when it's clicked?" Integration tests check that several pieces work together correctly, like "does submitting the login form actually update the stored session?" End-to-end tests simulate a real user going through an entire flow, like signing up, logging in, and placing an order, all in one continuous test.

The reason to write tests at all is that as an app grows, it becomes impossible to manually re-check everything every time you make a change. Tests act like a safety net: if you accidentally break something while adding a new feature, a test will fail and alert you immediately, instead of a real user discovering the bug later.

A good test also doesn't rely on the real, live server — it uses fake ("mocked") responses, so the tests run quickly and reliably without needing an internet connection or a working backend.

---

## Phase 11: Cross-Platform Verification

Even though React Native lets you write one codebase for Android, iOS, and web, the platforms don't behave identically — this phase is about hunting down and checking those differences on purpose, rather than being surprised by them later.

Each platform has its own quirks. Android has a physical/software "back" button that can unexpectedly take users to the wrong screen if navigation isn't handled carefully. iOS has its own permission pop-ups and "safe areas" (parts of the screen blocked by notches or rounded corners) that need extra padding. Web users expect browser behaviors to just work, like refreshing a page without losing their spot, and typing a specific link directly into the browser's address bar.

"Permissions" refers to features like camera, location, or notifications access — each platform asks the user to approve these differently, and your app needs to handle both the "approved" and "denied" cases gracefully.

The point of this phase is simple: don't assume that because something works on your test device, it works everywhere. Testing on all three platforms deliberately, late enough that most features exist but early enough to still fix issues, catches problems that would otherwise reach real users.

---

## Phase 12: Release Preparation Without Deployment Automation

This final phase is about getting the app ready to be shipped out into the world — but importantly, this roadmap stops short of actually automating that shipping process (things like automatic deployment pipelines are intentionally left for later, so you're not overwhelmed trying to learn everything at once).

Before release, you clean up leftover "debug" code — things you added temporarily to help yourself while developing, like console logs showing sensitive information, which should never ship to real users. You also double check configuration: making sure the app is pointing at the real production server address and not your local development one, and that things like app names, icons, and version numbers are correct.

Running the full test suite and type checks one more time here acts as a final safety check before anyone outside the development team touches the app. "Static analysis" just means tools that scan your code for likely mistakes without actually running it — catching issues early and cheaply.

Finally, the deferred items listed (like Sentry, which is a tool for tracking errors that happen in a live app, and CI/CD, which stands for Continuous Integration/Continuous Deployment — automated systems that test and publish your app every time you make a change) are purposely left out of this roadmap's scope. They're real and important for a production app, but they're treated as a separate, later project so that the roadmap doesn't try to teach everything about building, testing, and deploying software all at once.
