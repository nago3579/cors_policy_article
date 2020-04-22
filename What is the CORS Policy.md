---


---

<h1 id="what-is-the-cors-policy">What is the CORS Policy</h1>
<p>The CORS policy or the Cross-Origin Resource Sharing policy prevents some web resources from sources other than the current server the website is running on for security purposes.</p>
<h3 id="blocked-by-cors">Blocked by CORS</h3>
<p>Imagine you wanted a website with images on it, but that image is hosted on a different server. This can be done easily with an HTML image tag.</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>https://www.section.io/assets/images/education/authors/nadiv-gold-edelstein.jpg<span class="token punctuation">"</span></span>  
<span class="token attr-name">alt</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>the image at the bottom of the article<span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>With the src attribute, we can access the picture stored on <a href="http://Section.io">Section.io</a>’s servers and embed it on our website.<br>
<strong>We now have an issue.</strong> What happens when <a href="http://Section.io">Section.io</a> (or a hacker that has access to <a href="http://Section.io">Section.io</a>’s server) changes the stored picture, or removes it? Fortunately for us, images are very safe, and the worst that could happen is the image showing up as something else or broken.</p>
<p>Now imagine we added JavaScript from another server. If that server gets</p>

