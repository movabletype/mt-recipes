## Description

You might have a form with options corresponding to possible entry listing archives, such as year, month and category. You could point that form to this PHP script to then redirect the user to the corresponding file if it exists, and redirect to a not found page if it does not exist.

## Details

This script takes URL parameters `language_path`, `category`, `year` and `month` and
assigns to variables `$p`, `$c`, `$y` and `$m`. It is assumed `language_path` and `category`
will consist of alphanumeric or underscore/hyphen characters, and the `year` and
`month` will be integers.

The user is redirected to the appropriate predictable archive listing URL if it
exists, otherwise user is redirected to a "no results" page.

**TO DO:** If user specifies a month but no year, currently no "invalid" message is
displayed, but rather we just redirect to the "no results" page.

    <?php

    $debug = false;

    if($debug){echo $_SERVER['QUERY_STRING']."<br />\n";}

    $p = isset($_GET['language_path']) ? preg_replace('/[^a-z0-9-_]/i','',$_GET['language_path'])  : ''    ;
    $c = isset($_GET['category'])      ? preg_replace('/[^a-z0-9-_]/i','',$_GET['category'])       : false ; // this is mt:CategoryID required for mt-search.cgi
    $y = isset($_GET['year'])          ? strval(intval($_GET['year']))                             : false ;
    $m = isset($_GET['month'])         ? intval($_GET['month'])                                    : false ;

    if( strlen($p) > 0 ){ $p .= '/'; }
    $blog_url  = str_replace('/main/','/main/'.$p,'<$mt:BlogURL$>');
    $blog_path = str_replace('/main/','/main/'.$p,'<$mt:BlogSitePath$>');
    $params    = '?category='.$c.'&year='.str_pad($y,4,'0',STR_PAD_LEFT).'&month='.str_pad($m,2,'0',STR_PAD_LEFT);
    $options   = '';

    if($debug){echo $params."<br />\n";}

    if ($c) {
      if($debug){echo '$c is true: '.$c."<br />\n";}
      switch ($c) {
        <mt:Categories>
          case <$mt:CategoryID$>: $c = '<$mt:CategoryBasename$>'; break;
        </mt:Categories>
      }
      if($debug){echo '$c is now: '.$c."<br />\n";}
    }

           if( $c && $y && $m ){
      $options = $c.'/'.str_pad($y,4,'0',STR_PAD_LEFT).'/'.str_pad($m,2,'0',STR_PAD_LEFT);
      if($debug){echo "e1<br />\n";}
    } else if( $c && $y       ){
      $options = $c.'/'.str_pad($y,4,'0',STR_PAD_LEFT);
      if($debug){echo "e2<br />\n";}
    } else if( $c       && $m ){
      if($debug){echo '$c && $m is true<br />\n';}
      $params .= '&nonefound';
    } else if( $c             ){
      $options = $c;
      if($debug){echo "e3<br />\n";}
    } else if(       $y && $m ){
      $options = str_pad($y,4,'0',STR_PAD_LEFT).'/'.str_pad($m,2,'0',STR_PAD_LEFT);
      if($debug){echo "e4<br />\n";}
    } else if(       $y       ){
      $options = str_pad($y,4,'0',STR_PAD_LEFT);
      if($debug){echo "e5<br />\n";}
    } else if(             $m ){
      if($debug){echo '$m is true'."<br />\n";}
      $params .= '&nonefound';
    }

    if( strlen($options) > 0 ){
      $target_file = $options.'/index.html';
    } else {
      $target_file = 'index.html';
    }
    if( !file_exists( $blog_path.$target_file ) ){
      if($debug){echo 'FALSE: file_exists('.$blog_path.$target_file.")<br />\n";}
      $target_file = 'index.html';
      $params .= '&nonefound';
    }

    if($debug){
      echo 'Location: '.$blog_url.$target_file.$params."<br />\n";
    } else {
      header( 'Location: '.$blog_url.$target_file.$params );
    }

    ?>

The form code could look something like this (jQuery is used in the `script` block following.):

    <form name="listingchooser" id="listingChooserForm" action="<$mt:BlogURL$>listingchooser.html" method="get">
      <div class="searchFormText">View by Date and Category:</div>
      <input type="hidden" name="language_path" value="<$mt:Var name="language_path" replace="/",""$>" />
      <select name="month">
        <option value="0"<?php  if(isset($_GET['month']) && !strcmp($_GET['month'],'0'))  echo " selected"; ?>>All months</option>
        <option value="01"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'01')) echo " selected"; ?>>January</option>
        <option value="02"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'02')) echo " selected"; ?>>February</option>
        <option value="03"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'03')) echo " selected"; ?>>March</option>
        <option value="04"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'04')) echo " selected"; ?>>April</option>
        <option value="05"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'05')) echo " selected"; ?>>May</option>
        <option value="06"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'06')) echo " selected"; ?>>June</option>
        <option value="07"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'07')) echo " selected"; ?>>July</option>
        <option value="08"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'08')) echo " selected"; ?>>August</option>
        <option value="09"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'09')) echo " selected"; ?>>September</option>
        <option value="10"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'10')) echo " selected"; ?>>October</option>
        <option value="11"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'11')) echo " selected"; ?>>November</option>
        <option value="12"<?php if(isset($_GET['month']) && !strcmp($_GET['month'],'12')) echo " selected"; ?>>December</option>
      </select>
      <select name="year">
        <option value="0"<?php if(isset($_GET['year']) && $_GET['year']==0) echo " selected"; ?>>All years</option>
        <mt:ArchiveList archive_type="Yearly">
          <option value="<$mt:ArchiveTitle$>"<?php if(isset($_GET['year']) && !strcmp($_GET['year'],'<$mt:ArchiveTitle$>')) echo " selected"; ?>><$mt:ArchiveTitle$></option>
        </mt:ArchiveList>
      </select>
      <select name="category">
        <option value="0"<?php if(isset($_GET['category']) && !strcmp($_GET['category'],'0')) echo " selected"; ?>>All categories</option>
        <mt:Categories>
          <option value="<$mt:CategoryID$>"<?php if(isset($_GET['category']) && !strcmp($_GET['category'],'<$mt:CategoryID$>')) echo " selected"; ?>><$mt:CategoryLabel$></option>
        </mt:Categories>
      </select>
      <div id="listingChooserButton" class="dynButton">
        <a class='searchButton' href="#">View</a>
      </div>
    </form>
    <script type="text/javascript">
      $('#searchFormButton').click(function () { $('#searchForm').submit(); });
      $('#listingChooserButton').click(function () { $('#listingChooserForm').submit(); });
    </script>

## Credits

Example contributed by [601am](http://601am.com).
