# rss-pod-link-test

here is my atempt at creating a podcast feed for free using youtube as a host

## Temporal rss feed generator:


https://codepen.io/jon-walstedt/pen/jsIup

source code in html coment

<!--

HTML

<script id="channel-info-template" type="text/x-handlebars-template">
  <?xml version="1.0" encoding="UTF-8"?>
  <rss xmlns:itunes="http://www.itunes.com/dtds/podcast-1.0.dtd" version="2.0">
  <channel>
    <title>{{channelTitle}}</title>
    <link>{{channelLink}}</link>
    <language>{{channelLang}}</language>
    <copyright>{{channelCopyright}}</copyright>
    <itunes:subtitle>{{channelSubtitle}}</itunes:subtitle>
    <itunes:author>{{channelAuthor}}</itunes:author>
    <itunes:summary>{{channelSummary}}</itunes:summary>  
    <itunes:owner>
      <itunes:name>{{channelOwnerName}}</itunes:name>
      <itunes:email>{{channelOwnerEmail}}</itunes:email>
    </itunes:owner>
    <itunes:image href="{{channelImageUrl}}" />
    <itunes:category text="{{channelCategory}}"/>
    {{#each items}}
      <item>
        <title>{{itemTitle}}</title>
        <itunes:author>{{itemAuthor}}</itunes:author>
        <itunes:subtitle>{{itemSubtitle}}</itunes:subtitle>
        <itunes:summary>{{itemSummary}}</itunes:summary>
        <itunes:image href="{{itemImageUrl}}" />
        <enclosure url="{{itemEnclosureUrl}}" length="{{itemEnclosureLength}}" type="{{itemEnclosureType}}"/>
        <guid>{{itemGuid}}</guid>
        <pubDate>{{itemPubDate}}</pubDate>
        <itunes:duration>{{itemDuration}}</itunes:duration>
      </item>
    {{/each}}
  </channel>
  </rss>
</script>

<div class="wrapper">
  <header class="header">
    <div class="header-body">
      <h1>Helper to generate Itunes podcast XML</h1>
      <div class="field">
      <!--<label for="add-item">Add item to existing template</label>
          <input id="add-to-existing" type="checkbox" value="addItem" />-->
      <button id="add-item">Add new item</button>
      <button id="select-code">Select all code</button>
      </div>
      <div class="header-helper-output">
        
      </div>
    </div>
  </header>
  
  <div class="form">
    <form action="#" id="podcast" method="post">

      <fieldset class="channel-info">
        <legend>Channel info</legend>
        <div class="field">
          <label for="channel-title">Title</label>
          <input id="channel-title" name="channelTitle" placeholder="Title" type="text" data-help-text="Add the title of the podcast.<br/> Make your title specific. A podcast entitled 'Our Community Bulletin' is too vague and will attract no subscribers, no matter how compelling the content." />
        </div>
        <div class="field">
          <label for="channel-link">Link</label>
          <input id="channel-link" name="channelLink" placeholder="Link" type="text" data-help-text="Add the url of the podcast. Will be used for website link and arrow in Name column within Itunes"/>
        </div>
        <div class="field">
          <label for="channel-lang">Language</label>
          <input id="channel-lang" name="channelLang" placeholder="en" type="text" data-help-text="Because iTunes operates sites worldwide, it is critical to specify the language of a podcast. Accepted values are those in the <a href='http://www.w3.org/WAI/ER/IG/ert/iso639.htm' target='_blank'>ISO 639-1</a> Alpha-2 list (two-letter language codes, some with possible modifiers, such as 'en-us')."/>
        </div>
        <div class="field">
          <label for="channel-copyright">Copyright</label>
          <input id="channel-copyright" name="channelCopyright" placeholder="Copyright" type="text" data-help-text="The copyright of the podcast content, will not be visible within Itunes"/>
        </div>
        <div class="field">
          <label for="channel-subtitle">Subtitle</label>
          <input id="channel-subtitle" name="channelSubtitle" placeholder="Subtitle" type="text" data-help-text="The contents of this tag are shown in the Description column in iTunes. The subtitle displays best if it is only a few words long." />
        </div>
        <div class="field">
          <label for="channel-author">Author</label>
          <input id="channel-author" name="channelAuthor" placeholder="Author" type="text" data-help-text="The content of this tag is shown in the Artist column in iTunes. If the tag is not present, iTunes uses the contents of the 'author' tag. If 'itunes:author' is not present at the feed level, iTunes will use the contents of 'managingEditor'." />
        </div>
        <div class="field">
          <label for="channel-summary">Summary</label>
          <textarea id="channel-summary" name="channelSummary" placeholder="Summary" data-help-text="The contents of this tag are shown in a separate window that appears when the 'circled i' in the Description column is clicked. It also appears on the iTunes page for your podcast. This field can be up to 4000 characters. If 'itunes:summary' is not included, the contents of the 'description' tag are used."></textarea>
        </div>
        <!--
        <div class="field">
          <label for="channel-description">Description</label>
          <textarea id="channel-description" name="channelDescription" placeholder="Description"></textarea>
        </div>
        --><!-- Description not needed if summary is used-->
        <div class="field">
          <label for="owner-name">Owner name</label>
          <input id="owner-name" name="channelOwnerName" placeholder="Owner name" type="text" data-help-text="This tag contains information that will be used to contact the owner of the podcast for communication specifically about the podcast. It will not be publicly displayed. <br/>Put the email address of the owner in a nested <itunes:email> element."/>
        </div>
        <div class="field">
          <label for="owner-email">Owner email</label>
          <input id="owner-email" name="channelOwnerEmail" placeholder="Owner email" type="text" data-help-text="Put the name of the owner in a nested 'itunes:name' element."/>
        </div>
        <div class="field">
          <label for="channel-image-url">Image url</label>
          <input id="channel-image-url" name="channelImageUrl" placeholder="Image Url" type="text" data-help-text="This tag specifies the artwork for your podcast.iTunes prefers square .jpg images that are at least 1400x1400 pixels, which is different from what is specified for the standard RSS image tag. In order for a podcast to be eligible for an iTunes Store feature, the accompanying image must be at least 1400x1400 pixels."/>
        </div>
        <div class="field">
          <label for="channel-category">Category</label>
          <!--<input id="channel-category" name="channelCategory" placeholder="Category" type="text" data-help-text="Category column and in iTunes Store Browse."/>-->
          <select id="categories-dropdown" class="categories" name="channelCategory" data-help-text="Select category for your podcast. You can manually add more categories after copying the code if needed. Read more about categories here: <a href='https://www.apple.com/itunes/podcasts/specs.html'>https://www.apple.com/itunes/podcasts/specs.html</a>">
    <option value="Arts">Arts</option>
    <option value="Design">Design</option>
    <option value="Fashion">Fashion & Beauty</option>
    <option value="Food">Food</option>
    <option value="Performing Arts">Performing Arts</option>
    <option value="Visual Arts">Visual Arts</option>
    <option value="Business">Business</option>
    <option value="Business News">Business News</option>
    <option value="Careers">Careers</option>
    <option value="Investing">Investing</option>
    <option value="Management & Marketing">Management & Marketing</option>
    <option value="Shopping">Shopping</option>
    <option value="Comedy">Comedy</option>
    <option value="Education">Education</option>
    <option value="Education Technology">Education Technology</option>
    <option value="Higher Education">Higher Education</option>
    <option value="K-12">K-12</option>
    <option value="Language Courses">Language Courses</option>
    <option value="Training">Training</option>
    <option value="Games & Hobbies">Games & Hobbies</option>
    <option value="Automotive">Automotive</option>
    <option value="Aviation">Aviation</option>
    <option value="Hobbies">Hobbies</option>
    <option value="Other Games">Other Games</option>
    <option value="Video Games">Video Games</option>
    <option value="Government & Organizations">Government & Organizations</option>
    <option value="Local">Local</option>
    <option value="National">National</option>
    <option value="Non-Profit">Non-Profit</option>
    <option value="Regional">Regional</option>
    <option value="Health">Health</option>
    <option value="Alternative Health">Alternative Health</option>
    <option value="Fitness & Nutrition">Fitness & Nutrition</option>
    <option value="Self-Help">Self-Help</option>
    <option value="Sexuality">Sexuality</option>
    <option value="Kids & Family">Kids & Family</option>
    <option value="Music">Music</option>
    <option value="News & Pooptiontics">News & Pooptiontics</option>
    <option value="Reoptiongion & Spirituality">Reoptiongion & Spirituality</option>
    <option value="Buddhism">Buddhism</option>
    <option value="Christianity">Christianity</option>
    <option value="Hinduism">Hinduism</option>
    <option value="Islam">Islam</option>
    <option value="Judaism">Judaism</option>
    <option value="Other">Other</option>
    <option value="Spiritualty">Spiritualty</option>
    <option value="Science & Medicine">Science & Medicine</option>
    <option value="Medicine">Medicine</option>
    <option value="Natural Sciences">Natural Sciences</option>
    <option value="Social Sciences">Social Sciences</option>
    <option value="History">History</option>
    <option value="Personal Journals">Personal Journals</option>
    <option value="Philosophy">Philosophy</option>
    <option value="Places & Travel">Places & Travel</option>
    <option value="Sports & Recreation">Sports & Recreation</option>
    <option value="Amateur">Amateur</option>
    <option value="College & High School">College & High School</option>
    <option value="Outdoor">Outdoor</option>
    <option value="Professional">Professional</option>
    <option value="Technology">Technology</option>
    <option value="Gadgets">Gadgets</option>
    <option value="Tech">Tech News</option>
    <option value="Podcasting">Podcasting</option>
    <option value="Software How-To">Software How-To</option>
    <option value="TV & Film">TV & Film</option>
  </select>
        </div>
      </fieldset>
      <div class="item-wrapper">
        <fieldset class="item">
          <legend>Episode info</legend>
          <button class="remove-item">Remove Item</button>
          <div class="field">
            <label for="item-title">Item Title</label>
            <input class="item-title" id="item-title" name="itemTitle" placeholder="Item Title" type="text" data-help-text="Add the title of the episode.<br/> Make your title specific. A podcast entitled 'Our Community Bulletin' is too vague and will attract no subscribers, no matter how compelling the content."/>
          </div>
          <div class="field">
            <label for="item-author">Item Author</label>
            <input class="item-author" id="item-author" name="itemAuthor" placeholder="Item Author" type="text" data-help-text="The content of this tag is shown in the Artist column in iTunes. If the tag is not present, iTunes uses the contents of the 'author' tag. If 'itunes:author' is not present at the feed level, iTunes will use the contents of 'managingEditor'."/>
          </div>
          <div class="field">
            <label for="item-subtitle">Item Subtitle</label>
            <input class="item-subtitle" id="item-subtitle" name="itemSubtitle" placeholder="Item Subtitle" type="text" data-help-text="The contents of this tag are shown in the Description column in iTunes. The subtitle displays best if it is only a few words long."/>
          </div>
          <div class="field">
            <label for="item-summary">Item Summery</label>
            <textarea class="item-summary" id="item-summary" name="itemSummary" placeholder="Item Summery" data-help-text="The contents of this tag are shown in a separate window that appears when the 'circled i' in the Description column is clicked. It also appears on the iTunes page for your podcast. This field can be up to 4000 characters. If 'itunes:summary' is not included, the contents of the 'description' tag are used."></textarea>
          </div>
          <div class="field">
            <label for="item-image-url">Item Image Url</label>
            <input class="item-image-url" id="item-image-url" name="itemImageUrl" placeholder="Item Image Url" type="text" data-help-text="This tag specifies the artwork for your podcast. iTunes prefers square .jpg images that are at least 1400x1400 pixels, which is different from what is specified for the standard RSS image tag. In order for a podcast to be eligible for an iTunes Store feature, the accompanying image must be at least 1400x1400 pixels."/>
          </div>
          <div class="field">
            <label for="item-enclosure-url">Item Url</label>
            <input class="item-enclosure-url" id="item-enclosure-url" name="itemEnclosureUrl" placeholder="Item Url" type="text" data-help-text="Add the URL to the source file of the podcast. The file extension of the URL attribute of this tag is used to determine if an item should appear in the podcast directory. Supported extensions include .m4a, .mp3, .mov, .mp4, .m4v, .pdf, and .epub."/>
          </div>
          <div class="field">
            <label for="item-enclosure-length">Item Mp3 Length</label>
            <input class="item-enclosure-length" id="item-enclosure-length" name="itemEnclosureLength" placeholder="Item Length" type="text" data-help-text="The length attribute is the file size in bytes. Find this information in the file’s properties (on a Mac, choose Get Info from the File menu and refer to the size row)."/>
          </div>
          <div class="field">
            <label for="item-enclosure-type">Item Type</label>
            <select class="item-enclosure-type" id="item-enclosure-type" name="itemEnclosureType" data-help-text="The type element depends upon the type of file the enclosure refers to. Common files and their MIME type extensions are listed in the dropdown">
              <option selected="selected" value="audio/mpeg">audio/mpeg</option>
              <option value="video/mp4">video/mp4</option>
              <option value="audio/x-m4a">audio/x-m4a</option>
              <option value="video/x-m4v">video/x-m4v</option>
              <option value="video/quicktime">video/quicktime</option>
              <option value="application/pdf">application/pdf</option>
              <option value="document/x-epub">document/x-epub</option>
            </select>
          </div>
          <div class="field">
            <label for="item-guid">Item Guid</label>
            <input class="item-guid" id="item-guid" name="itemGuid" placeholder="Item Guid" type="text" data-help-text="Every <item> should have a globally unique identifier (GUID) that never changes. When you add episodes to your feed, GUIDs are compared in case-sensitive fashion to determine which episodes are new. If you omit the GUID for an episode, the episode URL will be used instead."/>
          </div>
          <div class="field">
            <label for="item-pub-date">Item Publication Date</label>
            <input class="item-pub-date" id="item-pub-date" name="itemPubDate" placeholder="Item Publication Date" type="text" data-help-text="This tag specifies the date and time when an episode was released. The format for the content should be per <a href='http://www.faqs.org/rfcs/rfc2822.html' target='_blank'>RFC 2822;</a> e.g.:
<br/>
Wed, 15 Jun 2005 19:00:00 GMT"/>
          </div>
          <div class="field">
            <label for="item-duration">Item Duration</label>
            <input class="item-duration" id="item-duration" name="itemDuration" placeholder="Item Duration" type="text" data-help-text="The content of this tag is shown in the Time column in iTunes.
<br/><br/>
The tag can be formatted HH:MM:SS, H:MM:SS, MM:SS, or M:SS (H = hours, M = minutes, S = seconds)."/>
          </div>
         
        </fieldset>
      </div>
    </form>
  </div>
  <div class="output-wrapper">
    <pre id="output"></pre>
  </div>
</div>


CSS


@import compass

// Work in progress.... This is the start for a helper for a friend
body
  background: #232425
  color: #ffffff
  padding: 80px 0px 0px 0px

  ::selection
    color: #ffffff
    background: rgba(0, 0, 0, 0.4)

  ::-moz-selection
    color: #ffffff
    background: rgba(0, 0, 0, 0.4)
    
.wrapper
  position: relative
  width: 1020px
  height: 650px
  margin: auto

  
/* Header */
.header
  border: 1px solid #333
  box-shadow: 0px 3px 2px 1px rgba(0, 0, 0, 0.5)
  position: fixed
  height: 80px
  width: 100%
  top: 0px
  left: 0px
  padding: 10px 0px
  background: #232425
  z-index: 10
  
  .header-body
    position: relative
    width: 1020px
    margin: auto
  
  .header-helper-output
    position: absolute
    top: 10px
    right: 80px
    color: #ccc
    width: 55%
    height: 70px
    font-size: 12px
    line-height: 18px
  
  a
    color: #fff
      
  h1
    font-family: helvetica
    font-weight: 100
    font-size: 16px
    color: #ccc
    margin-top: 0
  

/* Form styles*/
.form
  width: 400px
  float: left
   
  fieldset
    position: relative
    margin: 30px 0px 
    border: 1px solid #444
    legend
      color: #ccc
    
  label
    width: 140px
    display: inline-block
    color: #ccc
    font-size: 14px
    
  .hide
    height: 0px
    overflow: hidden
    transition: height 1s ease-out
  
  .item:nth-child(1)
    .remove-item
      display: none


  .field
    margin: 10px 0px

input[type="text"], input[type="date"], textarea, button
  border: 1px solid #444
  background: #222
  padding: 6px 8px
  color: #ccc
  width: 200px
  transition: background-color 0.2s ease-out
  font-size: 14px
  &:focus, &:hover
    background: #000

button
  display: inline-block
  width: 140px
  font-size: 12px
  border-radius: 4px
  height: 30px
  padding-top: 4px
  &:active
    padding-top: 5px
  
  
/* XML output */
.output-wrapper
  min-height: 400px
  float: left
  margin-top: 12px
    
  #output
    position: fixed
    padding: 10px 0px 0px 20px
    font-size: 14px
    width: 500px
    height: 400px
    overflow-y: scroll
    overflow-x: hidden
  
/* XML Node styling */
.node
  font-weight: normal
  color: #444 //#8e6e35

.attribute
  color: #fff !important
  
.output-wrapper:hover .node
  color: #8e6e35 
  
  
  
  
  

JS CoffeeScript


class XMLGenerator
  
  data: null
  addToExisting: false
  
  $document: null
  $fields: null
  $select: null
  $channelTemplate: null
  $itemTemplate: null
  $channelInfo: null
  $headerHelperOutput: null
  $output: null
  $addToExisting: null
  $itemsWrapper: null
  $items: null
  $addItem: null
  $removeItem: null
  $pubDate: null
  
  constructor: (@context) ->
    @data = {}
    @$document = $ document
    @$channelTemplate = $ "#channel-info-template"
    @$channelInfo = @context.find ".channel-info"
    @$fields = @context.find "input, textarea, select"
    @$select = @context.find "select"
    @$output = @context.find "#output"
    @$headerHelperOutput = @context.find ".header-helper-output"
    @$addToExisting = @context.find "#add-to-existing"
    @$itemsWrapper = @context.find ".item-wrapper"
    @$items = @context.find ".item"
    @$addItem = @context.find "#add-item"    
    @$selectCode = @context.find "#select-code"
    @$removeItem = @context.find ".remove-item"
    @$pubDate = @context.find ".item-pub-date"
    
    date = new Date()
    @$pubDate.val new Date(date.getTime())
    
    @resize()
      
    @addEventListeners()
    return
  
  addEventListeners: ()=>
    @$addItem.on "click", @onAddItemClick
    @$selectCode.on "click", @onSelectCodeClick
    @$document.on "click", @$removeItem, @onRemoveItemClick
    
    @$document.on "keyup", @$fields, @onKeyUp
    @$document.on "focus", "input, textarea, select", @addHelperText
    @$document.on "blur", "input, textarea, select", @removeHelperText
    #@$fields.on "focus", @addHelperText
    
    @$document.on "change", @$select, @onKeyUp
    @$addToExisting.on "change", @onAddToExistingChange
    
    $(window).on "resize", @onResize
    return

  addHelperText: (event) =>
    $field = $ event.target
    txt = $field.data "help-text"
    @$headerHelperOutput.html txt
    return
  
  removeHelperText: () =>
    @$headerHelperOutput.text ""
    return
  
  resize: () =>
    @$output.css
      height: $(window).height()-130
    return
  
  selectText: (element) =>
    doc = @$document.get(0)
    text = doc.getElementById element
    if doc.body.createTextRange
      range = doc.body.createTextRange()
      range.moveToElementText(text)
      range.select()
    else if window.getSelection
      selection = window.getSelection()
      range = doc.createRange()
      range.selectNodeContents text
      selection.removeAllRanges()
      selection.addRange range
      
    return
  
  
  onResize: (event) =>
    @resize()
    return
  
  onSelectCodeClick: (event) =>
    @selectText "output"
    return
  
  onAddItemClick: (event) =>
    $newItem = @$items.eq(0).clone()
    @$itemsWrapper.append $newItem
    return
  
 
  onRemoveItemClick: (event) =>
    $target = $ event.target
    if $target.hasClass "remove-item"
      $item = $target.closest ".item"
      $item.fadeOut "slow", ()=> $item.remove()
    return
  
  onAddToExistingChange: (event) =>
    if @$addToExisting.is(":checked")
      @addToExisting = true
      @$channelInfo.addClass "hide"
    else
      @addToExisting = false
      @$channelInfo.removeClass "hide"
    return
  
  onKeyUp: (event) =>
    @getData event
    @outputData()
    return
  
  getData: (event) =>
    $field = $ event.target
    val = $field.val()
    name = $field.attr "name"
    @data[name] = val
    
    arr = []
    for item in $(".item")
      $item = $ item
      obj = {}
      
      $input = $item.find(":input").not("button")

      for i in [0..$input.length] by 1
        $field = $ $input[i]
        inputName = $field.attr "name"
        obj[inputName] = $field.val()
      arr.push obj
    @data["items"] = arr
    return

  outputData: () =>
    source = @$channelTemplate.html()
    template = Handlebars.compile source
    umlautsString = @umlauts template(@data)
    xmlString = @htmlEncode umlautsString
    styledString = xmlString.replace(new RegExp("&lt;", 'g'), "<span class='node'>&lt;")
                            .replace(new RegExp("&gt;", 'g'), "&gt;</span>")


    @$output.html styledString
    return
  
  umlauts: (str) =>
    str = str.replace(new RegExp("å", 'g'), "&aring;")
                .replace(new RegExp("ä", 'g'), "&auml;")
                .replace(new RegExp("ö", 'g'), "&ouml;")
                .replace(new RegExp("Å", 'g'), "&Aring")
                .replace(new RegExp("Ä", 'g'), "&Auml;")
                .replace(new RegExp("Ö", 'g'), "&Ouml;")
    return str
  
  htmlEncode: (htmlString) =>
    return $('<div/>').text(htmlString).html()
  
  
generator = new XMLGenerator $ ".wrapper"


--->
