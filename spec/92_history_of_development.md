
## History of development

Anti-chronological report

### 2024 Wiki-based source management dropped.

In the process we have dropped github wiki-based source management of term definitions. It's done in Spec-Up-T from early 2025.

### Comparison Spec-Up 2023 and TEv2 by Rieks Joosten, Jan 2024
This specification has used the following insights to write the Guidelines, most notably in the Roles section and the Normative section.

#### Spec-Up

I have had a look at the latest spec-up draft, specifically one relating to terminology. The text tells you about its features, but (as often), you need to see the source of that text (in RAW format) to figure out how to do things if you're new to this. Here's my understanding:
Spec-up term definition syntax is as follows:

[[def: <term> ]]
~ <text that is used as the description/definition of 'term'>

where
<term> is the term that is being defined. The documentation doesn't say what it can(not) be, e.g., whether or not it may contain spaces or special characters and

<text that is used...> appears to be a (single) line of text, which also isn't further specified.

If you want to specify aliases (what TEv2 calls 'form phrases'), you say:

[[def: <term>, <alias1>, <alias2> ... ]]
~ <text that is used as the description/definition of 'term' (and its aliases)>

Where <term>and <text that is used...> are as before, and <alias<i>> are the aliases, which are also not further specified, but the example shows they can contain spaces (so the, and the closing ]] are the delimiters for the term list.

#### TEv2 definitions appear in different forms:

As a set of (curated) text files (markdown), one for each term. They contain (YAML) frontmatter in which there are fields for (a) the term, (b) the aliases (called 'form phrases'), and (c) the text line (called 'glossaryTexts'). In their body, they contain more documentation related to the term.
As an entry in a machine-readable glossary (YAML), every entry basically consists of not only the frontmatter of the curated text file but also some other fields that (third-party) tools can use to find the curated text file or a rendered version thereof.
As a set of Wiki files that will (soon?) be ingestable (turned into curated text files).

Spec-up use of term references within markdown:
[[ref: <term-or-alias>]]

Where <term-or-alias> is the defined term or one of its aliases.
TEv2 use of term references can be done in different forms:
[<showtext>](@)

Where <showtext> is a defined term or form phrase. However, if <showtext> is not a defined term or form phrase, you can still make it refer to a defined term using the syntax:
[<showtext>](term@)

