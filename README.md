# Richard's Custom CSL files

My modified citation style language files for custom citation formats.

## CiTO

Experimenting with adding Citation Typing Ontology ([CiTO](https://sparontologies.github.io/cito/current/cito.html)) information to base citation formats
Inspired by ["Two years of explicit CiTO annotations [in the Journal of Cheminformatics]"](https://doi.org/10.1186/s13321-023-00683-2)

The goals was to be able to add 'citation intentions' information to my citation workflow.
This generates a much more interesting and useful citation graph as it allows the edges to be annotated with contextual information:

```mermaid
Article A -- Cites --> Article B

Article A -- Cites, Because it used a method in --> Article B
```

Things can can be cited frequently because people think they are wrong as well as correct or useful, it would be nice to know why citations happen not just that they happen.

By adding some information to the `Extra` field in Zotero you can make use of the 
name of this field as a variable in csl.

WARNING This is an unsupported / unofficial feature of Zotero and citeproc.js and is not portable to other csl implementations
It does not appear possible with the [current CSL spec](https://docs.citationstyles.org/en/stable/specification.html) to fully implement something like this.

See: https://www.zotero.org/support/kb/item_types_and_fields#citing_fields_from_extra
The Zotero style editor checks the XML against the schema and renders a preview
See: `Edit > Setings > Cite > Style Editor`

```
cito-terms: citesAsDataSource || citesAsEvidence
```

BibTeX produced from Zotero contains the `Extra` information in the `annotation` field

Obviously you may wish to cite the same paper for different reasons in different places so it does not make sense to embed this information permanently in a reference manger but if you are using project specific references files this could be a convenient way of generating them.
Project specific references files is one of the approaches taken in the Journal of Cheminformatics trial mentioned above, for LaTeX articles.
For markdown / pandoc files processed with a lua filter a syntax like this: `[@uses_method_in:agrees_with:Willighagen_2020]` could be used to indicate citation intension inline in the document.
This latter approach seems more convenient froma user perspective but requires all the various editors to implement this as a feature on top of existing reference mangement tooling.
Integrating it into the csl spec would still require downstream implementation but might be more likely to see wide implementation as a part of maintainers adding support for a new version of the csl spec.

You way wish to site the same paper for different reason in the same manuscript in which case the problem in the bibliography is somewhat analogous to be problem of citing diferent pages from the same book at different places in a manuscript.
You could have a single citation with both intensions / page ranges or entirely seperate - mostly duplicative - references in the bibliography.

In [ieee-CiTO.csl](ieee-CiTO.csl) I abused the names tag to concatenate a list of terms separated by `||`

Citations in the bibliography are appended with: **[cito:citesAsDataSource, citesAsEvidence]** for all types of cited entity by default.
The `cito` macro return the comma seperated list of terms otherwise unformatted and the `cito-generic` macro makes text bold and wraps with: `[cito:`, `]`

Another thing it would be great to be able to do here is link to the CiTO ontology directly from the term but this does not supported by csl either.
I could add the text of the link but not generate a hyperlink, with or without a name that differs from the link text.
I presume this is to preserve compatability with formats which do not support URLs, though it would seem reasonable at this juncture to permit electronic formats to represent this information as a hyperlink and print ones to represent it as an explicit string if they want to.

**[cito:[citesAsDataSource](https://sparontologies.github.io/cito/current/cito.html#d4e152)]**


### TODO

- See if I can use/adapt the lua filters here: https://github.com/jcheminform/markdown-jcheminf/tree/master for Quarto documents
- Inquire of csl upstream if this is something they might, at least eventually, be interested in supporting (see their [discourse](https://discourse.citationstyles.org/) forum)

