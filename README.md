---


---

<h1 id="websockets">Websockets</h1>
<p>List of websockets avalailable on <strong>Inobi</strong> platform server</p>
<h2 id="driver">Driver</h2>
<p><em>Path: /ws/taxi/driver/</em><br>
Socket for driver to stay in contact with server. Messages will be sent to driver when:</p>
<pre><code>- here is a trip for a driver to accept
- ...
</code></pre>
<h4 id="example">Example</h4>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> scheme <span class="token operator">=</span> <span class="token string">'ws://'</span>
<span class="token keyword">const</span> host <span class="token operator">=</span> <span class="token string">'dev.inobi.kg:12000'</span>
<span class="token keyword">const</span> path <span class="token operator">=</span> <span class="token string">'/ws/taxi/drivers/'</span>
<span class="token keyword">const</span> token <span class="token operator">=</span> <span class="token string">'1572d957-19e3-4a07-8519-3b04ca5c0b56'</span>
<span class="token keyword">const</span> socket <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">WebSocket</span><span class="token punctuation">(</span><span class="token template-string"><span class="token string">`</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>scheme<span class="token interpolation-punctuation punctuation">}</span></span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>host<span class="token interpolation-punctuation punctuation">}</span></span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>path<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">?token=</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>token<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">`</span></span><span class="token punctuation">)</span>
socket<span class="token punctuation">.</span>onclose <span class="token operator">=</span> socket<span class="token punctuation">.</span>onerror<span class="token operator">=</span> console<span class="token punctuation">.</span>log
socket<span class="token punctuation">.</span><span class="token function-variable function">onmessage</span> <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span>e<span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">const</span> data <span class="token operator">=</span> JSON<span class="token punctuation">.</span><span class="token function">parse</span><span class="token punctuation">(</span>e<span class="token punctuation">.</span>data<span class="token punctuation">)</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span>
	<span class="token keyword">if</span> <span class="token punctuation">(</span>data<span class="token punctuation">.</span>type <span class="token operator">==</span> <span class="token string">'TRIP'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">const</span> <span class="token punctuation">{</span> payload<span class="token punctuation">:</span> trip <span class="token punctuation">}</span> <span class="token operator">=</span> data<span class="token punctuation">;</span>
		<span class="token function">alert</span><span class="token punctuation">(</span><span class="token string">'trip to accept'</span><span class="token punctuation">,</span> trip<span class="token punctuation">.</span>name<span class="token punctuation">)</span><span class="token punctuation">;</span>
		console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>trip<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="trip">Trip</h2>
<p><em>Path: /ws/taxi/trips/{trip_id}/</em><br>
Socket for getting trip messages. Messages will be sent to user/driver/manager on every trip related event. Some of them are followings:</p>
<pre><code>- trip accepted
- driver arrived
- driver started
- driver sent his coordinate
- user notified driver he's coming
- driver paused/resumed trip
- trip finished
- etc
</code></pre>
<h4 id="example-1">Example</h4>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> scheme <span class="token operator">=</span> <span class="token string">'ws://'</span>
<span class="token keyword">const</span> host <span class="token operator">=</span> <span class="token string">'dev.inobi.kg:12000'</span>
<span class="token keyword">const</span> tripId <span class="token operator">=</span> <span class="token number">1</span>
<span class="token keyword">const</span> path <span class="token operator">=</span> <span class="token template-string"><span class="token string">`/ws/taxi/trips/</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>tripId<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">/`</span></span>
<span class="token keyword">const</span> token <span class="token operator">=</span> <span class="token string">'1572d957-19e3-4a07-8519-3b04ca5c0b56'</span>
<span class="token keyword">const</span> socket <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">WebSocket</span><span class="token punctuation">(</span><span class="token template-string"><span class="token string">`</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>scheme<span class="token interpolation-punctuation punctuation">}</span></span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>host<span class="token interpolation-punctuation punctuation">}</span></span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>path<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">?token=</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>token<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">`</span></span><span class="token punctuation">)</span>
socket<span class="token punctuation">.</span>onclose <span class="token operator">=</span> socket<span class="token punctuation">.</span>onerror<span class="token operator">=</span> console<span class="token punctuation">.</span>log
socket<span class="token punctuation">.</span><span class="token function-variable function">onmessage</span> <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span>e<span class="token punctuation">)</span> <span class="token punctuation">{</span>
	<span class="token keyword">const</span> data <span class="token operator">=</span> JSON<span class="token punctuation">.</span><span class="token function">parse</span><span class="token punctuation">(</span>e<span class="token punctuation">.</span>data<span class="token punctuation">)</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span>
	<span class="token keyword">if</span> <span class="token punctuation">(</span>data<span class="token punctuation">.</span>type <span class="token operator">==</span> <span class="token string">'ARRIVE'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">const</span> <span class="token punctuation">{</span> payload<span class="token punctuation">:</span> tripState <span class="token punctuation">}</span> <span class="token operator">=</span> data<span class="token punctuation">;</span>
		<span class="token function">alert</span><span class="token punctuation">(</span><span class="token string">'driver arrived'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
		console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>tripState<span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>

