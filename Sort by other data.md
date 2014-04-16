<div id="items_by_name" style="display:block;">
  <mt:EntryLinkingEntries field="loc_badge_entry" sort_by="title" sort_order="ascend">
    <$mt:Include module="Location item"$>
    <$mt:EntryID setvar="entry_id"$>
    <$mt:EntryFieldValue field="loc_rating_select" setvar="loc_rating_select"$>
    <$mt:Var name="item_list{$entry_id}" value="$loc_rating_select"$>
  </mt:EntryLinkingEntries>
</div>

<div id="items_by_rating" style="display:none;">
  <mt:Loop name="item_list" sort_by="value">
    <mt:Entries include_blogs="all" id="$__key__">
      <$mt:Include module="Location item"$>
    </mt:Entries>
  </mt:Loop>
</div>
