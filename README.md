# ihmisiishaku

Episode data has been scraped with the following code which outputs the current video description timestamps, and clicks to the next video in the playlist:

```
(async () => { document.querySelector('#expand').click(); await new Promise(r=>setTimeout(r,1000)); var found = []; document.querySelector('#description-inline-expander > yt-attributed-string > span').childNodes.forEach((n)=>{ var t = (n.innerText || n.textContent)+""; t = t.replace(/^\s*/,'').replace(/\n.*/g,''); if (!found.length && ! t.match(/00\:0.\:../)) return; if (t.match(/..\:..\:../) ) { found.push({"time":t,"href":n.querySelector("a").href.replace(/\&(list|index)\=[^\&]*/g,'')}) } else if (! found[found.length-1]["text"] ) { found[found.length-1]["text"] = t; } }); console.log("episodes.push("+JSON.stringify({title:document.querySelector("#title > h1 > yt-formatted-string").innerText,bookmarks:found})+");"); document.querySelector('#movie_player > div.ytp-chrome-bottom > div.ytp-chrome-controls > div.ytp-left-controls > a.ytp-next-button.ytp-button').click(); })()
```

This prints the data to the console in a form in which it can just be copied to the script in the index file.

Otherwise the beef of the repo is just the static index file which can either be served through github pages or copied elsewhere.
