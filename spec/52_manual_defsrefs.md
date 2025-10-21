## User manual defs, refs, trefs and xrefs

#### Background
To simplify the job of tech spec construction and editing, the Technology Stack WG has adopted the Spec-Up spec editing tool, which was originally a DIF open-source project ([here](https://github.com/decentralized-identity/spec-up)). 

Blockchainbird and TrustoverIP invest in improving this tool. It's currently at Blockchainbird's [Spec-Up-T](https://github.com/blockchainbird/spec-up-t) repository only but will eventually sync to [ToIP](https://github.com/trustoverip/spec-up-t).

This document also contains a [normative section](#spec-up-improvements) that has served as a design for the coding project since the start of 2024.

#### Objective
To offer authors and curators a hands-up guide to handle Spec-up's syntax correctly and efficiently with regard to `defs`, `refs`, `trefs` and `xrefs`. Thereby respecting the golden rule:

 "Try `(x/t)ref` before `def`"

([why?](#try-ref-before-def))

#### Characteristics

Why bother? Because it's going to be a mess soon, if you don't. 

Terminology has a life cycle. Some concepts and their specific terminology are long-lived. They reside in their field and are related to other concepts. Other terminologies are contemporary. Terminology can have broad applications or, conversely, have a specific small niche. Nevertheless, they all share these characteristics:
1. The sources (definitions or defs) need to be managed because its content is burdened with reputation
2. References (or refs, trefs and xrefs) need to be managed in the digital world where creating copies is easy, and every *copy* for no reason whatsoever might cause confusion
3. Different roles and responsibilities work with and work on terminology. We got to keep track of who did what in which role. 

#### Cheat-sheet using def,ref,tref and xref

You have your own definition of a term?

Use [[def:<term>]] and [[ref:<term>]]

Would you like to list an external term definition in your own glossary?

1. Declare an external glossary in your configuration file with an <xgloss> mnenomic to reference it
2. Use [[tref:<xgloss>, <term>]] to list a snapshot *in the Terms Definition section* of your specification or glossary.

Would you like to link to an external term definition anywhere in your own glossary (and have a popup definition with a mouse-over)?

1. Declare an external glossary in your configuration file with an <xgloss> mnenomic to reference it
2. Use [[xref:<xgloss>, <term>, {<alias>} ]] to link to it real time anywhere in your glossary or specification. The optional `alias` will be show as the link text.

#### Governance of own repo
The governance of def & refs in the own repo has to be strict: The content of definition has to be kept sound by humans. So check your `ref`s to see if you changed the `def`.  
[Source](https://wiki.trustoverip.org/display/HOME/2024-07-01+CTWG+Meeting+Notes)

#### ToIP glossaries

 In the ToIP Technology Architecture Specification, it's a long-desired feature to add an integrated glossary; It's named https://glossary.trustoverip.org.
 
 Our objective is to offer a framework to offer this in a sustainably consistent way. The Concept & Terminology work group (CTWG) has begun publishing the ToIP Glossary as its own standalone Spec-Up-T specification, where every entry is properly formatted, and people are able to include terms from the ToIP Glossary (without having to copy those 400+ terms over into its own glossary).

We have in fact three general-purpose glossaries available at ToIP/WebofTrust from April 2025:
- [General IT glossary](trustoverip.github.io/ctwg-general-glossary)
- [ToIP main glossary](https://glossary.trustoverip.org) which is focussed on term definitions in the Self-Sovereign-Identity field
- [KERIsuite glossary](https://weboftrust.github.io/kerisuite-glossary)

**Process check: content requirement**

External glossaries:

You should visually check each `def` created in a local Spec-Up document against *any `def`* that exists in any of the remotely referenced document URLs listed in the local document (see the `title` list description in your `specs.json`).

To find the list, look for `external_specs:`

```
 "external_specs": [
 {
 "TP": "https://trustoverip.github.io/ctwg-main-glossary/"
 }
 ...
```

##### Why "try ref before def" {#try-ref-before-def}

::: note Info
with ref we mean the broader concept of `tref`, `xref`, `iref` and `ref`
:::

These are the advantages of *trying ref before def*:
- consensus building: if you study defs of related scopes under the same umbrella, you'll become more knowledgeable and aware of the different fields
- less work: it's easier to adopt a definition with well-formed criteria than having to [design one](#terminology-design-aids) yourself
- leading by example: your refs might be copied, enforcing the reputation of the `def` at hand.
  
Keep reading for an **important caveat** to these advantages! (No, [bring me there](#caveat-copy-def) now)  

**Decide whether you'd like to adopt a definition as is, adopt with a comment, or define yourself.** See [flow diagram](#flow-of-writing-a-specification-in-spec-up)

#### Functionality
For an author, there are three main relevant functionalities.
1. Spec-Up already has a basic glossary feature: `def` tags for defining glossary entries and `ref` tags for marking up terms in the spec that refer to def-tagged terms. Def tags only reference def tags *in the same* Spec-Up document.
2. An `xref` supports *remote* refs
3. A `tref` to print a external definition in your own glossary
4. An `iref` to include a front-end generated inline copy of a definition.
5. We have functionality that detects dangling `refs` and `defs`. In other words, code that checks to see that: 
 a. any ref tag defined in the spec has a corresponding def tag for the glossary entry, and  
 b. every def tag defining a glossary entry has at least one ref tag pointing to it.

Supported consistency pre-cautions and reporting:

::: note Status
October 2025 - The feature "health checks" is operational and available as a separate repository:  https://github.com/trustoverip/spec-up-t-healthcheck. Also, the npm package is available via npm install spec-up-t-healthcheck (Oct 2025: version 1.0.0)
:::

Each `def` in a local Spec-Up document has **exactly the same** `def`* existing in any of the remotely referenced document URLs listed in the local document (see the `title` list description in your `specs.json`). This is also a recommended visual check performed by authors. ([Why?]({#try-ref-before-def}))

Each `ref` has an existing `def`. Each `xref` has an existing `def` in the `title` glossary.

It **checks** each `ref` and `xref` created in reference `doctags` against *any `def`* that you're about to **remove** from a local file. 

It **signals** each `ref` and `xref` created in reference `doctags` against *any `def`* that you're about to **change** in a local file.  

When a local Spec-Up document includes a certain glossary from another remote Spec-Up document, this can be considered as a statement: "We think we might be on the same page as the people that maintain this glossary."

It's important to make explicit that somebody in a certain [role](./role.md#user-reader) added context to a remotely referenced term definition. Or he/she has chosen to refrain from that.

#### Title (formerly "Doctag")

#### External linking (tref and xref)

::: note Info
the `key` refers to a term specified in key-format spelling; lowercase with dashes instead of spaces. Example: `self-sovereign-identity`.
:::

We need the capability for all ToIP specs to use remote refs to reference a common ToIP Glossary in addition to their own internal glossary. So far, an incentivization under TSWG spec authors would be fine with that capability: they can use any term already defined in the ToIP Glossary without having to repeat it in their glossary, and they can add any term specific to their spec.

```
[[tref: group, key, {alias1}, {aliases 2 to n}]] and [[xref: group, key, {alias1} ]]
```

`key` MUST be one of `term` in any of `group`'s glossary. If there is an `alias1` it'll be used as the definition text (tref) and link text (xref).

For example, a specification that includes an `xref` tag that looks like this: [[xref: toip, key, ]] would reference a def tag defined in the ToIP Glossary. Similarly, a ref that looks like [[xref: hxwg, {term}]] would reference a defined term in the (theoretical) HXWG glossary.

With this remote reference feature, all ToIP specifications (and any other deliverable written with Spec-Up) would be able to include linked glossary terms (including hover pop-up definitions), both from within its own glossary and from any referenced glossary in another document that also uses Spec-Up.

Mind you, this process touches on group dynamics, consensus building, and communication.

#### Dangers of bluntly referencing and copying  {#caveat-copy-def}

It's important to note that team members in various [roles](#Roles) should feel free to define a term as they wish, **after studying what's available**. This is an important caveat for referencing terms.

#### chains of refs and context switching

##### What is "chains of refs"

Specifications have their own mental model. Referencing definitions and text sections in other specs or glossaries means consensus building (via `tref`) and syncing ideas (via `tref` and `xref`).

In Spec-Up-T we've been able to group specs and glossaries under a certain umbrella in an "ecosystem" of interrelated GitHub pages end-products and repos.

A chain of ref mean: a tref to a tref to a tref, etc. Is also means the possibility a of a circular ref.
**We do not want chain of refs**, rejected on content grounds too, which we call `context switching`

Context switching means that you refer to exactly the same term or alias of a term in another context, without confirming that you're talking about the same concept.

##### Example

`witness` in KERI means something other than what is usually understood in the broader SSI field.

The design decision of Spec-Up-T therefore, is:
only one-deep trefs
only one-deep xrefs
a local (i)ref to a tref(-alias) is fine

Not allowed:
- an xref to a tref
- an xref to an alias
- a tref to a tref
- a tref to an alias

This way Spec-Up-T prevents circular refs and unobserved context-switching (or mental-model switching).

##### Substitutions to not switch contexts

Spec-Up-T offers front-end functionality to substitute each `ref` in a `tref`ed text snippet for the **local match** of that `key` as long as the `ref`ed term has the syntax of a `key`.

Spec-Up-T also offers front-end functionality to make each full URL in a `tref`ed text snippet operational. It can only check the validity of the link with tooling as specified in the [parent issue](https://github.com/trustoverip/spec-up-t/issues/160)

`Trefs` can also be presented as plain text without links. So the toggle offers plain text or text with links; these links consist of full URLs and locally-matched `refs` in the proper `key` format.

#####  It should consist of **errors** for:

Dangling tref: there's no match in the external document on the `key` to a `def`

Dangling xref: there's no match in the external document on the `key` to a `def`

##### It should consist of **warnings** for:

Dangling refs: there's no hit in the document to a `def`(-alias), `tref`(-alias)

Dangling def: 
1. There's no `ref` in the local document, 
 2. There's no `xref` or `tref` in the ecosystem of interlinked specs

Dangling tref: there's no `ref` in the local document to the `key` or `alias` of the `tref`

Plain external links: broken, full URLs to outside 

Local anchors: broken, for cross-references and bibliography's normative and informative links

##### Mind you: we cannot accept chains of refs nor context switching:

xrefs: we do not match an *alias* defined in an external document's `def`, only the properly formatted `key`

xrefs: we do not match anything from a `tref` defined in an external document

trefs: we do not match an *alias* defined in an external document's `def`

trefs: we do not match anything from a `tref` defined in an external document

#### Add context and metadata

::: note Status
March 2025 - The feature "context metadata" is in the design phase, so it is not operational
:::

Adopting a term from a related scope (under the ToIP umbrella) or externally has the possibility for the author, curator, and maybe even other team members to add context to the definition adopted. The following metadata will be (automatically as much as possible) registered:

- `term`, or (optional) `alias` or (optional) `acronym` of the term definition used to reference
- `URL` of the spec in which the term definition list is present and the name of the header
- `commit hash` of the term definition plus specification adopted
- `authenticated GitHub user` that adopts the term (create), changes its context (update) or deletes the context.

This metadata can be added:

- `group name` from which the term will be adopted
- `role` of the `authenticated GitHub user` in the current scope

You could add or remove:
- `context`, which is a block of free text.

The **order in which these changes take place** to a terminology definition, referencing, and/or comments will be registered.

Mind you: the adopter of a term can't delete nor alter the original definition present in another scope.

#### Local versus Remote references
Technically, the only difference between a local ref and a remote ref is that the former are always within the same Spec-Up document — they look like:

`[[ref: term]]`

The latter allows the author to reference a def in a different Spec-Up document. They look something like:

::: note Status
March 2025 - The features "tref and xref" are under testing, so it is not fully operational yet
:::

`[[xref: title, term]]` is a short unique tag assigned to the remote Spec-Up document containing the def for the term being referenced. So, any Spec-Up document that uses remote refs would need to include a `doctag` section that looks something like this:

In `specs.json`:
```
 "external_specs": [
 {
 "<title>": "<URL>"
 }
```
example
```
 "external_specs": [
 {
 "PE": "https://identity.foundation/presentation-exchange"
 },
 {
 "TP": "https://trustoverip.github.io/ctwg-main-glossary/"
 }
 ...
```

### Adopt, add context, or define

::: note Status
March 2025 - The feature "context metadata" is in the design phase, so it is not operational
:::

Check the flow diagram of writing terminology (references) in a specification [here](#flow-of-writing-a-specification-in-spec-up).

##### How do we adopt the term "as is"? {#adopt-asis}

*Local* preferable
`[[ref: term]]` 

Or *remote* reference

`[[xref: title, term]]`  and `[[tref: title, term]]` 

Where `term` is either a term, acronym, or alias.

##### How do you adopt a term with added or updated context? {#adopt-context}

::: note Status
March 2025 - The feature "adopt a term with context and metadata" is in the design phase, so it is not operational
:::

**Example**
Where `KE` is the `title` (doctag) of the KERI spec in spec-up format and `TP` is the title of the ToIP overall glossary in spec-up.

```
[[def: verification]]

~ Verification in Healthcare is in between the strict [[xref: KE, verification]]
 and the more loose ToIP definition [[xref: TP, verification]]. However, we have the same criteria as KERI
 because our system will be KERI-based.
```

Print the definition in the Terms Definition section (to be specific in the .md file under the subdirectory of directory `./spec` that holds all term derfinition of a specification:

`verification.md` contains:
 ```
 [[tref: TP, verification]]
```
##### Local inline transclusion of a definition

The specification: `[[iref, key or alias]]` and this tag produces:

<p>key/alias : {def text}</p> with a <a href="{anchor}">source</a> link if it can be found, and nothing at all if it can't; the result itself doesn't get an anchor.

In principal we have one contains-all glossary per repo/specification but `iref` offers the extra ability to repeat a `def`-ed of `tref`-ed definition with an inline reference.

Example:
```
[[iref, Attestation]]
```

If there's a local match, the tag produces for example:
```
Attestion: An identifiable set of data that describes an [entity]({link}), which is the [subject]({link}) of the attribute.
```

if no match: non-fatal error

##### How do you add context to an adopted term?

`[[tref]]` + extra text in the Markdown file using `~` per paragraph

Example Markdown in example file `decentralized-identifier.md`:

```
[[tref: toip1, decentralized-identifier, Decentralized ID]]

~ In our project an identifier is a hash made of the uploaded image, ...
```

##### How to reference an external definition?

Remove the local `def` and change.

`[[ref: term]]` into `[[xref: term]]`

Now, the term is again externally referenced as "as is."

##### How to transclude an external definition?

[[tref]]

##### Form phrase macros

A disputable way of matching terms to definitions is by using Form phrase macros. See Annex [Form phrase macros](#form-phrase-macros) by Rieks Joosten.

The upside of using Form phrase macros is that you don't have to explicitly list all possible aliases of a term.

The upside of using Form phrase macros is that you have to guess or reason how matches have been established.

As of October 2025 we don't a have a clear policy yet, and aliases all have to be explicitly summed up.

### Normative section

Have a look at it [here](#spec-up-improvements) and be informed that Spec-Up is a longer running open source project that [originated in DIF](https://github.com/decentralized-identity/spec-up). ToIP will invest in improvements to it in 2024. And offers these improvements as PRs to the DIF repo.

Here, we focus on the informative aspects of the technical specification: what it is, why we are programming it, and how to use it.

It is possible to include references to terms from external spec-up generated specifications. To include a source you would like to pull references from, include an external_specs array in your spec config. The value should be a key/value object where the key is used in the external reference below, and the value should be the URL of the external spec.

To include **an external term reference** within your spec, use the following format `[[xref: {title}, {term}]]` where `{title}` is the title given to the spec in the `specs.json` configuration file and `{term}` is the term being used. 

To include an **external term definition print-out** within your spec, use the following format `[[tref: {title}, {term}]]` where `{title}` is the title given to the spec in the `specs.json` configuration file and `{term}` is the term being used. You will recognize the `tref` by an altered background color and other controls in the panel.

For example, using the `PE` spec given in this example:
```json
{
  "specs": [
 {
      ...
      "external_specs": [
 {"PE": "https://identity.foundation/presentation-exchange"}
 ]
 }
 ]
}
```

#### Internal definition (def)
definitions (`def`s)

::: note Status
The feature "acronym" is under construction!
:::

```
[[def: term , {acronym}, {alias}, {alias}, ... ]]
~ Lorem Ipsum 
```
{optinal}

Define a `term` in a ToIP definition style: lowercase.

Optionally, an `alias` could be referenced. If you do so, the reference MUST end with the definition of `term`. Test by simply clicking the link.

::: note More Info
Check `defs` of aliases https://github.com/decentralized-identity/spec-up/blob/master/single-file-test/spec.md#term-references
and the working `refs` here: https://identity.foundation/spec-up/#term-references
:::

An `acronym` could be defined and referenced. If you do so, a separate definition of `acronym` must be present in the document itself.

::: note Status
March 2025 - This feature "acronym" is in the design phase, so not operational. However, you can already use acronyms as a def and as an alias.
:::

##### Don't do this
```
[[def: term (acronym)]] and  
[[ref: phrase]]
```
But do this

::: note Status
March 2024 - This feature "abbrev" is in the design phase, so not operational
:::

```
[[def: term, acronym]]
```
How do you add an acronym after the term? Two ways possible:
1. in the markdown, but NOT in the reference to the term:
 [[ref:]]
2. There will be post-markdown processing available to proportionally add the acronym


#### Internal linking (ref)

```
[[ref: phrase]]
```
`phrase` MUST be one of `term`, `acronym` or `alias`.

Three ways of offering references (`ref`s) to definitions (`def`s) by the author of a text:
1. explicitly created by the author
2. extra by default, after n occurrences or below a header of a certain level

1. MUST be done in the source by hand
2. MUST be done by code; we'll add a data attribute to the resulting HTML that indicates the origin of the link.

| TBW, where is the registry to ensure the uniqueness of doctags and the prevention of duplicitous [[ref: doctag]]s? |


## System feature Consistency

Have a look at it [here](#spec-up-improvements) and be informed that Spec-Up is a longer running open source project that [originated in DIF](https://github.com/decentralized-identity/spec-up). ToIP will invest in improvements to it in 2024. And offers these improvements as PRs to the DIF repo.

The tool will perform:
- Basic domain checks
- Domain checks Spe-Up or GitHub actions
- Parser checks Spe-Up or GitHub actions

### External Consistency
We like the reuse of existing terminology laid out in definitions and glossaries. If applied correctly, reuse will increase consensus within TrustoverIP.

Given this positive effect, we encourage people to look at what's there already before defining and writing their own definition.

How do we know which known glossary to use? Maybe any glossary we have previously created a cross-reference from should be included?
There is already tooling available to include existing glossaries and give a unified overview of them in [KERISSE](https://weboftrust.github.io/WOT-terms/docs/glossary-unified?level=2). This listing can be adjusted to "ToIP only".


### No effective system without governance

The governance rules that we have to put in place (at least with the ToIP community) should be:

1. If the spec authors want to use a term with its definition term as defined in the ToIP Glossary, the spec authors MUST insert a remote ref to that term in their spec and MUST NOT copy the term (or worse, redefine it) in their internal spec glossary.

2. If the spec authors want to use a term defined in the ToIP Glossary but modify its definition, they COULD raise an issue and/or a pull request (PR) to the ToIP Glossary, making the case for their proposed change. If that change is resolved to their satisfaction, they can proceed as per rule #1 above.

3. If the spec authors want to use a new term that does not exist in the ToIP Glossary to their liking, they have two choices:
- If the spec authors believe the term should apply “ToIP community-wide”, they can submit a PR to have it added to the ToIP Glossary. If accepted, they can then follow rule #1 above.
- If the spec authors believe the term only applies in the scope of their particular spec, they can define it with a def tag in their own internal spec glossary and then ref it there.

Of course, this set of rules only works within a coherent community willing to follow them. We can’t control the use of terminology outside of the ToIP community.

## System feature functionality  {#post-processing}

The front-end functionality of the resulting github.io page of a Specification can and must be altered to comply with various Reader allowances:
- Only so and so often is a link to a known term in the glossary
- Only so and so often is an acronym of a term added to the term in the core text
- Pop-ups consistently showing definitions while hovering over the term
- Consensus tooling (kerific) as a browser extension
- Search functionality is present already in Spec-Up-T
- Harmonica function available, to hide info or restrain search function to only the headers.


## System feature layout
The front-end layout and pdf layout of the resulting GitHub.io page can and must be altered to comply with various style-guide rules of external parties like IETF or ISO.

This is out of scope of this terminology governance guide.