## Description

Example of sorting data by custom data using hashes. Sorting by native custom fields is trivial (`sort_by="field:your_custom_field"`), but sorting by other data, such as something output by a plugin, is trickier.

## Details

Movable Type can store data in a hash and later loop through the hash sorted by either the keys or values. We can take advantage of that to sort by data other than the [typical criteria](http://movabletype.org/documentation/appendices/tags/entries.html#sort_by).

First we loop through the entries, in this case storing the output of `<$mt:EntryFieldValue field="my_rating_field"$>` into the `item_list` hash by first assinging the output to the variable `my_rating_field` and then inserting that into the hash. We use the entry ID as the hash key.

      <mt:EntryLinkingEntries field="my_linking_field" sort_by="title" sort_order="ascend">
        <$mt:EntryID setvar="entry_id"$>
        <$mt:EntryFieldValue field="my_rating_field" setvar="my_rating_field"$>
        <$mt:Var name="item_list{$entry_id}" value="$my_rating_field"$>
      </mt:EntryLinkingEntries>

Now that our hash is built, we can loop through it with `mt:Loop`, taking advantage of its `sort_by="value"` modifier.

      <mt:Loop name="item_list" sort_by="value">
        <mt:Entries include_blogs="all" id="$__key__">
          <!-- entry output here -->
        </mt:Entries>
      </mt:Loop>

## Example

Using the same idea as above, we can output two lists of entries, with the second one hidden by default. JavaScript could toggle the visibility between the two `div` containers when the user clicks a "Sort by Name" or "Sort by Rating" link.

    <div id="items_by_name" style="display:block;">
      <mt:EntryLinkingEntries field="my_linking_field" sort_by="title" sort_order="ascend">
        <!-- entry output here -->
        <$mt:EntryID setvar="entry_id"$>
        <$mt:EntryFieldValue field="my_rating_field" setvar="my_rating_field"$>
        <$mt:Var name="item_list{$entry_id}" value="$my_rating_field"$>
      </mt:EntryLinkingEntries>
    </div>

    <div id="items_by_rating" style="display:none;">
      <mt:Loop name="item_list" sort_by="value">
        <mt:Entries include_blogs="all" id="$__key__">
          <!-- entry output here -->
        </mt:Entries>
      </mt:Loop>
    </div>

## Plugins used

Field Day provides the `EntryLinkingEntries` and `EntryFieldValue` tags.

## Credits

Example contributed by [601am](http://601am.com).
