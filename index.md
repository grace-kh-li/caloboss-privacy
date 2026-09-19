---
title: CaloBoss Privacy Policy
---

<!-- This is the source of truth. The copy the App Store points at is published
     at https://grace-kh-li.github.io/caloboss-privacy/ — run
     scripts/publish-privacy.sh after changing anything here, or the public page
     will quietly describe an older version of the app. -->

# CaloBoss — Privacy Policy

**Last updated: 15 September 2026**

CaloBoss is a food and training log. This page explains exactly what it stores,
what leaves your phone, and who else sees it. It describes the app as built —
if something here stops being true, this page changes with it.

There is no analytics SDK, no advertising, no tracking, and no third-party
service in the app other than the ones named below. Nothing is sold or shared
with data brokers.

## What stays on your device only

- **Anything read from Apple Health.** Workouts and weigh-ins imported from
  Health are cached in a separate on-device database that is deliberately never
  synced to iCloud. Apple's HealthKit rules forbid putting Health data in
  iCloud, and CaloBoss doesn't. Your other devices get this data from Health's
  own sync, not from us.
- **API keys and access tokens.** If you configure a provider key or a CaloBoss
  Cloud token, it is stored in the iOS Keychain, on that device only, and is not
  included in backups that leave the device unencrypted.

**Health data is never sent anywhere without you switching it on.** There is
exactly one setting that changes this — *Settings → Apple Health → "Let the coach
see Health data"* — and it is off unless you turn it on. See
[The AI coach](#the-ai-coach) below.

## What syncs to your own iCloud

If you turn on iCloud sync, the following goes to **your** private CloudKit
database — your Apple account, not ours. We have no access to it:

- Meals you log, including any photos you attach
- Sessions and weigh-ins **you entered yourself**, and your routines
- Your profile: sex, date of birth, height, weight, goals and targets
- Which Health sessions you chose to keep, and any corrections you made to them

That last item is stored as an identifier plus your own edit — never a copy of
the values Health supplied.

You can turn sync off in Settings. Doing so leaves the data on the device.

## What goes to the CaloBoss server

When you use the **CaloBoss Cloud** provider, the app sends the following to a
server we operate at `caloboss-proxy.fly.dev`:

- The meal description you typed, or the meal photo you took
- The list of nutrients the app tracks
- Your access token, so the request can be attributed and rate-limited

**Registering.** To get that access token you sign in with Apple, and the app
sends the server the signed confirmation Apple gives it, plus your name if Apple
supplied one. The server checks Apple's signature and then keeps:

- An opaque identifier derived from Apple's account identifier. The identifier
  Apple gave us is **not** stored — only a one-way hash of it, which is what
  appears in our logs instead of anything identifying.
- Your name, so usage reports are readable.
- The email address in Apple's confirmation, which is a private-relay address if
  that is what you chose.
- A one-way hash of each access token issued to your devices. **The tokens
  themselves are never written down**, so our records cannot be used to act as
  you.

Apple's signed confirmation is checked and discarded; it is not stored, and it
expires within minutes in any case.

**Your meal text and photos are not stored on that server.** They exist only for
the length of the request and are then discarded.

The server does keep a log of each call, containing **metadata only**: the time,
the opaque identifier above, which task ran, which model was used, how many images were
attached, token counts, estimated cost, how long it took, whether it succeeded,
and an error message if it failed. No meal descriptions and no photos. It exists
so we can see usage and cost per person during the beta.

Our host, [Fly.io](https://fly.io/legal/privacy-policy/), processes the server's
traffic and retains operational logs containing the same metadata for a short
period.

## The AI coach

The coach reads your log and comments on it, and can turn a sentence about your
day into entries. Both send data to an AI provider.

What it sends is a **summary**, not your entries: daily calorie and macro
averages, how many days you logged, weekly training volume and strength days,
your weight trend and rate of change, your targets, and your age, sex, height and
goal. Not individual meals, not photos, not notes. You can read the exact text
before sending it — the coach screen has a **"See exactly what gets sent"**
button that shows it verbatim.

**By default the summary excludes anything imported from Apple Health.** Sessions
and weigh-ins that came from Health are left out, and the coach tells you how many
it left out so you know the picture is partial.

If you switch on *"Let the coach see Health data"*, training and weigh-ins read
from Apple Health are included in that summary and therefore sent to the AI
provider. That is a genuinely different thing from sending what you typed here,
which is why it is its own switch, defaults to off, and is not bundled into any
other setting. You can turn it off again at any time; it only affects what is
sent from that point on.

When you use the coach to log a day, the sentence you type is sent so it can be
turned into entries. Nothing is saved until you review and confirm it.

## Talking to the coach

You can dictate to the coach instead of typing, and have its answer read back.

**Dictation** uses the microphone and Apple's speech recognition. CaloBoss asks
for your device's **on-device** recogniser, so on an iPhone that supports it your
voice is turned into text on the phone and the audio goes nowhere. Where the
device can't do that, iOS sends the audio to Apple to transcribe — Apple's own
permission prompt says so, and CaloBoss says so too, on screen, while it is
listening. The text that results is then treated exactly like text you typed.

**Reading the answer aloud** is entirely on-device. It needs no permission and
sends nothing anywhere.

CaloBoss never records audio to a file, and never keeps it. The microphone is
live only while you are holding a dictation open, and the transcript is the only
thing that survives.

## What goes to the AI provider

To produce an estimate or a coach response, the server forwards the relevant
content — your meal description, your meal photo, or the coach summary described
above — to an AI provider, by default **OpenAI**, under our own account, not one
tied to you. The provider receives the meal content but nothing identifying you: no
name, no email, no device identifier, no account.

The provider's own terms govern what they do with it, including any retention
for abuse monitoring. See
[OpenAI's API data policy](https://openai.com/policies/api-data-usage-policies).

You have alternatives, chosen in Settings:

- **Apple Intelligence** — runs entirely on your device. Nothing leaves the
  phone. Text only, so photo estimates aren't available.
- **Your own API key** for OpenAI, Anthropic or Google Gemini — the app calls
  that provider directly with your key, and the CaloBoss server is not involved
  at all.

## Apple Health

CaloBoss **reads** workouts, active and resting energy, heart rate, steps,
walking, cycling and swimming distance, body mass and VO₂ max — only after you
grant permission, and only to log training and estimate calories burned.

The only thing it ever **writes** is the body weight you log in the app, and
only while you have that toggle switched on. It writes nothing else to Health.

You can review or revoke any of this in the Health app, under Sharing → Apps.

## Sign in with Apple

If you sign in, Apple provides your name and an email address — which you may
choose to hide behind Apple's private relay.

Signing in does two separate things, and only the second one leaves the device:

- **In the app**, it identifies you and is stored on that device. It is not what
  makes iCloud sync work — that follows whichever iCloud account the device is
  signed in to.
- **Registering for CaloBoss Cloud** sends Apple's signed confirmation to our
  server, which is how we know a real Apple ID is behind a request without
  asking you for a password or handing out a shared code. What the server keeps
  is listed under "What goes to the CaloBoss server" above.

You can use CaloBoss without either. The app works fully without AI estimates,
and the estimate features also run against Apple Intelligence on the device or
against your own provider key, neither of which involves our server or a
sign-in.

## Camera, photos and Face ID

The camera and photo library are used only for the pictures you choose to take
or pick. Face ID, if you enable the app lock, is handled entirely by iOS —
CaloBoss never receives your biometric data.

## Deleting your data

- **In the app:** Settings has a delete-everything action that removes your
  entries, sessions, weigh-ins, routines and the cached Health data, and
  propagates those deletions to iCloud.
- **Deleting the app** removes everything stored on the device, including the
  Keychain token.
- **On our server**, your registration and the usage metadata described above are
  keyed to the opaque identifier. Ask us and we'll delete both and revoke your
  access. Tapping **Leave CaloBoss Cloud** in Settings forgets the token on that
  device but does not by itself remove the registration.

## Children

CaloBoss is not directed at children under 13 and we do not knowingly collect
information from them.

## Contact

Questions, or a deletion request: **iigraceii.li@icloud.com**
