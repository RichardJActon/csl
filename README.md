# Richard's Custom CSL files

My modified citation style language files for custom citation formats.

Experimenting with adding [CiTO](https://sparontologies.github.io/cito/current/cito.html) information to base citation formats
Inspired by ["Two years of explicit CiTO annotations [in the Journal of Cheminformatics]"](https://doi.org/10.1186/s13321-023-00683-2)

By adding some information to the `Extra` field in Zotero you can make use of the 
name of this field as a variable in .csl.

WARNING This is an unsupported / unofficial feature of Zotero and citeproc.js and is not portable to other csl implementations

see: https://www.zotero.org/support/kb/item_types_and_fields#citing_fields_from_extra

```
cito-terms: citesAsDataSource || citesAsEvidence
```

BibTeX produced from Zotero contains the `Extra` information in the `annotation` field

In [ieee-CiTO.csl](ieee-CiTO.csl) I abused the names tag to concatenate a list of terms separated by `||`


