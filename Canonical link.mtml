This works for index templates if $tmpl_self has previously been set to the name of the template.
It will throw an error if $tmpl_self is set, but set to something other than the name of an
existing index template.

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
<mt:If name="canonical_url"><link rel="canonical" href="<$mt:Var name="canonical_url"$>" /></mt:If>
</mt:Unless>

The following works if there are not multiple mappings for any given archive type:

<mt:Unless name="system_template">
<mt:If tag="ArchiveType">
  <$mt:ArchiveLink with_index="1" setvar="canonical_url"$>
<mt:Else name="tmpl_self">
  <mt:Link template="$tmpl_self" with_index="1" setvar="canonical_url">
</mt:If>
<mt:If name="canonical_url"><link rel="canonical" href="<$mt:Var name="canonical_url"$>" /></mt:If>
</mt:Unless>


Note:

David: i think the error that would halt rebuilding if $tmpl_self does not match an existing
index template name can be avoided, but the code would be a bit more complex ;)

Charlie: yeah, i'm fine with it as it is. the error would point out the problem and shouldn't
be too confusing i think

David: basically, you could load up the valid index template names in an mt variable using
<mt:IndexList>, check $tmpl_self against that list, then use a conditional to test that $tmpl_self
is in the list of index template names before using it in an <mt:Link> tag