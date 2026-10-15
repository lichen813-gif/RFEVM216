# RFEVM216 Reference Examples

Place each reference application in its own directory:

```text
examples/
  <example-name>/
    README.md
    hw/
    sw/
    scripts/
```

Every example README should state:

1. purpose and expected result;
2. supported RFEVM216 hardware revision;
3. required Vivado, Vitis, operating-system, and driver versions;
4. hardware connections and safety prerequisites;
5. reproducible build, programming, and runtime steps;
6. expected logs, captures, or measurements;
7. known limitations and unverified hardware or RF behavior.

Generated projects, build outputs, bitstreams, and large captures should not be committed unless they are deliberate release artifacts.
