---
layout: post
title: Where's the Glue?
tags:
- Geek
- Personal
status: publish
type: post
published: true
meta: {}
---
Perhaps I'm out of the loop on this one, but I've found an odd gap between edge Rails and the simply_restful plugin.  Here's what's up:

<b>The Controller</b>
<pre><code>
ShoesController &lt; ApplicationController
  ...
  def show
    @shoe = Shoe.find @params[:id]
  end
  ...
end
</code></pre>
<b>The Views</b>
<pre><code>
app/shoes/show.rhtml
         /show.rxml
         /show.rjs
</code></pre>
<b>My Expectation</b>

When I <code>GET /shoes/1.xml</code> I get the XML format via the <code>show.rxml</code> file, and when I <code>GET /shoes/1.html</code> I get the HTML format via the <code>show.rhtml</code> file -- afterall, the format is specified in the request, and passed through as <code>@params[:format]</code>.

Unfortunately, I don't have deep knowledge of the internal Rails code (yet!), so I kludged together a quick workaround that automatically determines format-based views.

<b>The Workaround</b>
<pre><code>
def render_formatted
  @params[:format] ||= "html"  # Default format
  # build the preferred template path
  template = "#{RAILS_ROOT}/app/views/#{@params[:controller]}/#{@params[:action]}.r#{@params[:format]}"
  if File.exist? template
    render :file =&gt; template
  else
    render :text =&gt; "'#{@params[:format]}' format not available for '#{@request.path}'", :status =&gt; 404
  end
end
</code></pre>
In practice, <code>#render_formatted</code> would be called at the end of any given action to provide the appropriate response.  Know a better way to do this?  Any feedback would be appreciated, especially if I'm missing a vital link in the clue train ...

Thanks!
