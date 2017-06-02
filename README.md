# NBIS site tools

This repository contains descriptions of tools that are under
development and maintenance by NBIS staff. The tool descriptions are
presented on the NBIS website:
http://www.nbis.se/infrastructure/tools/.

All mature, released tools that are maintained by NBIS should have a
description in this repository. We also include descriptions for tools
that we are developing, but have not yet released, to show what we are
working on, both to colleagues within NBIS and externally.

## Directory structure

- `README.md`    This file
- `_scripts/`    Scripts to aid creation of tool descriptions
- `_stubs/`      Description "stubs" used when fetching information from bio.tools
- `_templates/`  Templates for tool descriptions
- `tools/`       Tool descriptions to be displayed on the website

Directories that should be ignored by the website content managment
system (Jekyll) are prefixed with underscore.

## Adding tool descriptions

The tool descriptions follow a simple YAML format. Please see the
files under the directory `tools` for examples, and check how they are
displayed at http://www.nbis.se/infrastructure/tools/. Each YAML file
corresponds to one tool.

To add a file or make changes, first clone the
[nbis-site](https://github.com/NBISweden/nbis-site) repository as
described in its README. You will then find this repository under the
directory `nbis_site/_biotools`, as a submodule. To see the effect of any
changes you make, follow the instructions in the nbis-site README file
to build and serve the NBIS web pages locally.

The procedure for adding tool descriptions depends on whether the tool
has been released.

### Adding unreleased tools

This is very easy. Just add a YAML file with information about the
tool, in the directory `tools` (i.e. `nbis_site/_biotools/tools`). You
can use the file `templates/minimal.yml` as a starting point.

### Adding released tools

Tools that are released should preferably be added to the ELIXIR tools
registry [bio.tools](https://bio.tools) first. The aim with bio.tools
is to catalog *all* available bioinformatics tools. Since NBIS is part
of ELIXIR, we should aid this effort by making sure our tools are
included in bio.tools.

After you have registered the tool on bio.tools, the script
`_scripts/tool_validator.py` should be used to fetch information from
bio.tools and create a YAML file. Some information that is lacking
from bio.tools must be provided to the script in a JSON file. For a
hypothethical tool *myTool*, the steps would be:

1. Install the PyYAML library, which `tool_validator.py` depends
   on. This can be done by running `pip install PyYAML`, preferably in
   a virtual environment. The script also uses `urllib2`, which is a
   Python 2 module and the script will therefore not work with
   Python 3.
2. Create a file `_stubs/myTool.json`, using
   `_templates/toolstub.json` as a template.  Normally, the tool
   version does not have to be specified in the JSON file; the script
   will simply grab the latest version from bio.tools. Sometimes,
   however, this does not work, and the version needs to be provided.
3. Execute: `python _scripts/tool_validator.py _stubs/myTool.json`
4. The above command should have created a file `myTool.yml`.
   Check that this newly created file looks OK.
5. Move the file into place: `mv myTool.yml tools`.

Steps 3-5 can be repeated to update a tool description if the
bio.tools record has been updated. We might automate this in the
future.

### Publishing your changes on the NBIS web site

Run Jekyll locally (see above) and check the result of your changes at
http://localhost:4000/infrastructure/tools/.

To get your changes into the actual NBIS web site, you need to create
a working branch of toolsinfo, commit your changes to that branch,
push the branch to GitHub and make a pull request to be approved by
Mikael Borg. If you are a tool developer, you are most likely familiar
with this procedure.

## Further technical notes

If you wish to make any other changes to this repository, please note
that files that are be ignored by Jekyll should be placed in a
directory prefixed with underscore. All YAML files that do not reside
in such excluded directories will be treated as tool descriptions and
displayed on the web site. All non-YAML files outside excluded
directories are copied to the website directory tree, unless
specifically excluded in the site config file `nbis_site/_config.yml`
(this README is excluded in that manner).

## Questions

Please send questions and comments to
[P&auml;r Engstr&ouml;m](mailto:par.engstrom@scilifelab.se). Pull
requests and general questions about the NBIS web site should be sent
to [Mikael Borg](mailto:mikael.borg@nbis.se).

The tool description system was designed and implemented by Jorrit
Boekel, Mikael Borg, Jonas Hagberg and P&auml;r Engstr&ouml;m.
