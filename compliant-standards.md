# EMC Compliant Standards

## 1. Introduction

### 1.1 What is this document?

The Email Markup Consortium (EMC) is working to improve email markup, the code used to structure and style content within an email. This document lays out the standards of what that markup should look like.  
  
This document is aimed at top level ideas of what the email markup should do, not specific ways to code.

### 1.2 Who is this document for?

This document is for anyone creating [email markup](https://github.com/email-markup-consortium/email-markup-consortium/blob/main/glossary.md#:~:text=Email%20markup), processing email markup, or displaying email markup. This includes (but isn’t limited to) [email developers](https://github.com/email-markup-consortium/email-markup-consortium/blob/main/glossary.md#:~:text=Email%20developer), email creation tools, email sending tools, and [email clients](https://github.com/email-markup-consortium/email-markup-consortium/blob/main/glossary.md#:~:text=Email%20client).

For this to work it will require developers to make improvements to the markup at the point of creation. As long as that markup is valid it should remain in a recognisable state with minimal changes through to the point the recipient opens the email. This means any processing of that markup by an ESP, mail server, email client or any other technology that touches it, should also follow the guidelines to preserve the standard.

### 1.3 Why is this needed?

The current state of email markup varies a lot. Email markup goes through several stages from development to being read by the recipient. Each of these stages can make changes to the markup. Depending on what services are used this can result in very different code being seen by the user as each service may take a different approach. This document sets out some top level goals for how the markup should be treated.  
  
Without this, there can be a stalemate in seeing progress in email markup. Senders won’t include updates that email clients don’t support and emails clients don’t see the need to include updates that senders aren’t including. We need changes on both sides.

### 1.4 What this document is not

* This document is not a “how to” guide on how you can be compliant with these standards.

* This document does not cover email design or content choices.

* This document does not cover email sending protocols.

* This document does not take into consideration current levels of markup support; these are targets to strive for.

## 2. Accessibility

Accessibility is key to achieving our markup standards. When email markup is properly designed and coded, people of all abilities can use it.

### 2.1 Content should fit the container

Email content should respond to fit the size of the container it is loaded in. A recipient should not have to scroll on more than one axis to see parts of the email, nor should content be cut off.

#### Example
Content should adjust to fit the available space with fluid content or @media queries.

### 2.2 Respect user preferences

User preferences should be applied to any email they are viewing. These could potentially be set at the OS level, browser level, or email client level. They should inherit down through these layers into the email markup which should respect the user’s preference and be allowed to change the content accordingly.

#### Example
Level 5 media queries can pass preferences like motion, colour schemes, transparency. We can also use rem units to pass prefered font size.

### 2.3 Make emails discoverable landmarks

Assistive technology should be able to quickly and easily discover an email in a webmail page or app using landmark navigation.

#### Example
Using a semantically appropriate landmark with a descriptive label, often this may be the same as the subject line.

### 2.4 Make focus visible

Keyboard focus should be visible at all times within the email content.

#### Example
Either use default :focus or suitable custom styling.

### 2.5 Allow for content manipulation

A recipient should be able to manipulate the content to a point to make it readable.

#### Example
This can include zoom tools, style adjustment tools, and translation tools.

### 2.6 Email markup should not conflict with email client semantics

Email markup should work in a logical semantic structure without interfering with the email client structure.

#### Example
Use logical heading structure. Avoid using a `<main>` landmark in the email content as this is likely to already include a <main#### Example
landmark.

### 2.7 Define a language

Emails should define a language and language direction for the content. Any changes of language should also be defined in the markup.

#### Example
Set lang and dir attributes

### 2.8 Follow WCAG standards

In addition to these recommendations, you should also consult the latest [WCAG standards](https://www.w3.org/WAI/standards-guidelines/wcag/).

## 3. Resilience

Markup should follow [Postel’s Law](https://en.wikipedia.org/wiki/Robustness_principle): “Be conservative in what you send; be liberal in what you accept.”

### 3.1 Only use supported markup

All code should be within the [WHATWG HTML Standard](https://html.spec.whatwg.org/). Any use of non-standard code should follow the guidelines for [valid custom element names](https://html.spec.whatwg.org/multipage/custom-elements.html#valid-custom-element-name), [custom data-attributes](https://html.spec.whatwg.org/#embedding-custom-non-visible-data-with-the-data-*-attributes), etc.

#### Example
Don’t make up custom elements, attributes, styles, etc. as it may interfere with future development of HTML.

### 3.2 Don’t remove supported code

Supported code should remain intact when unsupported code is removed from around or alongside it by a code sanitizer.

#### Example
If invalid or unsupported code is removed, the code around it should remain unchanged. Gmail currently removes an entire style block for one mistake.

### 3.3 Maintain structure when sanitising code

Unsupported elements should keep their supported attributes and be replaced with a semantically neutral element or [valid custom element](https://html.spec.whatwg.org/multipage/custom-elements.html#valid-custom-element-name).

#### Example
Replace `<main class="foo">` with `<div class="foo">`

### 3.4 Group code to fallback when not supported

Code that is dependent on support of other code should be grouped in a way that it can fallback without showing broken partial support.

#### Example
Issues can arise when `display: flex` is supported but not `flex-wrap`. We can use approaches such as @supports targeting to help group these so they fallback cleanly.

## 4. Performance

Email is a global format, and should be built for all. Some recipients may experience very low bandwidth or very high data costs. This needs to be a consideration so email markup can perform with these restrictions.

### 4.1 Emails should work in low bandwidth environments

Emails should be able to display and perform all actions in a low bandwidth environment.

#### Example
Keep external assets to a minimum file size.

### 4.2 Provide fallbacks for interrupted or low bandwidth connections

When assets fail to load the content should still be consumable.

#### Example
Fallback fonts, good alt text, [placeholder background colors](https://www.dev-diaries.com/social-posts/css-background-color-for-image/) behind solid images, or background images.

### 4.3 Only download content that is used

Unused hidden assets should not be downloaded.

#### Example
Swapping images should be done with `<picture>` elements.

### 4.4 Use suitable formats for assets

Assets should load using suitable formats with optimum compression.

#### Example
Use AVIF, WebP, SVG in `<picture>` and/or `srcset`.

### 4.5 Provide low data content alternatives

Alternate content should be provided when requested.

#### Example
plain text version, use `prefers-reduced-data` query

  

## Changelog

-   (no changes yet)
    