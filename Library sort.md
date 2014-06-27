## Description

Sort entries using a library style alpha sort where a leading "a", "an" or "the" is disregarded.

## Details

We can use a regular expression replacement like `regex_replace="/^(a|an|the)[-_ ]+(.*)/gi","$2"` to remove leading English articles and the following underscore, space or hyphen. In the code below, we do this to store the `EntryBasename` in a variable with the corresponding entry ID. We then use `mt:Loop` to sort by the name, and then output the `EntryTitle`.

    <mt:Entries lastn="0">
      <mt:SetVarBlock name="mytitle">''<mt:EntryBasename regex_replace="/^(a|an|the)[-_ ]+(.*)/gi","$2" />''|<mt:EntryID></mt:SetVarBlock>
      <mt:setvar function="push" name="myarray"  value="$mytitle"/>
    </mt:Entries>
    <mt:Loop  name="myarray" sort_by="value">
      <mt:SetVarBlock  name="itemid"><mt:var  name="__value__" regex_replace="/''(.*)?''\|(.*)/gi","$2"></mt:SetVarBlock>
      <mt:Entries  id="$itemid" limit="1">
        <mt:EntryTitle>
      </mt:Entries>
    </mt:Loop>

Note this method works well if you have not modified the basenames of the entries. If you have, you might want to change `EntryBasename` in the code above to `EntryTitle`, but that adds some complications with dealing with leading punctuation.
