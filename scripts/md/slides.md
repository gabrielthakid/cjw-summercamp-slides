title: Presenters
class: big
build_lists: true

<!---

  eZ Summercamp 2015 Talk

  Multiple Colors of Migration

  (c) 2015 Ekkehard Doerre, Donat Fritschy, Jan Meier, Martin Wilde, Felix Woldt, Dirk Lampe, Gabriel Werzner Regalado


-->
* <strong>Ekke</strong> is a consultant with deep knowledge in eZ Publish 4 and 5, eZ Find / Apache Solr and with a faible for coming cutting edge web technologies. He is one of the organizers of the PHP Unconference since eight years.
* <strong>Donat</strong> is owner of Webmanufaktur, a full service web agency in Switzerland. He works as projects manager, software architect and developer and likes thinking outside of the box. In the last year he has been involved in major pure eZ 5 projects.

* Members of CJW Network

---

title: Multiple Colors of Migration

- There are still many (too much) eZ Publish legacy sites 
- eZ Publish 5.4 / 2014.11 is supported until May 2019
- So there is a stable business base for the next 4 years
- And since one year in internet is seven years in real live, 28 years of best business!
- **Why waiting? OK, we try to help you with arguments and know how**

- <https://github.com/cjw-network/cjw-summercamp-slides/blob/master/Multiple-Colors-of-Migration.pdf>


---

title: Who is in the audience?
subtitle: Let us know you better ...


- Who has realized eZ Publish 5 sites (productive)?
- Who has realized pure eZ Publish 5 sites (no legacy)?

---

title: DOING Agenda

Things we would like to discuss:

- Reasons for not waiting any more
- Run legacy only
- Run eZ Publih 5 Symfony stack only
- Your fast (easy) way to pure TWIG Templates
 

---

title: Why waiting?
subtitle: Pro and cons
class: segue dark nobackground

---

title: What are the problems?
subtitle: Still hard to start but we prepared a lot

- no starting point: a good eZ Publish version like 4.7 is missing -> cjwpublish1411
- <https://github.com/cjw-network/cjwpublish1411>
- many logic is in templates, everything new, everything different?
- no multi site / multi repository setup
- performance, performance, performance,

---

title: Why waiting?
subtitle: Financial reasons - How to sell it to your customer?


- update / upgrade - but still no new feature for editors
- many security fixes - but often part of maintenance support

- Relaunch: Make responsive, look at <http://getbootstrap.com> or <http://foundation.zurb.com/>
- Relaunch: Mobile first, it is coming to marketing people
- new feature mobile editing
- Do you have one more?

---

title: Why waiting?
subtitle: Technical reasons for starting now


- it is on the upgrade path to eZ Platform 6
- many security and bug fixes
- TWIG for new templates and fallback to old templates when needed
- easy to extend with Symfony bundles, there are more than 2500 on e.g. <http://knpbundles.com/>
- switch to responsive web design and make it mobile first

---

title: Which version to use?
subtitle: We need a version as a stable base for the next 4 years

- eZ Publish 5.3 / 5.4 aka 2014.11 is supported until May 2019
- but many fixes are in the legacy bridge (-)
- but newer versions are pre alpha (+)
- but there is no real save version to switch (-)
- solution take our cjwpublish1411 and help to keep it fresh (+)

---

title: Run legacy only
subtitle:
class: segue dark nobackground

---

title: Run legacy only 
subtitle: Short introduction

- if you only need the bug fixes and security patches in legacy
- our arguments won't convince you or your customer
- the installation has more than 150 extensions
- then link your requests into the legacy folder
- go the upgrade path <https://doc.ez.no/display/EZP/Upgrade>
- and read more <https://doc.ez.no/display/EZP/Legacy+code+and+features>
- but we advice you to go to "Run Symfony only"

---

title: Run Symfony only
subtitle:
class: segue dark nobackground

---

title: Team up with a Symfony crack

