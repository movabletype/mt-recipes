## Description

Outputting a list of categories is trivial, but sometimes you want to output those categories in an HTML format allowing for multiple columns.

## Details

The following code will output `num_cols` (6) columns of categories, with each column wrapped in a `div` HTML block. The code output for each category is on L. 6.

    <$mt:Var name="num_cols" value="6"$>
    <$mt:Var name="index" value="0"$>
    <mt:Categories>
      <$mt:Var name="index" op="++" setvar="index"$>
      <mt:SetVarBlock name="categories{$index}">
        <a href="<$mt:CategoryArchiveLink$>"><$mt:CategoryLabel remove_html="1"$></a>
      </mt:SetVarBlock>
    </mt:Categories>
    <$mt:Var name="categories" function="count" setvar="cat_count"$>
    <$mt:Var name="cat_count" op="%" value="$num_cols" setvar="modulus"$>
    <mt:If name="modulus" gt="0">
      <$mt:Var name="cat_count" op="-" value="$modulus" setvar="cat_count_minus_mod"$>
      <$mt:Var name="cat_count_minus_mod" op="/" value="$num_cols" setvar="cats_per_col"$>
      <$mt:Var name="cats_per_col" op="+" value="1" setvar="cats_per_col"$>
    <mt:Else>
      <$mt:Var name="cat_count" op="/" value="$num_cols" setvar="cats_per_col"$>
    </mt:If>
    <mt:SetVarTemplate name="for_inner">
      <$mt:Var name="index" op="++" setvar="index"$>
      <mt:Unless name="index" gt="$cat_count">
        <$mt:Var name="categories{$index}"$>
      </mt:Unless>
    </mt:SetVarTemplate>

    <$mt:Var name="index" value="0"$>
    <$mt:Var name="col_num" value="1"$>
    <mt:For from="1" to="$num_cols">
      <div class="col<$mt:Var name="col_num"$>">
        <mt:For from="1" to="$cats_per_col">
          <$mt:Var name="for_inner"$>
        </mt:For>
      </div>
      <$mt:Var name="col_num" op="++" setvar="col_num"$>
    </mt:For>

## Credits

Example contributed by [601am](http://601am.com).
