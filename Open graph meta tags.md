<$mt:Include module="Set Self URL"$>
<mt:Unless name="system_template">
<meta property="og:site_name" content="<$mt:BlogName encode_html="1"$>" />
<meta property="fb:admins" content="<$mt:Var name="fb_app_id"$>" />
<mt:If name="self_url">
  <meta property="og:url" content="<$mt:Var name="self_url"$>" />
<mt:Else>
  <meta property="og:url" content="<$mt:BlogURL$><?php echo substr($_SERVER['PHP_SELF'],1); ?>" />
</mt:If>
<mt:If tag="ArchiveType" eq="Individual">
  <mt:EntryAssets limit="1"><$mt:AssetURL setvar="image_url"$><$mt:BlogURL setvar="blog_url"$><$mt:Var name="image_url" strip_linefeeds="1" trim="1" replace="$blog_url","http://cdn.consumerist.com/" setvar="image_url"$></mt:EntryAssets>
  <meta property="og:type" content="article"/>
  <meta property="og:title" content="<$mt:EntryTitle encode_html="1"$>" />
  <meta property="og:image" content="<$mt:Var name="image_url"$>" />
  <meta property="og:description" content="<$mt:EntryExcerpt encode_html="1"$>" />
<mt:Else tag="ArchiveType" eq="Page">
  <mt:PageAssets limit="1"><$mt:AssetURL setvar="image_url"$><$mt:BlogURL setvar="blog_url"$><$mt:Var name="image_url" strip_linefeeds="1" trim="1" replace="$blog_url","http://cdn.consumerist.com/" setvar="image_url"$></mt:PageAssets>
  <meta property="og:type" content="article"/><mt:Ignore>matches better than website I think</mt:Ignore>
  <meta property="og:title" content="<$mt:PageTitle encode_html="1"$>" />
  <meta property="og:image" content="<$mt:Var name="image_url"$>" />
  <meta property="og:description" content="<$mt:PageExcerpt encode_html="1"$>" />
<mt:Else tag="ArchiveType">
  <meta property="og:type" content="website"/>
  <meta property="og:title" content="<$mt:BlogName encode_html="1"$>: <$mt:ArchiveTitle encode_html="1"$>" />
  <meta property="og:image" content="<$mt:BlogURL$>css/images/default.gif" />
  <meta property="og:description" content="<$mt:ArchiveTitle encode_html="1"$>" />
<mt:Else>
  <meta property="og:type" content="website"/>
  <meta property="og:title" content="<$mt:BlogName encode_html="1"$>" />
  <meta property="og:image" content="<$mt:BlogURL$>css/images/default.gif" />
  <meta property="og:description" content="<$mt:BlogDescription encode_html="1"$>" />
</mt:If>
</mt:Unless>