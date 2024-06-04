# Personal Nuclei Templates

## Detecting WordPress plugins

## Using plugin slug

```console
nuclei -t http/wordpress-single-plugin-check.yaml -u https://example.com -V SLUG=ninja-forms
```

Output example:

```console
                     __     _
   ____  __  _______/ /__  (_)
  / __ \/ / / / ___/ / _ \/ /
 / / / / /_/ / /__/ /  __/ /
/_/ /_/\__,_/\___/_/\___/_/   v3.2.8

                projectdiscovery.io

[WRN] Found 26 template[s] loaded with deprecated paths, update before v3 for continued support.
[INF] Current nuclei version: v3.2.8 (latest)
[INF] Current nuclei-templates version: v9.8.7 (latest)
[WRN] Scan results upload to cloud is disabled.
[INF] New templates added in latest release: 62
[INF] Templates loaded for current scan: 1
[INF] Executing 1 signed templates from unsigned
[INF] Targets loaded for current scan: 1
[wordpress-plugin-check] [http] [info] https://example.com/wp-content/plugins/ninja-forms/readme.txt
[wordpress-plugin-check:outdated] [http] [info] https://plugins.svn.wordpress.org/ninja-forms/trunk/readme.txt ["false"]
[wordpress-plugin-check:target] [http] [info] https://plugins.svn.wordpress.org/ninja-forms/trunk/readme.txt ["example.com"]
[wordpress-plugin-check:detected_version] [http] [info] https://plugins.svn.wordpress.org/ninja-forms/trunk/readme.txt ["3.8.3"]
[wordpress-plugin-check:last_version] [http] [info] https://plugins.svn.wordpress.org/ninja-forms/trunk/readme.txt ["3.8.3"]
```

### Katana + Nuclei

```console
katana -u https://example.com | nuclei -t http/wordpress-all-plugins-check.yaml -j -o plugins_with_katana.json
```

Filtering the output to get a list of unique plugins:

```bash
jq -r -s '[.[]["extracted-results"][]] | unique | join(", ")' plugins_with_katana.json
```

Output example:

```console
complianz-gdpr, ninja-forms, wp-meta-and-date-remover, elementor
```