TEv2 has additional syntax for using terms that refer to stuff
other than concepts (such as mental models, e.g., [<showtext>](pattern:jurisdiction@)
in other scopes, e.g., [parties](@essif-lab), in particular versions of terminology, e.g., [tag](@tev2:latest)

Also, TEv2 has mechanisms where users can define/configure their own syntax for term references, as well as mechanisms for specifying what a termref (when found) should be converted into.
Spec-up glossaries are a rendered version of the list of spec-up definitions, which requires them to all be specified in that same location. When a user clicks on a termref (in the rendered version), it is taken to the location where the term is defined. I haven't seen any documentation of whether/how that would work with multiple files.
TEv2 glossaries come in two forms: machine-readable glossaries (MRGs) and human-readable glossaries (HRGs). TEv2 sees an HRG as a rendered reference to a particular MRG, so (like TermRefs) users can specify a so-called 'MRG-Ref' in their markdown, and when that is processed, an HRG is generated at that location from the designated MRG in a format, and using contents that the user specifies. Here is an example of various HRGs generated on a single page.

#### Discussion

Spec-up is quite different from TEv2. Most notably, By design, spec-up is (very) simple to use and has the basic features you need when writing (simple) specifications. When things become more complex, or you want to explicitly position a spec in a context where other specs also live, my guess is that you run into its limitations. But then, that's not what spec-up was designed to do.
TEv2, on the other hand, is not simple when viewed from a single-context perspective. But you can use and build on the terminologies of others. Another source of perceived complexity may be caused by its flexibility, e.g., it allows users to specify syntaxes (for TermRefs and MRGRefs), as well as the (html, markdown, or other constructs) that they can be converted into.

So, the basic question seems to be whether or not there is an actual need for spec-up and/or TEv2 within ToIP, which I think we can ponder by understanding what we can and cannot do. 

[tno-terminology-design.github.io](tno-terminology-design.github.io)

Glossary Generation Demo | TNO Terminology Design

This page is evidence that an HRG can be generated for every MRG that is available within the scope. It also shows that HRGs can be generated in different formats.

Regarding the roles (specification author, curator, end-user/reader), some thoughts:

Authors come in different flavors. An author who writes specs has different capabilities (e.g., being precise and so) than an author who writes learning stuff (things for Muggles and so on). Darrell can do git and markdown, but I recall that Nicky (and others) thought that to be too cumbersome. The minimalistic use cases would differ for the different author sub-roles, so we should give some thought to which sub-roles exist within ToIP.

When we were talking about the 'term communities,' we also had the role of 'contributor,' which is the role a person performs as (s)he helps draft criteria (for definitions), mental models, and other stuff that we envisaged could be needed in a particular WG, TF (scope). Do we still think that way?

Apart from having the minimalistic use cases, I think it would be helpful if, for every activity or product from the CTWG, we knew
who would *actually* be using it and
what they would need to be able to do with that
so that we can make sure that they can use it and do with it what they need to. And IMHO, that is far from trivial; we should give that some attention.

#### Roadmap to TEv2
As a TEv2 creator and frontman, we share Rieks Joosten's viewpoint on this proposal for using Spec-Up-T refs and defs. 

He explained that the same features being discussed here were also added to TEv2. 

There is always tension between adding a lot of features and taking a long time or keeping things very minimal. He pointed out that creating glossaries based on cherry-picking glossary entries based on personal preferences can be problematic because it doesn't actually establish shared understanding and criteria for defining terms.  
The larger the group involved and the more varied their cultural backgrounds, the more problematic that can become. However, that doesn't mean we shouldn't start with tools that are actually working right now. Rieks' personal preference is to use terminology that expresses the author's intentions clearly. For example, reading the Spec-Up-T documentation was challenging for Rieks, because it was difficult to understand it without more context.

Rieks would like to have several more sessions on TEv2 so we can still look at how we can use it for our terminology. He's not opposed to enhancing Spec-Up-T for these features but, at the same time, keeping TEv2 tooling in progress. 

Rieks Joosten concluded that we need to see what tools are actually needed by both authors and readers to help them comprehend the terms they use. He can also explore how TEv2 tooling can be used to produce Spec-Up-T definitions.

Rieks Joosten was in favor of proceeding with changes to Spec-Up-T but also continuing the work on TEv2 to tackle larger issues of terminology management.

#### TEv2 Explanation

##### Current structure
```mermaid
flowchart LR
A[A:Root];B[B:ScopeDir];C[/C:SAF/]; D[D:GlossaryDir]; E[E:CurTextDir]
 A -->|install| B
 B -->|config| C
 B -->|populate| D
 B -->|populate| E 
```

#### Docusaurus example CURRENT
```mermaid
flowchart LR
A[A:Root];B[B:/docs];C[/C:saf.yaml/]; D[D:glossaries]; E[E:terms]
 A -->|install| B
 B -->|create| C
 B -->|populate| D
 B -->|populate| E 
```
#### SpecUp example CURRENT
```mermaid
flowchart LR
A[A:Root];B[B:/spec];C[/C:saf.yaml/]; D[D:glossaries]; E[E:terms]
 A -->|install| B
 B -->|create| C
 B -->|populate| D
 B -->|populate| E 
```

##### Internal Scope

![internal-scope-terminology](https://github.com/henkvancann/terminology-governance-guide/blob/b64cd36d65c4b0076ccec3e0a30c3f17705e9220/diagrams/internal-scope-terminology-2024-02-26-144340.svg?raw=true)

##### External Scopes and internal scope

![external-scope-terminology](https://github.com/henkvancann/terminology-governance-guide/blob/b64cd36d65c4b0076ccec3e0a30c3f17705e9220/diagrams/external-glossaries-import-2024-02-26-144418.svg?raw=true)

##### Full architecture

![tev2-architecture](https://github.com/henkvancann/terminology-governance-guide/blob/b64cd36d65c4b0076ccec3e0a30c3f17705e9220/diagrams/tev2-architecture-2024-02-26-144443.svg?raw=true)


#### Always archive, never delete

Darrell O'Donnell clarified that technical maintainers will not delete any ToIP repos but will only archive them.

### Brief history of the guide

In 2021, TrustoverIP published the [Specification for Creating and Using Terms](https://wiki.trustoverip.org/display/HOME/Specification+for+Creating+and+Using+Terms)

In the years to follow, the guide to creating [Term wikis](https://wiki.trustoverip.org/display/HOME/Terms+Wikis) has been established. It gives extensive instructions on how to create wikis, use markdown and hyperlinks, etc.

As the number of implementations grew, maintenance of the wikis became out of sync, the number of broken links increased, and duplicate definitions of terms and deviations from the structure and governance offered.

> Darrell O'Donnell: As I am deep in a rabbit hole looking at definitions, a thought occurred to me. We may end up with “over-defined” terms - meaning the definition exists in multiple places. Have you considered that case?
> I believe that a ToIP Master: ToIP Specification conflict should be avoided. If a spec needs a different term than is in the Master glossary, then the conflict should be resolved:
adjust Master Glossary, or
create a new term in Spec
> BUT where we end up looking at terms that are managed even further afield, this gets really hard.
Just curious if this is a condition you’ve thought of.
> I see the following possibilities:
> - multiple def: in a single document (this is just sloppy work - but easy to do, for me at least)
> - duplicated def: - say in Spec and ToIP Master Glossary

::: note Basic Note
 [Check quickly out](https://henkvancann.github.io/ctwg-terminology-governance-guide/#system-feature-consistency) how we take on these concerns
:::

Some of these developments are part of the natural evolution of concepts and terminologies within an umbrella organization like ToIP. Others could be more streamlined.

This specification intends to offer a *[[ref: Guide]]*. A Guide has little or no normative statements as it describes advice on how to create a specific terminology by sticking to guidance and certain rules to know how to **write or adopt definitions**, how to reference them, and where to store and manage them:

- reuse the **specification template** and how to do this in a sustainable manner
- reuse the **ToIP over-arching glossary** where possible
- avoid breaking links in the future
- use the full power of **def, refs, and aliases** in individual documents based on Spec-Up (which is behind the specification template as of 202?)
- be able to generate your documents in a few leading **style guides** like ToIP, ISO, etc.
- Last but not least, any group with a certain scope will need to **source manage their own definitions** or views on the definition, which means that we need to earmark creation and updates with time & author.

## Historical perspective

### Past Practise Terminology Governance

![Past Practise Terminology Governance](https://github.com/henkvancann/terminology-governance-guide/blob/be980e063e99f97cbb14093735ed42d9e8d617e2/images/past-practice-terminology-gov.png?raw=true)

### Current Practise Terminology Governance

![Current Practise Terminology Governance](https://github.com/henkvancann/terminology-governance-guide/blob/be980e063e99f97cbb14093735ed42d9e8d617e2/images/current-practice-terminology-gov.png?raw=true)

### Future Practise Terminology Governance

![Future Practise Terminology Governance?](https://github.com/henkvancann/terminology-governance-guide/blob/be980e063e99f97cbb14093735ed42d9e8d617e2/images/future-practice-terminology-gov.png?raw=true)