- To be honest: as eZ 4 developers, we are complete novices in eZ 5
- It's easier for a Symfony crack to learn eZ than other way round
- Symfony community is hungry for a CMS, so watch out for new competition
- But @Symfony cracks: It's not easy: an eZ Publish and CMS expert will reduce your risk
- And will make your content architecture better and more maintainable
- **OR take the shortcut for integrators**

---

title: CjwPublishToolsBundle
subtitle: Your easy way to eZ Publish Symfony
class: segue dark nobackground

---

title: CjwPublishToolsBundle
subtitle:  for integrators of small to medium sites

- He comes from front end design and speaks fluent HTML and CSS
- He has no problems with digging into template languages
- He prefers solutions with all needed functionality
- He wants to develop web sites fast and easy at low cost
- <https://github.com/cjw-network/CjwPublishToolsBundle>

---

title: Treemenu

<img src="images/treemenu.png" alt="" width="613" style="margin-top:-30px">

<li>
<pre class="prettyprint" data-lang="Twig">
{% set treemenu = cjw_treemenu( locationId, {
                      'depth': '2',
                      'offset': '1',
                      'include': [ 'cjw_article', 'cjw_folder', 'cjw_feedback_form' ],
                      'sortby': { 'LocationPriority': 'ASC' },
                      'datamap': false } ) %}
</pre>
</li>
<li>
<pre class="prettyprint" data-lang="Twig">
{% for item in treemenu %}
    {{ ez_content_name( item.node.contentInfo ) }}   
{% endfor %}
</pre>
</li>

---

title: Breadcrumb
subtitle: cjw_breadcrumb

<img src="images/breadcrumb.png" alt="" width="421" style="margin-top:-30px">

<li>
<pre class="prettyprint" data-lang="Twig">
{% set path = cjw_breadcrumb( locationId, { 'offset': '1',
                                            'rootName': 'Home',
                                            'separator': '' } ) %}
{% for item in path.items %}   
       {{ item.name }}        
{% endfor %}
</pre>
</li>

---

title: Folder with line view screenshot

<img src="images/folder_with_line_view.png" alt="" width="527" style="margin-top:-30px">


---

title: Folder with line view source code
subtitle: cjw_fetch_content

<li>
<pre class="prettyprint" data-lang="Twig">
{% set listChildren = cjw_fetch_content( [ location.id ], { 'depth': '1',
        'limit': listLimit,
        'offset': listOffset,
        'include': [ 'cjw_folder', 'cjw_article', 'cjw_folder_section', 'cjw_file'  ],
        'language': [],
        'datamap': false,
        'count': true } )[ location.id ] %}
</pre>
</li>
<li>
<pre class="prettyprint" data-lang="Twig">        
{% for child in listChildren['children'] %}
    {#{{ render( controller( "ez_content:viewLocation", 
                            {'location': child, 'viewType': 'line'} ) ) }}#}
    {{ cjw_render_location( {'location': child, 'viewType': 'line'} )  }}

                
{% endfor %}
</pre>
</li>

---

title: Pagination (was called Google navigator)


<img src="images/pagination.png" alt="" width="529" style="margin-top:-50px">

- Twig Template
- <https://github.com/cjw-network/CjwPublishToolsBundle/blob/master/Resources/views/parts/navigator.html.twig>

---

title: Article full view screenshot


<img src="images/article_full_view.png" alt="" width="741" style="margin-top:-30px">

---

title: Article full view source code
class: smaller

<li>
<pre class="prettyprint" data-lang="Twig">
{% extends site_bundle_name ~ '::pagelayout.html.twig' %}
{% block content %}

    {% if content.fields.title is defined and not ez_is_field_empty( content, 'title' ) %}
        {{ ez_field_value( content, 'title' ) }}
    {% endif %}
    
    {% if content.fields.short_description is defined and not ez_is_field_empty( content, 'short_description' ) %}
        {{ ez_render_field( content, 'short_description' ) }}
    {% endif %}
    
    {% if content.fields.image is defined and not ez_is_field_empty( content, 'image' ) %}
        {{ ez_render_field( content, 'image', 
                    {parameters: {alias: 'medium', class: 'imageleft'}} ) }}
    {% endif %}

