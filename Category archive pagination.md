## Description

Movable Type category page with `mt-search.cgi` powered pagination and nine generated page numbers relative to current page. Requires PHP.

## Examples

    <$mt:Var name="entries_per_page" value="7"$>

    <mt:SetVarBlock name="pager_block">
      <mt:Section strip_linefeeds="1">
        <mt:If tag="ArchiveType"><$mt:ArchiveCount setvar="total_entries"$><mt:Else><$mt:BlogEntryCount setvar="total_entries"$></mt:If>
        <mt:If name="total_entries" gt="$entries_per_page">
          <mt:If name="total_entries" op="%" value="$entries_per_page" eq="0">
            <$mt:Var name="total_entries" op="/" value="$entries_per_page" setvar="total_pages"$>
          <mt:Else>
            <$mt:Var name="total_entries" op="%" value="$entries_per_page" setvar="remainder"$>
            <$mt:Var name="total_entries" op="-" value="$remainder" setvar="total_entries"$>
            <$mt:Var name="total_entries" op="/" value="$entries_per_page" setvar="total_pages"$>
            <$mt:SetVar name="total_pages" op="++"$>
          </mt:If>
          <mt:If name="total_pages" gt="1">
            <div class="pageNumberSelector unlimited">
              <mt:If name="search_results">
                <mt:Ignore>Next IF should be redundant as the prev link should only show on search result based pages</mt:Ignore>
                <mt:If name="request.page" gt="1">
                  <a class="previousButton" href="?p=<$mt:Var name='request.page' op='--'$>">&nbsp;</a>
                </mt:If>
              </mt:If>
              <div class="pageNumberLinks <mt:If name='search_results'>pageNumberLinksGenerated</mt:If>">
                <mt:If name="search_results">
                  <a href="?p=1">&laquo;&nbsp;</a>
                </mt:If>
                <mt:If name="search_results">
                  <$mt:Var name="request.page" setvar="p"$>
                  <$mt:Var name="total_pages" op="-" value="$p" setvar="pagesToEnd"$>
                  <mt:If name="total_pages" le="9">
                    <$mt:Var name="fromPage" value="1"$>
                    <$mt:Var name="total_pages" setvar="toPage"$>
                  <mt:Else name="pagesToEnd" le="4">
                    <$mt:Var name="total_pages" op="-" value="8" setvar="fromPage"$>
                    <$mt:Var name="total_pages" setvar="toPage"$>
                  <mt:Else name="p" lt="5">
                    <$mt:Var name="fromPage" value="1"$>
                    <$mt:Var name="fromPage" op="+" value="8" setvar="toPage"$>
                  <mt:Else>
                    <$mt:Var name="p" op="-" value="4" setvar="fromPage"$>
                    <$mt:Var name="p" op="+" value="4" setvar="toPage"$>
                  </mt:If>
                  <mt:For from="$fromPage" to="$toPage" step="1">
                    <mt:If name="__index__" eq="$p">
                      <span class="current"><$mt:Var name="__index__"$></span>
                    <mt:Else>
                      <a href="?p=<$mt:Var name='__index__'$>"><$mt:Var name="__index__"$></a>
                    </mt:If>
                    <mt:If name="__index__" le="9">&nbsp;</mt:If>
                  </mt:For>
                <mt:Else>
                  <mt:If name="total_pages" le="9">
                    <$mt:Var name="total_pages" setvar="last_visible"$>
                  <mt:Else>
                    <$mt:Var name="last_visible" value="9"$>
                  </mt:If>
                  <mt:For from="1" to="$last_visible" step="1">
                    <mt:If name="__first__">
                      <span class="current">1</span>
                    <mt:Else>
                      <a href="?p=<$mt:Var name='__index__'$>"><$mt:Var name="__index__"$></a>
                    </mt:If>
                    <mt:If name="__index__" le="9">&nbsp;</mt:If>
                  </mt:For>
                </mt:If>
                <mt:If name="search_results">
                  <$mt:Var name="request.page" setvar="p"$>
                  <mt:If name="p" lt="$total_pages">
                    <a href="?p=<$mt:Var name="total_pages"$>">&nbsp;&raquo;</a>
                  </mt:If>
                <mt:Else>
                  <a href="?p=<$mt:Var name="total_pages"$>">&nbsp;&raquo;</a>
                </mt:If>
              </div>
              <mt:If name="search_results">
                <mt:If name="request.page" lt="$total_pages">
                  <a class="nextButton" href="?p=<$mt:Var name='request.page' op='++'$>">&nbsp;</a>
                </mt:If>
              <mt:Else>
                <a class="nextButton" href="?p=2">&nbsp;</a>
              </mt:If>
            </div>
          </mt:If>
        </mt:If>
      </mt:Section>
    </mt:SetVarBlock>

    <mt:Ignore><!-- Construct the url for querying entries. --></mt:Ignore>
    <mt:SetVarBlock name="search_link">
        <$mt:CGIPath$><$mt:SearchScript$>?IncludeBlogs=<$mt:BlogID$>
        &template_id=<$mt:BuildTemplateID$>
        &limit=<$mt:Var name="entries_per_page"$>
        <mt:If name="archive_template">
            &archive_type=<$mt:ArchiveType$>
            <mt:If name="datebased_archive">
                &year=<$mt:ArchiveDate format='%Y'$>&month=<$mt:ArchiveDate format='%m'$>&day=<$mt:ArchiveDate format='%d'$>
            </mt:If>
            <mt:If name="category_archive">
                &category=<$mt:CategoryID$>
            </mt:If>
            <mt:If name="author_archive">
                &author=<$mt:AuthorID$>
            </mt:If>
        <mt:Else>
            &archive_type=Index
        </mt:If>
        &page=
    </mt:SetVarBlock>
    <mt:Ignore><!-- Strip spaces and trim value. --></mt:Ignore>
    <$mt:Var name="search_link" strip="" trim="1" setvar="search_link"$>

    <mt:If name="search_results">
      <mt:If name="request.pager" eq="1">
        <$mt:Var name="pager_block"$>
      <mt:Else>
        <mt:Entries limit="$entries_per_page" search_results="1">
          <$mt:Include module="Latest Posts - Entry Listing"$>
        </mt:Entries>
      </mt:If>
    <mt:Else>
      <mt:SetVarBlock name="pagetitle"><mt:ArchiveTitle></mt:SetVarBlock>
      <mt:Include module="SEO - Header">
      <div class="grid_12"></div>
      <div class="spacer"></div>
      <div class="clear"></div>
      <!-- BEGIN MAIN CONTENT AREA -->
      <div class="grid_8" id="mainContent">
        <mt:Include module="Hero - Entry Listing">
        <!-- BEGIN Category Posts -->
        <div class="spacer"></div>
        <h4 class="titleHead">Latest Posts in <mt:ArchiveTitle></h4>
        <div class="categoryContainer">
          <?php
            $page = intval($_REQUEST['p']);
            if ( empty($page) || $page < 1 ) { $page = 1; }
            if ( $page == 1 ) {
          ?>
              <mt:Entries lastn="$entries_per_page">
                <$mt:Include module="Latest Posts - Entry Listing"$>
              </mt:Entries>
          <?php
            } else {
              readfile('<$mt:Var name="search_link"$>'.$page);
            }
          ?>
        </div>
        <?php
          if ( $page == 1 ) {
        ?>
            <$mt:Var name="pager_block"$>
        <?php
          } else {
            readfile('<$mt:Var name="search_link"$>'.$page.'&pager=1');
          }
        ?>
        <!-- END Category Posts -->
        <div class="clear"></div>
        <div class="grid_4 alpha" id="mainLeftBar">
        </div>
        <div class="grid_4 omega" id="mainRightBar">
        </div>
        <div class="clear"></div>
        <div class="mainContentLower2">
          <div class="spacer"></div>
        </div>
      <!-- END MAIN CONTENT AREA -->
      </div>
      <?php include ('<mt:BlogSitePath>inc/sidebar.php') ; ?>
      <?php include ('<mt:BlogSitePath>inc/footer.php') ; ?>
    </mt:If>

## Credits

Example contributed by [601am](http://601am.com).
