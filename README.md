# proto-processing-lib

proto-processing-lib is a library that provides utility functionality for proto
field scrubbing.

## FieldMask AIP-161 compatibility

The field mask implementation in this library currently has some minor
inconsistencies with the [AIP-161](https://google.aip.dev/161) specification,
particularly around resource update behavior. While the current functionality is
robust for most use cases, please be aware of this nuance when working with
field masks in your applications.

### Proto Processing Library's Field Mask Implementation: Differences from [AIP-161](https://google.aip.dev/161) Standard

Proto Processing Library's implementation of field masks diverges from the
AIP-161 standard in the following key ways. This table summarizes the
similarities/differences:

| Feature          | AIP-161 (Standard)          | Library Implementation     |
| :--------------- | :-------------------------- | :------------------------- |
| Repeated fields  | Restricted except at path   | No restriction, allowed on |
:                  : end                         : non-leaf nodes             :
| Map keys         | String or integer           | String (escaped)           |
| Wildcards        | Supported for repeated      | Supported                  |
:                  : fields/maps                 :                            :
| Struct traversal | Supported using '.'         | Supported                  |
| Map traversal    | Supported using '.', keys:  | Supported (string/int      |
:                  : string/int                  : keys), '.' insertion not   :
:                  :                             : supported                  :
| Validation       | Ignore invalid reads, error | Error on invalid field     |
:                  : on writes                   : names                      :
| Update behavior  | Read after masked update    | Not supported              |
:                  : returns same                :                            :
| Intersection     | Not explicitly mentioned    | Supported, returns         |
:                  :                             : intersection of two        :
:                  :                             : FieldMask trees            :
