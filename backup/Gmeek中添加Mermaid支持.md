原生github的issue预览是支持Mermaid图表显示的
但是发布文章后,Mermaid图表在文章里却是显示为了代码

在config.json中添加下面代码
就可以让Mermaid代码以预期的效果还原了

https://pigrass.github.io/post/12.html 这是我用Gmeek发布博文后,仍然保留Mermaid图表效果的案例



```code
<script>(function(){var` KW=['graph','flowchart','sequenceDiagram','classDiagram','stateDiagram','erDiagram','gantt','pie','journey','gitGraph','mindmap','timeline','quadrantChart','sankey','xychart','block','packet','architecture','info','zenuml','requirementDiagram','c4Context','%%'];var CDS=['','https://unpkg.com/mermaid@11/dist/mermaid.min.js'];var DBG={found:0,rendered:0,src:'',error:''};window.__gmeekMermaid=DBG;var BOXES=[];function looks(t){t=(t||'').trim();for(var i=0;i<KW.length;i++){if(t.indexOf(KW[i])===0)return true}return false}function collect(){var seen=[],out=[];function add(p,trusted){if(!p||seen.indexOf(p)>=0)return;if(p.hasAttribute&&p.hasAttribute('data-processed'))return;if(p.querySelector&&p.querySelector('svg'))return;if(!trusted&&!looks(p.textContent||''))return;seen.push(p);out.push(p)}var q=document.querySelectorAll('div[class*=highlight-source-mermaid] pre,pre[lang=mermaid],pre[data-lang=mermaid],pre>code[class*=mermaid],div[class*=mermaid]>pre');for(var i=0;i<q.length;i++){var n=q[i];add(n.tagName==='PRE'?n:n.closest('pre'),true)}var all=document.querySelectorAll('pre');for(var j=0;j<all.length;j++){add(all[j],false)}return out}function convert(list){return list.map(function(p){var txt=(p.querySelector('code')||p).textContent;var b=document.createElement('pre');b.className='mermaid';b.textContent=txt;var h=p.parentNode;if(h&&h.classList&&(h.classList.contains('highlight')||h.classList.contains('highlight-source-mermaid'))){h.replaceWith(b)}else{p.replaceWith(b)}return b})}function render(){if(!window.mermaid){DBG.error='引擎未就绪';console.error('[Gmeek Mermaid] 引擎未就绪',DBG);return}try{window.mermaid.initialize({startOnLoad:false,theme:'default'});var r=window.mermaid.run({nodes:BOXES});if(r&&r.then){r.then(function(){DBG.rendered=BOXES.length;console.log('[Gmeek Mermaid] 渲染完成',DBG)},function(e){DBG.error=String(e);console.error('[Gmeek Mermaid] 渲染失败',e)})}else{DBG.rendered=BOXES.length;console.log('[Gmeek Mermaid] 渲染完成',DBG)}}catch(e){DBG.error=String(e);console.error('[Gmeek Mermaid] 渲染异常',e)}}function load(i){if(i>=CDS.length){DBG.error='所有 CDN 均加载失败';console.error('[Gmeek Mermaid]',DBG.error,DBG);return}var s=document.createElement('script');s.src=CDS[i];DBG.src=CDS[i];s.onload=render;s.onerror=function(){load(i+1)};(document.head||document.documentElement).appendChild(s)}function go(){var list=collect();DBG.found=list.length;console.log('[Gmeek Mermaid] 命中代码块',list.length);if(!list.length){DBG.error='未找到 mermaid 代码块';console.warn('[Gmeek Mermaid]',DBG.error,DBG);return}BOXES=convert(list);if(window.mermaid){render()}else{load(0)}}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',go)}else{go()}})();</script>
```

mermaid.min.js目前是走了cdn的,
AI建议也可以考虑把 mermaid.min.js 下载下来放进仓库 docs/static/，然后把片段里的 CDS 数组改成自己的地址，比如 ['https://你的域名/static/mermaid.min.js']。这样完全不依赖外网。

[mermaid.min.js](https://github.com/user-attachments/files/34849018/mermaid.min.js)