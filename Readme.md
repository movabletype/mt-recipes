# Movable Type recipes

Efficient designers and developers want to spend time solving problems rather than reinventing the wheel. To help all our users be more effective, we're collecting examples of how Movable Type can be used in interesting ways to address recurring issues.

## Browse recipes

* [Basename generation function](Basename generation function.md)
* [Canonical link](Canonical link.md)
* [Category archive pagination](Category archive pagination.md)
* [Category distributor over columns](Category distributor over columns.md)
* [Date ordinal](Date ordinal.md)
* [Detect existance of archive listing](Detect existance of archive listing.md)
* [Entries matching any of multiple custom fields](Entries matching any of multiple custom fields.md)
* [Entries with nonunique titles](Entries with nonunique titles.md)
* [Export entry data in MT format](Export entry data in MT format.md)
* [Library (alphanumeric) sort](Library sort.md)
* [Monthly archives distributor over columns](Monthly archives distributor over columns.md)
* [Open graph meta tags](Open graph meta tags.md)
* [Search processing time](Search processing time.md)
* [Sort by other data](Sort by other data.md)
* [Thumbnail size calculator](Thumbnail size calculator.md)
* [XML feed primary category tag](XML feed primary category tag.md)

## Contribute

We welcome any additions from the community. Please follow the guidelines below. We may make edits or add more examples.

You can contribute via these methods:

* If you're Git savvy, feel free to [fork this repository](https://github.com/movabletype/mtml-recipes/fork), add your recipe files in Markdown format, and send us a pull request.
* You may [open an issue](https://github.com/movabletype/mtml-recipes/issues) with all the information about your recipe. Ideally this would be Markdown formatted, but we welcome all contributions.

This is the standard format of each recipe file. The filename is a very brief description of the recipe. The file itself is Markdown formatted. Please include as much information as possible. See [Sort by other data.md](Sort by other data.md) for a real example.

    ## Description

    Short description of the problem solved and perhaps a bit about the solution. Just give enough to
    differentiate this from other solutions.

    ## Details

    Full explanation, including background and (Markdown style) links to relevant documentation. This
    should assume basic MTML knowledge, but explain advanced concepts and give the user direction to
    find more information.

    Limit code used in the details section to the minimum required to illustrate the technique. Remember
    to indent MTML code examples four spaces so this can render well if we paste it into MovableType.org
    documentation at some point.

          <mt:Loop name="item_list" sort_by="value">
            <mt:Entries include_blogs="all" id="$__key__">
              <!-- entry output here -->
            </mt:Entries>
          </mt:Loop>

    ## Example

    A full example, including any HTML or other code that might have been stripped out for the basic example
    in the last section. Perhaps this would be an example from a real life website. Please change any names
    and other information to make it generic and broadly applicable. If no examples are necessary to fully
    explain the technique, this section can be omitted.

    ## Plugins used

    List the plugins used in the examples so users can be sure which tags are from plugins. Format this as a
    simple list like this:

    * My Plugin provides the `MyPluginData` and `MyPluginData2` tags.

    If no plugins are used, omit this section.

    ## Credits

    Brief credit if necessary, otherwise omit this section.
