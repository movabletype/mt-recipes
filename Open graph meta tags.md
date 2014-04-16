## Description

Many websites add special HTML `meta` tags following the [Open Graph protocol](http://ogp.me/) to define specific information about a web page to make sharing on social networks like Facebook more effective. Some Movable Type template logic can be employed to intelligently generate these `meta` tags for any published template.

## Details

The following example assumes you have previously defined the page URL in a variable `self_url`, which is detected with PHP below if not set.
Alternatively, you can generate the URL using logic from the [Canonical link](Canonical link.md) recipe.

    <mt:Unless name="system_template">
      <meta property="og:site_name" content="<$mt:BlogName encode_html="1"$>" />
      <meta property="fb:admins" content="<$mt:Var name="fb_app_id"$>" />
      <mt:If name="self_url">
        <meta property="og:url" content="<$mt:Var name="self_url"$>" />
      <mt:Else>
        <meta property="og:url" content="<$mt:BlogURL$><?php echo substr($_SERVER['PHP_SELF'],1); ?>" />
      </mt:If>
      <mt:If tag="ArchiveType" eq="Individual">
        <mt:EntryAssets limit="1"><$mt:AssetURL setvar="image_url"$><$mt:BlogURL setvar="blog_url"$></mt:EntryAssets>
        <meta property="og:type" content="article"/>
        <meta property="og:title" content="<$mt:EntryTitle encode_html="1"$>" />
        <meta property="og:image" content="<$mt:Var name="image_url"$>" />
        <meta property="og:description" content="<$mt:EntryExcerpt encode_html="1"$>" />
      <mt:Else tag="ArchiveType" eq="Page">
        <mt:PageAssets limit="1"><$mt:AssetURL setvar="image_url"$><$mt:BlogURL setvar="blog_url"$></mt:PageAssets>
        <meta property="og:type" content="article"/><mt:Ignore>matches better than website I think</mt:Ignore>
        <meta property="og:title" content="<$mt:PageTitle encode_html="1"$>" />
        <meta property="og:image" content="<$mt:Var name="image_url"$>" />
        <meta property="og:description" content="<$mt:PageExcerpt encode_html="1"$>" />
      <mt:Else tag="ArchiveType">
        <meta property="og:type" content="website"/>
        <meta property="og:title" content="<$mt:BlogName encode_html="1"$>: <$mt:ArchiveTitle encode_html="1"$>" />
        <meta property="og:image" content="<$mt:BlogURL$>PATH_TO_A_DEFAULT_IMAGE" />
        <meta property="og:description" content="<$mt:ArchiveTitle encode_html="1"$>" />
      <mt:Else>
        <meta property="og:type" content="website"/>
        <meta property="og:title" content="<$mt:BlogName encode_html="1"$>" />
        <meta property="og:image" content="<$mt:BlogURL$>PATH_TO_A_DEFAULT_IMAGE" />
        <meta property="og:description" content="<$mt:BlogDescription encode_html="1"$>" />
      </mt:If>
    </mt:Unless>

## Credits

Example contributed by [601am](http://601am.com).
