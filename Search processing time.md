## Description

This recipe shows how to add a line like "This search completed in 1.5 seconds" to your Movable Type generated search results. This could also be used for timing complex pieces of templates or whole templates.

## Details

To time a chunk of template code, create a system or blog level template module called `timing`:

    <mt:If name="part" eq="start">
      <$mt:Date format="%H" setvar="hours"$>
      <$mt:Date format="%M" setvar="minutes"$>
      <$mt:Date format="%S" setvar="seconds"$>
      <$mt:Var name="hours" op="*" value="3600" setvar="hourseconds"$>
      <$mt:Var name="minutes" op="*" value="60" setvar="minuteseconds"$>
      <$mt:Var name="totalseconds" value="$hourseconds"$>
      <$mt:Var name="totalseconds" op="+" value="$minuteseconds" setvar="totalseconds"$>
      <$mt:Var name="totalseconds" op="+" value="$seconds" setvar="totalseconds"$>
      <$mt:Var name="totalseconds" setvar="startseconds"$>
    <mt:Else name="part" eq="stop">
      <$mt:Date format="%H" setvar="hours"$>
      <$mt:Date format="%M" setvar="minutes"$>
      <$mt:Date format="%S" setvar="seconds"$>
      <$mt:Var name="hours" op="*" value="3600" setvar="hourseconds"$>
      <$mt:Var name="minutes" op="*" value="60" setvar="minuteseconds"$>
      <$mt:Var name="totalseconds" value="$hourseconds"$>
      <$mt:Var name="totalseconds" op="+" value="$minuteseconds" setvar="totalseconds"$>
      <$mt:Var name="totalseconds" op="+" value="$seconds" setvar="totalseconds"$>
      <$mt:Var name="totalseconds" setvar="finishseconds"$>
      <$mt:Var name="finishseconds" op="-" value="$startseconds" setvar="elapsedseconds">
      <!-- This search completed in <mt:If name="elapsedseconds" eq="0">less than 1 second<mt:Else name="elapsedseconds" eq="1">1 second<mt:Else><$mt:Var name="elapsedseconds"$> seconds</mt:If>. -->
    </mt:If>

Then, in a template you want to time something in, place these two lines at the start and end of the chunk of interest:

    <$mt:Include module="timing" part="start"$>
    <$mt:Include module="timing" part="stop"$>

This might go at the beginning and end of the "Search Results" system template for a particular blog.

Also, you could of course add a line of output in the "start" section if you want to denote in the output where the timing started.

## Credits

Example contributed by [601am](http://601am.com).
