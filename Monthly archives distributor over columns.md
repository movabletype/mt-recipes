## Description

Outputting a list of monthly archives is trivial, but sometimes you want to output those links in an HTML format allowing for multiple columns.

## Details

The following code will output `num_cols` (2) columns of categories, with each column wrapped in a `ul` HTML block. The code output for each individual item is on L. 14, and the entire thing is contained by the header and footer described within `ArchiveListHeader` and `ArchiveListFooter`, respectively.

    <mt:IfArchiveTypeEnabled archive_type="Monthly">

      <$mt:Var name="num_cols" value="2"$>
      <$mt:Var name="index" value="0"$>
      <mt:ArchiveList archive_type="Monthly">
        <mt:ArchiveListHeader>
          <mt:SetVarBlock name="monthly_archive_header">
            <div class="box">
              <h2><$mt:ArchiveTypeLabel$> Archives</h2>
              <div class="block columns">
          </mt:SetVarBlock>
        </mt:ArchiveListHeader>
        <$mt:Var name="index" op="++" setvar="index"$>
        <mt:SetVarBlock name="months{$index}">
          <li><a href="<$mt:ArchiveLink$>"><$mt:ArchiveTitle$></a></li>
        </mt:SetVarBlock>
        <mt:ArchiveListFooter>
          <mt:SetVarBlock name="monthly_archive_footer">
                <div class="clear"></div>
              </div>
            </div>
          </mt:SetVarBlock>
        </mt:ArchiveListFooter>
      </mt:ArchiveList>
      <$mt:Var name="months" function="count" setvar="month_count"$>
      <$mt:Var name="month_count" op="%" value="$num_cols" setvar="modulus"$>
      <mt:If name="modulus" gt="0">
        <$mt:Var name="month_count" op="-" value="$modulus" setvar="month_count_minus_mod"$>
        <$mt:Var name="month_count_minus_mod" op="/" value="$num_cols" setvar="months_per_col"$>
        <$mt:Var name="months_per_col" op="+" value="1" setvar="months_per_col"$>
      <mt:Else>
        <$mt:Var name="month_count" op="/" value="$num_cols" setvar="months_per_col"$>
      </mt:If>
      <mt:SetVarTemplate name="for_inner">
        <$mt:Var name="index" op="++" setvar="index"$><mt:Unless name="index" gt="$month_count"><$mt:Var name="months{$index}"$></mt:Unless>
      </mt:SetVarTemplate>

      <$mt:Var name="monthly_archive_header"$>

      <$mt:Var name="index" value="0"$>
      <$mt:Var name="col_num" value="1"$>
      <mt:For from="1" to="$num_cols">
        <ul class="left col<$mt:Var name="col_num"$> <mt:If name="col_num" eq="$num_cols">last</mt:If>">
          <mt:For from="1" to="$months_per_col">
            <$mt:Var name="for_inner"$>
          </mt:For>
        </ul>
        <$mt:Var name="col_num" op="++" setvar="col_num"$>
      </mt:For>

      <$mt:Var name="monthly_archive_footer"$>

    </mt:IfArchiveTypeEnabled>

## Credits

Example contributed by [601am](http://601am.com).