{% endblock %}
</pre>
</li>

---

title: TODO Multi language
subtitle: 
build_lists: true

<img src="images/ed-de-01.png.png" alt="" width="612" style="margin-top:-30px">


---

title: Feedback Form (infocollector) I
subtitle: what is it doing

- cjw_feedback_form => with infocollector using CjwPublishToolsBundle eZ Publish content type mapping to symfony form handling

    - Symfony form validation and form rendering is used
    => ez contenttype cjw_feedback_form  
    => with infocollector attributes 
    => will be render a symfony form which will
    => store content into infocollector table and will send an email


---

title: Feedback Form (infocollector) I

    Define custom formbuilder.yml which will be load for this project
    
    src/Cjw/SiteCjwpublishBundle/app/config/parameters.yml
  <li>
   <pre class="prettyprint" data-lang="yaml">   
        parameters:
            # Filepath + -name for formbuilder Config, from EZROOT directory => sitaccessaware config
            # set default config for all siteaccesses can be overitten by siteaccess or siteaccessgroup if you 
            # need a separate formbuilderconfig
            cjw_publishtools.default.formbuilder.config_file: src/Cjw/SiteCjwpublishBundle/Resources/config/formbuilder.yml
    </pre>
    </li>

---

title: Feedback Form (infocollector) I


    example for defining an infocollector for of ezpublish content type / class  'cjw_feedback_form
    src/Cjw/SiteCjwpublishBundle/Resources/config/formbuilder.yml
    
 <li>
 <pre class="prettyprint" data-lang="yaml">       
        ...
        formcollector_config:
            parameters:
                button_config:
                    save_button:
                        label:  cjw_publishtools.formbuilder.default.button.send
                    cancel_button: false
            types:
                cjw_feedback_form:
                    handler:
                        infocollector:
        #                sendmail:
        #                    email_sender: @email
        #                    email_subject: @subject
                        success:
                            template: :form:success.html.twig
    
</pre>
</li>




---

title: Frontend editing
subtitle: Example configuration YAML file
build_lists: true

<li>
    <pre>
button_label_config:
    cancel_button_label: cjw_publishtools.formbuilder.default.button.cancel
    save_button_label: cjw_publishtools.formbuilder.default.button.save
frontendediting_config:
    parameters:
        template: :edit.html.twig

        button_config:
            save_button:
                label: cjw_publishtools.formbuilder.default.button.save
            cancel_button:
                label: cjw_publishtools.formbuilder.default.button.cancel

    handler:
        success:
            handler_class: successHandler
            template: ':email:user_register.html.twig'
    types:
        user:
            parameters:
                template: :user:edit.html.twig
            handler:
            fields:
                - first_name
                - last_name
                - user_account
    </pre>
</li>

---

title: Frontend editing
subtitle: Example TWIG template
build_lists: true

<li>
    <pre>
{% extends site_bundle_name ~ '::pagelayout.html.twig' %}

