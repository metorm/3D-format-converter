# 3D-format-converter

A colloction of 3D format converters, step->wrl, iges->obj/mtl, step->obj/mtl

# description list

## step2wrl-occ

**[Originally by twlostow](https://github.com/twlostow/step2wrl)**

A converter based on openCASCADE, which accepts `*.step` or `*.igs` and exports `*.wrl`.

I created a CMakeList to compile the project with `windows`/`openCASCADE 6.3.1`.

Problems TODO:
1. If the step is exported from UG and **some** of the faces are colored, then the un-colored faced are not exported. However, if **all** faces are uncolored, the output is OK; This shall be a logical problem in the code because all entities are loaded according to the verbose information of `occ`.
2. `*.igs` loading is unstable. There may be empty output.
3. This may not be able to deal with compicated models.