# RFEVM216 Documentation and Examples

English is the primary documentation language in this repository. A complete Chinese edition is maintained alongside it, with chapter-level language links for quick switching.

## Documentation

- [English documentation](docs/en/index.md)
- [中文文档](docs/zh/index.md)
- [RFEVM216 User Guide](docs/en/user-guide/index.md)
- [RFEVM216 FPGA Tutorial](docs/en/fpga-tutorial/index.md)
- [RFEVM216 RF Development Guide](docs/en/rf-development-guide/index.md)

The documentation is organized as a searchable MkDocs site. After GitHub Pages is enabled for this repository, the published site will be available at:

<https://lichen813-gif.github.io/RFEVM216/>

## Examples

Reference applications should be added under [`examples/`](examples/README.md). Keep each example self-contained and include its hardware target, tool version, build steps, runtime steps, and expected result.

## Local documentation preview

```bash
python -m pip install -r requirements-docs.txt
mkdocs serve
```

Open <http://127.0.0.1:8000/> in a browser.

## Translation notice

The English documentation is machine-assisted and has been spot-checked for terminology and formatting. For electrical connections, timing, register configuration, safety limits, or production procedures, refer to the Chinese source, schematics, component datasheets, and the actual project as the authoritative sources.

---

# RFEVM216 文档与参考程序

本仓库以英文文档作为默认入口，同时维护完整中文版本。每个章节顶部都提供中英文切换链接。

- [英文文档](docs/en/index.md)
- [中文文档](docs/zh/index.md)
- 后续参考程序统一放入 [`examples/`](examples/README.md)，每个例程应独立说明硬件目标、工具版本、编译步骤、运行步骤和预期结果。
