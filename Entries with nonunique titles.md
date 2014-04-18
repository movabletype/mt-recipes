## Description

Identify entries with nonunique titles and loop through them, such as to create a CSV file of this data.

This could be helpful if your URL scheme depends on entries having unique titles for whatever reason, or if you're simply trying to enhance the specificity of titles for SEO purposes.

## Details

Set up a hash variable called `entry_ids` to store the list of all entry titles and their corresponding entry IDs, and set up a hash variable called `duplicate_ids` that will simply store all the entry IDs of entries with titles that are not unique. We use a hash variable so we can sort by the key, the entry ID, later on.

    <mt:Entries blog_ids="all" limit="0">
      <$mt:EntryTitle setvar="entry_title"$>
      <$mt:EntryID setvar="entry_id"$>
      <mt:If name="entry_ids{$entry_title}">
        <mt:Ignore>
          Next two lines store the first entry, as it wasn't stored already
          since we didn't know it was going to be a duplicate.
        </mt:Ignore>
        <$mt:Var name="entry_ids{$entry_title}" setvar="first_id"$>
        <$mt:Var name="duplicate_ids{$first_id}" function="push" value="1"$>
        <mt:Ignore>Store current entry ID in $duplicate_ids</mt:Ignore>
        <$mt:Var name="duplicate_ids{$entry_id}" function="push" value="1"$>
      <mt:Else>
        <$mt:Var name="entry_ids{$entry_title}" value="$entry_id"$>
      </mt:If>
    </mt:Entries>

Now we loop through all the nonunique entry IDs and set up an entries context to act on them.

    <mt:Loop name="duplicate_ids" sort_by="key reverse">
      <mt:Entries blog_ids="all" id="$__key__">
        <!-- output here -->
      </mt:Entries>
    </mt:Loop>

## Examples

The following code is suitable for outputting a CSV formatted file containing the entry titles and entry IDs for all entries with nonunique titles. Simply copy and paste this code into an index template and set the publish path to a file with a `.csv` extension. The outer `<mt:Section>` block removes blank lines and the inner one makes each entry appear on one line by removing the line breaks.

    <mt:Section regex_replace="/\n[\s]*\n/mg","\n">

    <mt:Entries blog_ids="all" limit="0">
      <$mt:EntryTitle setvar="entry_title"$>
      <$mt:EntryID setvar="entry_id"$>
      <mt:If name="entry_ids{$entry_title}">
        <$mt:Var name="entry_ids{$entry_title}" setvar="first_id"$>
        <$mt:Var name="duplicate_ids{$first_id}" function="push" value="1"$>
        <$mt:Var name="duplicate_ids{$entry_id}" function="push" value="1"$>
      <mt:Else>
        <$mt:Var name="entry_ids{$entry_title}" value="$entry_id"$>
      </mt:If>
    </mt:Entries>

    entry_title,entry_id

    <mt:Loop name="duplicate_ids" sort_by="key reverse">
      <mt:Entries blog_ids="all" id="$__key__">
    <mt:Section strip_linefeeds="1">
    "<$mt:EntryTitle replace='"','\"'$>",
    "<$mt:EntryID$>"
    </mt:Section>
      </mt:Entries>
    </mt:Loop>

    </mt:Section>
