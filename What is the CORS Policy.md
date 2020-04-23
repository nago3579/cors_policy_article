---


---

<h1 id="what-is-the-cors-policy">What is the CORS Policy</h1>
<p>The CORS policy or the Cross-Origin Resource Sharing policy prevents acessing web resources from sources other than the server the website is running on for security purposes.</p>
<h3 id="accessing-assets">Accessing Assets</h3>
<p>For most websites, all of the assets (images, text, files, etc.) they use are held on the same server the website is hosted on. Since a website should be trusted by the server hosting it, the site is given permission to use resources held by the host server. This is called the same-origin policy, as both the website and the assets share the same origin, namely the server they are hosted on.</p>
<h3 id="assets-on-another-server">Assets on Another Server</h3>
<p>Imagine you wanted a website to make a call to another server with information on it. This can be done easily with the <code>fetch()</code> JavaScript function.</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token comment">// gets the text written by the server and prints it in the console</span>
<span class="token function">fetch</span><span class="token punctuation">(</span><span class="token string">"url_of_server"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span>req <span class="token operator">=&gt;</span> req<span class="token punctuation">.</span><span class="token function">text</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span>console<span class="token punctuation">.</span>log<span class="token punctuation">)</span>
</code></pre>
<p>With the above GET request, we can access the information stored on the servers we target.</p>
<h3 id="why-cors-is-important">Why CORS Is Important</h3>
<p>Now that we can get arbitrary data from another server with a GET request, we can just as easily change or modify that data on the server by sending DELETE, POST, or UPDATE requests.</p>
<p>The server needs a way to make sure malicious websites can’t seal or damage protected information, while still allowing access to approved sites.</p>
<h3 id="simulating-cors">Simulating CORS</h3>
<p>We can see how this works by making a simple webserver.  Try running this Node.js server with <a href="https://repl.it/@NadivGold/cors1">this repl.it link</a>.</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token comment">//This is the template Node.js code provided by repl.it</span>
<span class="token keyword">var</span> http <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'http'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">//create a server object:</span>
http<span class="token punctuation">.</span><span class="token function">createServer</span><span class="token punctuation">(</span><span class="token keyword">function</span>  <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span>  <span class="token punctuation">{</span>
	res<span class="token punctuation">.</span><span class="token function">write</span><span class="token punctuation">(</span><span class="token string">'Section is cool'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  <span class="token comment">//write a response to the client</span>
	res<span class="token punctuation">.</span><span class="token function">end</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  <span class="token comment">//end the response</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">listen</span><span class="token punctuation">(</span><span class="token number">6003</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  <span class="token comment">//the server object listens on port 6003</span>
</code></pre>
<p>If you have Node.js, I recommend running this code locally.</p>
<p>To test the webserver, open the browser’s <a href="https://support.monday.com/hc/en-us/articles/360002197259-How-to-Open-the-Developer-Console-in-your-Browser">console</a> on this website, and enter:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token string">"https://cors1--nadivgold.repl.co/"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span>req<span class="token operator">=&gt;</span> req<span class="token punctuation">.</span><span class="token function">text</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span>console<span class="token punctuation">.</span>log<span class="token punctuation">)</span>
</code></pre>
<p>If you’re using the Node.js local version, use:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token string">"localhost:6003"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span>req <span class="token operator">=&gt;</span> req<span class="token punctuation">.</span><span class="token function">text</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span>console<span class="token punctuation">.</span>log<span class="token punctuation">)</span>
</code></pre>
<p>Running this <code>fetch()</code> command in the console acts as if the website was sending the request.</p>
<p>You should see a CORS error in your console, looking something like:</p>
<pre><code>Access to fetch at 'https://cors1--nadivgold.repl.co/' from origin '**editor's note, please put the url of this article inside these single quotation marks**' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
</code></pre>
<p>The asset we tried to request was the string “Section is cool” from the Node.js web server. Our request was blocked because the server did not explicitly give our website permission.</p>
<p>To fix this issue, we can add the ‘Access-Control-Allow-Origin’ to our web server. This HTML header lets CORS know that we are okay with letting others request the asset. Just add</p>
<pre class=" language-javascript"><code class="prism  language-javascript">res<span class="token punctuation">.</span><span class="token function">setHeader</span><span class="token punctuation">(</span><span class="token string">"Access-Control-Allow-Origin"</span><span class="token punctuation">,</span>  <span class="token string">"*"</span><span class="token punctuation">)</span>  <span class="token comment">//sets the allow use to all requests html header</span>
</code></pre>
<p>to the Node.js server before the write, or use this <a href="https://repl.it/@NadivGold/cors2">new replit link</a>.</p>
<p>The star symbol in the second argument denotes that all requests are accepted. If we just wanted to give access to one site, replace the star with the url of that site.</p>
<p>We can now run the same fetch request as above to access our string.</p>
<p>If you’re using the replit version, use this fetch instead:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token function">fetch</span><span class="token punctuation">(</span><span class="token string">"https://cors2--nadivgold.repl.co/"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span>req <span class="token operator">=&gt;</span> req<span class="token punctuation">.</span><span class="token function">text</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span>console<span class="token punctuation">.</span>log<span class="token punctuation">)</span>
</code></pre>
<p>We should now see <code>Section is cool</code> in the console.</p>
<h3 id="wrap-up">Wrap Up</h3>
<p>The most important thing to remember when dealing with CORS is to drink responsibly.<br>
The second most important thing is to remember is that, if you need something from another server, you also need permission.</p>

