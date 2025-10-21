## Integration
This is an informative section

Spec-Up from DIF, Spec-Up-T that started as "the Glossary tool", TEv2, and the KERISSE-engine (search engine, KERIDoc education) plus [Kerific]() tooling are gradually going to be integrated for the sake of concept & terminology management.

### Spec-Up-T is a migration from Spec-Up

Spec-Up-T does not support a backwards-compatible merge-back into Spec-Up due to architectural, structural, and functional advancements that fundamentally extend beyond the scope and capabilities of the original Spec-Up.

You can find the supporting arguments for this choice below.

#### Structural Differences in Configuration
Spec-Up-T introduces a significantly updated specs.json structure, including new fields such as spec_terms_directory, external_specs, and external_specs_repos. These are absent in the original Spec-Up and are essential to how Spec-Up-T organizes and renders terminology data, making direct backward merging infeasible.

#### Terminology Engine Dependency
Spec-Up-T integrates a dedicated terminology engine, which requires term definitions to be stored in individually structured files and tracked through terms-index.json. Spec-Up, by contrast, operates with simpler, monolithic Markdown files. This decoupling of terms is central to Spec-Up-T, and we cannot plausibly reverse-engineer it into Spec-Up without overhauling its processing logic.

#### Rendering and Output Mechanism Changes
Spec-Up-T introduces generated artifacts such as specs-generated.json and automated glossary indexing, which are not recognized or usable by Spec-Up's static site generator. These outputs are vital for maintaining terminological integrity and cross-spec reference management.

#### Command-Line and Automation Enhancements
The Spec-Up-T command-line interface includes extended tooling for rendering, xref management, and specification freezing (e.g., version snapshots), which depend on newer Node.js capabilities and structural expectations not present in Spec-Up.

#### One-Way Migration Path Provided
The official documentation only supports a forward migration path—from Spec-Up to Spec-Up-T—and includes no tooling or guidance for a reverse path. This unidirectional approach reinforces the directionality of development and the intent to treat Spec-Up-T as a successor, not a drop-in replacement.

#### Conclusion
The evolution of Spec-Up-T into a dual-purpose engine (technical specification + integrated glossary) reflects a shift that renders backwards compatibility impractical. Migration to Spec-Up-T is clearly supported and encouraged, but returning to Spec-Up would require dismantling key features and functionality, making such a merge-back both unsupported and strategically unwise.

#### Acknowledgement
We would like to thank Spec-Up for laying the groundwork with a simple and accessible way to write specs in Markdown, resulting in a one-pager on the web. Big thanks to Daniel Buchner for kickstarting it all—his early ideas and work made spec writing more structured and collaborative. Spec-Up-T builds on that same spirit, adding a terminology engine to tackle new needs.

### No current TEv2 

After the retirement of Rieks Joosten, TEv2 has become a dormant project?

We refer to the Annex of the achievements of TEv2 and how it has shaped Spec-Up-T.