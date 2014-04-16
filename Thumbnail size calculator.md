This works currently within the context of an asset.

Set desired maximum height and width as variables "x2" and "y2"
Example usage on last line

<mt:SetVarTemplate name="thumb_attribs">
  <$mt:Var name="x2" value="325"$>
  <$mt:Var name="y2" value="265"$>
  <$mt:AssetProperty property="image_width" setvar="x1"$>
  <$mt:AssetProperty property="image_height" setvar="y1"$>
  <$mt:Var name="x3" value="$x1"$>
  <$mt:Var name="y3" value="$y1"$>
  <$mt:AssetThumbnailURL setvar="url"$>
  <$mt:Var name="OR" value="0"$>
  <mt:If name="x1" ge="$x2"><$mt:Var name="OR" value="1"$></mt:If>
  <mt:If name="y1" ge="$y2"><$mt:Var name="OR" value="1"$></mt:If>
  <mt:If name="OR">
    <$mt:Var name="x2" op="/" value="$x1" setvar="rx"$>
    <$mt:Var name="y2" op="/" value="$y1" setvar="ry"$>
    <mt:If name="rx" gt="$ry">
      <$mt:Var name="ry" setvar="r"$>
    <mt:Else>
      <$mt:Var name="rx" setvar="r"$>
    </mt:If>
    <$mt:Var name="x1" op="*" value="$r" sprintf="%.0f" setvar="x3"$>
    <$mt:Var name="y1" op="*" value="$r" sprintf="%.0f" setvar="y3"$>
    <$mt:AssetThumbnailURL height="$y3" setvar="url"$>
  </mt:If>
  src="<$mt:Var name="url"$>" height="<$mt:Var name="y3"$>" width="<$mt:Var name="x3"$>"
</mt:SetVarTemplate>

<mt:EntryLinkedAssets field="image">
  <img <$mt:Var name="thumb_attribs"$> alt="" />
</mt:EntryLinkedAssets>