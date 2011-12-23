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
    <mt:SetVarBlock name="months{$index}"><li><a href="<$mt:ArchiveLink$>"><$mt:ArchiveTitle$></a></li></mt:SetVarBlock>
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
