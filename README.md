# Password generator

## Goal

The goal is to solve (part of) the problem that password managers solve without the associated honey pot risk (or cost).
We believe security and convenience both matter and we hope to strike an interesting balance between the two.

This app is meant to replace password managers systems and mentally managed password schemes. If you do not use a different password for each service, you are in a even worse position from the information security standpoint and this app will make an even bigger difference for you.

Password schemes, such as prefixing your super secret password core with the name of the service, are typically easy to reverse engineer (or impractical).

And your mentally managed password system almost certainly 
the plethora of password requirements (e.g., 4 to 8 characters with at least one special character) 

So if one YourFavoriteButNotVerySafeSite.com gets hacked and your password leaks (after all, [storing password in plain text is common practice](https://www.howtogeek.com/434930/why-are-companies-still-storing-passwords-in-plain-text/)) someone can use your leaked password to reverse engineer your password for services that have not leaked.

Or if in an emergency you need to share a password for a specific service with someone for a time-box single-purpose task, revoking that password might not suffice because you might have unwittingly shared your whole system, thus all your passwords for all services.

### Password encoding rules format

```json
{
  "required": {
    "lowercase": "<< int >>",
    "uppercase": "<< int >>",
    "digits": "<< int >>",
    "hyphen": "<< int >>",
    "underline": "<< int >>",
    "space": "<< int >>",
    "special": "<< int >>",
    "brackets": "<< int >>"
  },
  "length": {
    "min": "<< int n : n > 0 >>",
    "max": "<< int n : n >= min >>"
  }
}
```

## What must be remembered

The `version` for each `domain` must be remebered. Well, the password encoding rules too, but as they are not user-specific they need not be remebered by every user individually. See the section below for more on this.

### Not privacy conscious ways to store that

The plain map `{ domain => version }`, if leaked, could reveal which services you access. Not very privacy oriented, right?

If we replaced `domain` with `digest(domain)` it would be not obvious at plain sight which services you do access, but the number of services is not large enough to deter [dictionary](https://en.wikipedia.org/wiki/Dictionary_attack) or [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) attacks.

### The privacy conscious way to store that

By using the digest of the `domain` salted with `basePassword`, such attacks are no longer possible. Therefore, if the map `{ digest(combination(basePassword, domain)) => version }` leaks, it exposes no sensitive information about you. (The number of domains you have passwords for or how many passwords you have had for each is not considered sensistive.)

Sure, if you change you `basePassword` you will be unable to know the versions for each `domain`, but that would mean a new password for every `domain` anyway.

## What about the rules

They should be shared in a central repository, which can be accessed online or have its content exported and downloaded for offline usage.

## Requirements

Just a decent browser. No internet connection required for operation.
