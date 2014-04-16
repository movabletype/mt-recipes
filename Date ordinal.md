## Description

Generate the two character suffix on the day number, such as the "th" in "13th", using any date tag as input.

## Details

Assign any date tag with format `%d` to a variable `day`, and then create a new variable `day_suffix` based on the day number.

    <$mt:CommentDate format="%d" setvar="day"$>
    <mt:If name="day" eq="01"><$mt:Var name="day_suffix" value="st"$>
    <mt:Else name="day" eq="02"><$mt:Var name="day_suffix" value="nd"$>
    <mt:Else name="day" eq="03"><$mt:Var name="day_suffix" value="rd"$>
    <mt:Else name="day" eq="21"><$mt:Var name="day_suffix" value="st"$>
    <mt:Else name="day" eq="22"><$mt:Var name="day_suffix" value="nd"$>
    <mt:Else name="day" eq="23"><$mt:Var name="day_suffix" value="rd"$>
    <mt:Else name="day" eq="31"><$mt:Var name="day_suffix" value="st"$>
    <mt:Else><$mt:Var name="day_suffix" value="th"$></mt:If>

Then output the variable as needed.

    <$mt:CommentDate format="%b %e"><$mt:Var name="day_suffix"$>

## Credits

Example contributed by [601am](http://601am.com).
