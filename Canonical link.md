## Description

If your web pages might be accessible by multiple URLs, such as if you output a PHP page that can take URL parameters, you may want to use a [canonical URL link element](https://support.google.com/webmasters/answer/139066?hl=en#2).
This code can be placed in a global header template module and will output an appropriate `link` HTML tag on every published template.

## Details

This works for index templates if $tmpl_self has previously been set to the name of the template with a line like this at the top of each index template:

    <$mt:Var name="tmpl_self" value="Index Template Name"$>

**Note:**
It will throw an error if `$tmpl_self` is set, but set to something other than the name of an existing index template.
The error can be avoided, but the code would be a bit more complex.
You could load the valid index template names in a variable using `<mt:IndexList>`, check `$tmpl_self` against that list and then use a conditional to test that `$tmpl_self` is in the list of index template names before using it in an `<mt:Link>` tag.

    <mt:Unless name="system_template">
      <mt:If tag="ArchiveType" eq="Individual">
        <$mt:EntryPermalink with_index="1" setvar="canonical_url"$>
      <mt:Else tag="ArchiveType" eq="Page">
        <$mt:PagePermalink with_index="1" setvar="canonical_url"$>
      <mt:Else tag="ArchiveType">
        <$mt:ArchiveLink with_index="1" setvar="canonical_url"$>
      <mt:Else name="tmpl_self">
        <mt:Link template="$tmpl_self" with_index="1" setvar="canonical_url">
      </mt:If>
      <mt:If name="canonical_url">
        <link rel="canonical" href="<$mt:Var name="canonical_url"$>" />
      </mt:If>
    </mt:Unless>

The following works if there are not multiple mappings for any given archive type.
If in doubt, use the longer version above.

    <mt:Unless name="system_template">
      <mt:If tag="ArchiveType">
        <$mt:ArchiveLink with_index="1" setvar="canonical_url"$>
      <mt:Else name="tmpl_self">
        <mt:Link template="$tmpl_self" with_index="1" setvar="canonical_url">
      </mt:If>
      <mt:If name="canonical_url">
        <link rel="canonical" href="<$mt:Var name="canonical_url"$>" />
      </mt:If>
    </mt:Unless>

## Credits

Example contributed by [601am](http://601am.com).
