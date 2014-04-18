## Description

As of Movable Type 6, you cannot have more than one `field:basename` modifier on an `mt:Entries` tag. Using template tag variables, we can easily work around this restriction to select entries that match any of the desired custom fields.

## Details

We will build a hash variable called `entry_ids` where the keys are the matched entry IDs and the values are the corresponding entry dates, which we will sort by later.

<mt:SetVarTemplate name="id_collector">
  <$mt:EntryID setvar="entry_id"$>
  <mt:SetVarBlock name="entry_ids{$entry_id}"><$mt:EntryDate format="%Y%m%d%H%M%S"$></mt:SetVarBlock>
</mt:SetVarTemplate>
<mt:Entries limit="20" field:my_field_a="Nelson">
  <$mt:Var name="id_collector"$>
</mt:Entries>
<mt:Entries limit="20" field:my_field_a="David">
  <$mt:Var name="id_collector"$>
</mt:Entries>
<mt:Entries limit="20" field:my_field_a="Melody">
  <$mt:Var name="id_collector"$>
</mt:Entries>

<mt:Loop name="entry_ids" sort_by="value reverse">
  <mt:Entries id="$__key__">
    <!-- output -->
  </mt:Entries>
</mt:Loop>

## Credits

Example contributed by [601am](http://601am.com).
