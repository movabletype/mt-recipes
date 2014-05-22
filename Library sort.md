## Description

Sort entries using a library-style alpha sort, where a leading "a", "an", or "the" is disregarded.

## Details

	<mt:Entries><mt:setvarblock name="mytitle">''<mt:EntryBasename regex="s/^(a|an|the)_(.*)/$2/gi" />''|<mt:EntryID></mt:setvarblock><mt:setvar function="push" name="myarray"  value="$mytitle"/></mt:Entries>
	<mt:loop  name="myarray" sort_by="value">
	<mt:setvarblock  name="itemid"><mt:var  name="__value__" regex="s/''(.*)?''\|(.*)/$2/gi"></mt:setvarblock>
	<mt:entries  id="$itemid" limit="1">
	<mt:EntryTitle>
	</mt:entries>
	</mt:loop>
