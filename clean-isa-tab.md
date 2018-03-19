# Best Practices for Clean ISA-Tab imports

Clean ISA-Tab files import into ISA-Explorer without any manual intervention.
Making imports repeatable and reliable.

To that end:

- name the investigation file `i_Investigation.txt` (study and assay files can have any names, but should, following the ISA-Tab specification, match the names used in the investigation file)
- supply various `Comment[blah blahblah]` fields in the `STUDY` block of the investigation file. These are optional for ISA-Tab files, but required for display in ISA-Explorer. See below for full list.
- Populate the `Study Title` field of the `STUDY` block of the investigation file. They are the titles that are displayed in the ISA-Explorer browser (for example, http://scientificdata.isa-explorer.org/).
- Use UTF-8
- The `STUDY CONTACTS` block in the investigation file is used to populate the author field in the ISA-Explorer browser. So please fill in `Study Person Last Name`, `Study Person Mid Initials`, and so on.

## ISA-Explorer comment fields

ISA-Explorer requires the investigation file have the following comment fields in the `STUDY` block.
They can all be blank (there is some minor functionality loss), but they need to be present.
They can go after the `Study File Name`.

    Comment[Subject Keywords]
    Comment[Manuscript Licence]
    Comment[Experimental Metadata Licence]
    Comment[Supplementary Information File Name]
    Comment[Supplementary Information File Type]
    Comment[Supplementary Information File URL]
    Comment[Data Repository]
    Comment[Data Record Accession]
    Comment[Data Record URI]

Examples can be taken from the Scientific Data ISA-Explorer site, http://scientificdata.isa-explorer.org.
For example, http://scientificdata.isa-explorer.org/sdata201689 which has the ISA-Tab archive http://scientificdata.isa-explorer.org/data/sdata201689-isa1.zip