{% block content %}
    <div class="class-form content-view-edit">
        {#{{ include( site_bundle_name ~ ':parts:breadcrumb.html.twig' ) }}#}

        {#<div id="content-right">#}
            {#{{ include( site_bundle_name ~ ':parts:menu_user.html.twig' ) }}#}
        {#</div>#}

        <div id="content-main">
            <h1 class="content-header">Edit</h1>

            {{ form(form) }}

        </div>
    </div>

{% endblock %}
    </pre>
</li>

---

title: TODO, aus 2014 Multi-Site/Multi-Repository Setup
subtitle:
class: segue dark nobackground

---

title: Why a Multi-Site/Multi-Repository Setup?

* At CJW Network we have developed a multi-site/multi-repository setup for eZ Publish 4 several years ago
* This allows us to host many individual sites on a single eZ Publish installation

Advantages:

* Central site administration (site activation, cronjobs, ...)
* Easy deployment (update site extension with Subversion)
* Highly reduced maintenance costs (security patches, upgrades)
* Highly efficient use of hardware resources

Disadvantages:

* Some Kernel patches needed

---

title: TODO, aus 2014Multi-Site/Multi-Repository Setup in eZ 5
build_lists: fade


*First Approach (proven in production and depreciated)*

*  *Use different ezpublish app directories to host the different sites*


**Second approach (proven in production)**

* Use TODO ab hier bitte überarbeiten: `CJW MultiSiteBundle`

---

title: TODO, aus 2014Introducing CJW MultiSiteBundle
build_lists: true

Although the first approach works fine, it has several drawbacks:

* Application code scattered at different places (site directory, bundle, legacy extension), hard to maintain in VCS, hard to deploy
* Redundancy in config files
* No global settings
* No central site activation/administration

* Goal: keep everything in one place!

---

title: TODO, aus 2014CJW MultiSiteBundle Features
build_lists: true

* Boots kernel and environment based on domain name mappings
* Handles local, staging and live domain names
* Allows for global activation of bundles
* Allows for global settings
* Provides a common console for all sites
* Caches domain name mappings
* Moves cache and log files away from the ezpublish folder
* more to come ...

---

title: TODO, aus 2014cjwpublish Directory

The `cjwpublish` application directory sits next to the `ezpublish` directory.

<pre class="">
cjwpublish
&#8990; config
    cjwpublish.yml                  &lt;-- defines active bundles
    config.yml                      &lt;-- allows for global settings
  CjwPublishKernel.php              &lt;-- inherits from CjwMultiSiteKernel.php
  CjwPublishCache.php               &lt;-- inherits from CjwMultiSiteCache.php
  console
</pre>

---

title: TODO, aus 2014Symfony's app directory is back

Site Bundle Directory Layout

<pre class="">
src
&#8990; Cjw
  &#8990; SiteExampleBundle
    &#8990; app
      &#8990; config
          cjwpublish.yml            &lt;-- contains domain mappings
          config.yml
          ezpublish.yml
          ...
        CjwSiteExampleKernel.php    &lt;-- inherits from CjwPublishKernel.php
        CjwSiteExampleCache.php     &lt;-- inherits from CjwPublishCache.php
    &#8990; Controller
      ...
</pre>

---

title: TODO, aus 2014Caveats

Adjustments needed in `config.yml` to reflect different relative location of kernel

<pre class="prettyprint" data-lang="yml">
assetic:
    ...
    read_from:      %kernel.root_dir%/../../../../web
    write_to:       %kernel.root_dir%/../../../../web
    ...
ez_publish_legacy:
    ...
    root_dir: %kernel.root_dir%/../../../../ezpublish_legacy

parameters:
    ezpublish.kernel.root_dir: %kernel.root_dir%/../../../../vendor/ezsystems/ezpublish-kernel
</pre>

**More problems of this kind expected!**

---

title: TODO, aus 2014 Project Status TODO

* Currently in private Beta, not yet released
* Ideas and Feedback welcome
* Public Beta in October

* <mailto:info@cjw-network.com>
* <https://github.com/cjw-network/MultiSiteBundle>

---

title: Ressources

Slides as PDF

* <https://github.com/cjw-network/cjw-summercamp-slides/blob/master/Multiple-Colors-of-Migration.pdf>


Slides (Source)

* <https://github.com/cjw-network/cjw-summercamp-slides>

CJW MultiSiteBundle TODO link to cjwpublish

* <https://github.com/cjw-network/MultiSiteBundle>

CJW Publish for quick start
* <https://github.com/cjw-network/cjwpublish1411>
* <mailto:info@cjw-network.com>

---

title: <a href="http://vote.netgenlabs.com/" style="color:#fff;">http://vote.netgenlabs.com/</a>
subtitle: Please Vote!
class: segue dark nobackground


