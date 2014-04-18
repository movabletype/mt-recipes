## Description

Generate a text file of entry data suitable for importing into Movable Type with the *Tools* > *Import Entries* function.

## Details

This should match what you would get using *Tools* > *Export Entries*, but you can do more interesting processing, or simply add `include_blogs="all"` if you want to consolidate blogs.

## Examples

    <mt:Entries sort_by="created_on" sort_order="ascend" limit="0">
    AUTHOR: <$MTEntryAuthor strip_linefeeds="1"$>
    TITLE: <$MTEntryTitle strip_linefeeds="1"$>
    BASENAME: <$MTEntryBasename$>
    STATUS: <$MTEntryStatus strip_linefeeds="1"$>
    ALLOW COMMENTS: <$MTEntryFlag flag="allow_comments"$>
    CONVERT BREAKS: <$MTEntryFlag flag="convert_breaks"$>
    ALLOW PINGS: <$MTEntryFlag flag="allow_pings"$><MTIfNonEmpty tag="MTEntryCategory">
    PRIMARY CATEGORY: <$MTEntryCategory$></MTIfNonEmpty><MTEntryCategories>
    CATEGORY: <$MTCategoryLabel$></MTEntryCategories>
    DATE: <$MTEntryDate format="%m/%d/%Y %I:%M:%S %p"$><MTEntryIfTagged include_private="1">
    TAGS: <MTEntryTags include_private="1" glue=","><$MTTagName quote="1"$></MTEntryTags></MTEntryIfTagged>
    -----
    BODY:
    <$MTEntryBody convert_breaks="0"$>
    -----
    EXTENDED BODY:
    <$MTEntryMore convert_breaks="0"$>
    -----
    EXCERPT:
    <$MTEntryExcerpt no_generate="1" convert_breaks="0"$>
    -----
    KEYWORDS:
    <$MTEntryKeywords$>
    -----
    <MTComments>
    COMMENT:
    AUTHOR: <$MTCommentAuthor strip_linefeeds="1"$>
    EMAIL: <$MTCommentEmail strip_linefeeds="1"$>
    IP: <$MTCommentIP strip_linefeeds="1"$>
    URL: <$MTCommentURL strip_linefeeds="1"$>
    DATE: <$MTCommentDate format="%m/%d/%Y %I:%M:%S %p"$>
    <$MTCommentBody convert_breaks="0"$>
    -----
    </MTComments>
    <MTPings>
    PING:
    TITLE: <$MTPingTitle strip_linefeeds="1"$>
    URL: <$MTPingURL strip_linefeeds="1"$>
    IP: <$MTPingIP strip_linefeeds="1"$>
    BLOG NAME: <$MTPingBlogName strip_linefeeds="1"$>
    DATE: <$MTPingDate format="%m/%d/%Y %I:%M:%S %p"$>
    <$MTPingExcerpt$>
    -----
    </MTPings>
    --------
    </mt:Entries>

## Credits

Example contributed by [601am](http://601am.com).
