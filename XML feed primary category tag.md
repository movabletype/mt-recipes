## Description

The default Atom feed template in Movable Type outputs a `category` tag for each category of the entries in context. This recipe shows how to add an additional tag to specify the primary category.

## Details

The default Atom feed template outputs a `category` tag for each category with this code:

    <mt:EntryCategories>
        <category term="<$mt:CategoryLabel encode_xml="1"$>" scheme="http://www.sixapart.com/ns/types#category" />
    </mt:EntryCategories>

This results in output like this:

    <category term="Category A" scheme="http://www.sixapart.com/ns/types#category" />
    <category term="Category B" scheme="http://www.sixapart.com/ns/types#category" />
    <category term="Category C" scheme="http://www.sixapart.com/ns/types#category" />

But that does not leave any indication of which category is the primary category for the entry. Perhaps we want something like this:

    <category term="Category A" scheme="http://www.sixapart.com/ns/types#category" />
    <category term="Category B" scheme="http://www.sixapart.com/ns/types#category" />
    <category term="Category C" scheme="http://www.sixapart.com/ns/types#category" />
    <sa:primarycategory term="Category B" />

To make this valid, you should first modify the this line:

    <feed xmlns="http://www.w3.org/2005/Atom">

To be something like this, even if the URL doesn’t actually work (but it should!):

    <feed xmlns="http://www.w3.org/2005/Atom" xmlns:sa="http://example.com/documentation-for-custom-namespace">

Then the magic involves replacing the above `<mt:EntryCategories>` block with the following code that utilizes some tracking variables:

    <$mt:Var name="entry_category" value=""$>
    <$mt:Var name="used_cat" value=""$>
    <mt:If tag="EntryCategory">
      <$mt:EntryCategory setvar="entry_category"$>
    <mt:Else>
      <mt:EntryCategories>
        <mt:Unless name="used_cat">
          <$mt:CategoryLabel setvar="entry_category"$>
        </mt:Unless>
        <$mt:Var name="used_cat" value="1"$>
      </mt:EntryCategories>
    </mt:If>
    <mt:EntryCategories>
      <mt:If tag="CategoryLabel" eq="$entry_category">
        <$mt:CategoryID setvar="category_id"$>
      </mt:If>
      <category term="<$mt:CategoryLabel encode_xml="1"$>" scheme="http://www.sixapart.com/ns/types#category" />
    </mt:EntryCategories>
    <mt:If name="entry_category">
      <mt:Categories>
        <mt:If tag="CategoryID" eq="$category_id">
          <sa:primarycategory term="<$mt:EntryCategory encode_xml="1"$>" />
        </mt:If>
      </mt:Categories>
    </mt:If>

For bonus points, if you also want to output information about the primary category's parent categories, you could replace the `<sa:primarycategory>` tag above with this, which accounts for three levels of parent categories:

      <sa:primarycategory term="<mt:ParentCategory><mt:ParentCategory><mt:ParentCategory><$mt:CategoryLabel encode_xml="1"$>/</mt:ParentCategory><$mt:CategoryLabel encode_xml="1"$>/</mt:ParentCategory><$mt:CategoryLabel encode_xml="1"$>/</mt:ParentCategory><$mt:EntryCategory encode_xml="1"$>" />

## Credits

Example contributed by [601am](http://601am.com).
