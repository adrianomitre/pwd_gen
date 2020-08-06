# Password generator

## Goal

The goal is to solve (part of) the problem that password managers solve without the associated honey pot risk (or cost).
We believe security and convenience both matter and we hope to strike an interesting balance between the two.

This app is meant to replace password managers and mentally managed password systems.

Mentally managed password systems, such as prefixing your super secret password core with the name of the service, are typically easy to reverse engineer (or impractical).

So if one YourFavoriteButNotVerySafeSite.com gets hacked and your password leaks (after all, [storing password in plain text is common practice](https://www.howtogeek.com/434930/why-are-companies-still-storing-passwords-in-plain-text/)) someone can use your leaked password to reverse engineer your password for services that have not leaked.

Or if in an emergency you need to share a password for a specific service with someone for a time-box single-purpose task, revoking that password might not suffice because you might have unwittingly shared your whole system, thus all your passwords for all services.

## What must be remembered

The `{ digest(combination(basePassword, domain)) => version }` map.

The plain map `{ domain => version }`, if leaked, could reveal which services you access. Not very privacy oriented, right?

If we replaced `domain` with `digest(domain)` it would be not obvious at plain sight which services you do access, but the number of services is not large enough to deter [dictionary](https://en.wikipedia.org/wiki/Dictionary_attack) or [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) attacks.

By using the digest of the `domain` salted with `basePassword`, such attacks are no longer possible. Therefore, if the map leaks, it exposes nothing of relevance about you.

## What about the rules

They should be shared in a central repository, which can be accessed online or have its content exported and downloaded for offline usage.

## Requirements

Just a decent browser. No internet connection required for operation.
