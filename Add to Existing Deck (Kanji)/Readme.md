# Add writing component to existing deck

Features
- Support Kanji and Kana
- Night mode
- Character and grid height
- Show and hide outline
- Show stroke with animation

# Add to existing deck with Kanji

1. Download zip files which contains necessary files<br>
[Download - Add Kanji writer v3.0](https://raw.githubusercontent.com/smileytechie/Write-Kanji/master/Add%20to%20Existing%20Deck%20(Kanji)/Add.Kanji.writer.to.existing.deck.version.3.0.zip)<br>
<br>
[Download - Character stroke data](https://raw.githubusercontent.com/smileytechie/Write-Kanji/master/Add%20to%20Existing%20Deck%20(Kanji)/Character%20stroke%20data.zip)

2. Extract zip file and copy all files to `Anki/User 1/collection.media` folder. Anki does not support subfolders in the collections.media folder, so make sure you put the character stroke data files directly in the collections.media folder.

3. Open card template editor or note editor for current deck and add the following to back or front side of card template.

**Note:** 1. Change `{{Expression}}` to fields in your Anki Kanji decks<br>
      2. **To hide the add this to the div of Expression**, `style="display:none;"`<br>
      `<div id='ch_kanji' class="text-color4" style="display:hidden">{{Expression}}</div>`

```html
<div id='ch_kanji' class="text-color4">{{Expression}}</div>
<div id="character-target-div"></div>
<div id="bottom-Button"></div>

<script src="{{Expression}}.js" type="text/javascript"></script>

<script>
    var data = JSON.stringify(char_data); // character stroke data from the .js loaded above
    var show_outline = true;     // default show outline, put false for hiding
    var charHW = 70;             // default grid size on screen on scale of 0-100
    var strokeWidth = 10;        // default brush size
</script>


<script>
    // https://forums.ankiweb.net/t/linking-to-external-javascript/1713/4
    var injectScript = (src) => {
        return new Promise((resolve, reject) => {
            const script = document.createElement('script');
            script.src = src;
            script.async = true;
            script.onload = resolve;
            script.onerror = reject;
            document.head.appendChild(script);
        });
    };

    (async () => {
        if (typeof keyman === 'undefined') {
            await injectScript('_hanzi_writer_xiehanzi_kanji.js');
        }
    })();
</script>
```

4. Add following to Styling of card template.
```css
@import "_hanzi_writer_style.css";
```

