# Organization

Upon properly cloning this repository according to the instructions in
[cloning.md][cln], you should end up with the following directory structure.

```
CARL-Air-Brake-Power-Supply-Hardware/
|__ CARL-Air-Brake-Power-Supply-Hardware.kicad-pro
|__ CARL-Air-Brake-Power-Supply-Hardware.kicad-prl
|__ CARL-Air-Brake-Power-Supply-Hardware.kicad-sch
|__ CARL-Air-Brake-Power-Supply-Hardware.kicad-pcb
|__ fp-lib-table -> ./library/fp-lib-table
|__ sym-lib-table -> ./library/sym-lib-table
|__ library/
|   |__ symbols/
|   |__ footprints/
|   |__ models/
|   |__ fp-lib-table
|   |__ sym-lib-table
|   |__ README.md
|__ README.md
|__ documentation/
    |__ images/
    |__ description.md
    |__ cloning.md
    |__ prerequisites.md
    |__ organization.md
    |__ flashing.md
```

The KiCad project files are located in the root directory. The KiCad component
library [KiCad Libraries][lib-repo] is contained as a submodule in the
[library][lib-dir] directory. Symbolic links [fp-lib-table][fp-lnk] and
[sym-lib-table][sym-lnk] in the root directory point to the library table files
[fp-lib-table][fp-file] and [sym-lib-table][sym-file] in the [library][lib-dir]
directory. These symbolic links are required for KiCad to be able to locate the
component library.

[cln]:      ./cloning.md

[fp-lnk]:   ../fp-lib-table
[sym-lnk]:  ../sym-lib-table
[fp-file]:  ../library/fp-lib-table
[sym-file]: ../library/sym-lib-table

[lib-dir]:  ../library
[lib-repo]: https://github.com/Kenneth-Goveas/KiCad-Libraries