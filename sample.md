Markdownサンプル
================

コード
------

```html:index.html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <meta name="robots" content="none">
    <title>MARKED</title>
    <meta http-equiv="Content-Style-Type" content="text/css" />
    <meta http-equiv="Content-Script-Type" content="text/javascript" />
    <!-- CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@11.5.1/build/styles/github.min.css">
    <!-- JS -->
    <script src="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@11.5.1/build/highlight.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.6.0/dist/jquery.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/mermaid@9.1.1/dist/mermaid.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/marked@4.0.16/marked.min.js"></script>
    <script>mermaid.initialize({startOnLoad:false});</script>
  </head>

  <body id="content">
    <script>
      //Markedのレンダリング設定
      //参考  https://mermaid-js.github.io/mermaid/#/usage?id=example-of-a-marked-renderer
      var renderer = new marked.Renderer();
      renderer.code = function (code, language) {
        if (language == 'mermaid') {
          //mermaid.js処理対象設定
          return '<div class="mermaid">' + code + '\n</div>';
        } else {
          //hilight.js処理
          return '<pre><code>\n' + hljs.highlightAuto(code).value + '\n</code></pre>';
        }
      }
      marked.use({ renderer });

      //Markdownファイル読み込み
      $(document).ready(function(){
        if (location.href.split("#").length > 1) {
          var urlParam = location.href.split("#")[1];
          $.get( urlParam, function( data ) {
            //marked.js処理
            $('#content').html(marked.parse(data));
            //mermaid.js処理
            mermaid.init();
          });
        } else {
          $('#content').html('please url#any.md');
        }
      });
    </script>
  </body>
</html>
```

グラフ
------

### flowchart#1

```mermaid
flowchart LR
  A[起床] --> B[朝食]
  B --> C[作業]
  C --> D[昼食]
  D --> E[作業]
  E --> F[夕飯]
  F --> G[就寝]
  G --> A
```

### flowchart#2

```mermaid
flowchart LR
  DataStore[|borders:tb|Database] -->|input| Process((System)) -->|output| Entity[Customer];
```

### flowchart#3

```mermaid
flowchart TD
  allSides[ stroke all sides ];
  allSides2[|borders:ltrb| stroke all sides ];
  rbSides[|borders:rb| stroke right and bottom sides ];
  ltSides[|borders:lt| stroke left and top sides ];
  lrSides[|borders:lr| stroke left and right sides ];
  noSide[|borders:no| stroke no side ];
```

### sequenceDiagram

```mermaid
sequenceDiagram
  title: FancySequenceDiagram
  participant Alice
  participant Bob
  participant John as John<br />Second Line
  autonumber 10 10
  rect rgb(200, 220, 100)
    rect rgb(200, 255, 200)
      Alice ->> Bob: Hello Bob, how are you?
      Bob-->>John: How about you John?
    end
    Bob--x Alice: I am good thanks!
    Bob-x John: I am good thanks!
    Note right of John: John thinks a long<br />long time, so long<br />that the text does<br />not fit on a row.
    Bob-->Alice: Checking with John...
    Note over John:wrap: John looks like he's still thinking, so Bob prods him a bit.
    Bob-x John: Hey John - we're still waiting to know<br />how you're doing
    Note over John:nowrap: John's trying hard not to break his train of thought.
    Bob-x John:wrap: John! Are you still debating about how you're doing? How long does it take??
    Note over John: After a few more moments, John<br />finally snaps out of it.
  end
  autonumber off
  alt either this
    Alice->>+John: Yes
    John-->>-Alice: OK
  else or this
    autonumber
    Alice->>John: No
  else or this will happen
    Alice->John: Maybe
  end
  autonumber 200
  par this happens in parallel
    Alice -->> Bob: Parallel message 1
  and
    Alice -->> John: Parallel message 2
  end
```

### gantt

```mermaid
gantt
  accTitle: A Gantt Diagram
  accDescr: Remaining Q4 Tasks
  dateFormat  YYYY-MM-DD
  section Section
  A task           :a1, 2014-01-01, 30d
  Another task     :after a1  , 20d
  section Another
  Task in sec      :2014-01-12  , 12d
  another task      : 24d
```

### journey

```mermaid
journey
  accTitle: My day
  accDescr: A user journey diagram of a typical day in my life
  section Go to work
    Make tea: 5: Me
    Go upstairs: 3: Me
    Do work: 1: Me, Cat
  section Go home
    Go downstairs: 5: Me
    Sit down: 5: Me
```
