<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <!--Import Google Icon Font-->
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <!--Import materialize.css-->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0-beta/css/materialize.min.css">

    <!--Let browser know website is optimized for mobile-->
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  </head>

  <body class="red darken-3 white-text">
    <div class="container">
      
      <h1><img style="width: 20%; margin-right: 20px; vertical-align: middle;" src="icon.png" alt="">警告</h1>
      <h4>あなたの<span id="device"></span>からウイルスが発見されました</h4>
      <p class="flow-text">このままではスマートフォンが発火もしくは破裂する可能性があります。</p>
      <p class="flow-text"><span id="timer" style="font-size: 2em;"></span>秒以内に以下のリンクから対処してください。</p>
      <a href="http://amzn.asia/5mDSMdf" class="btn btn-laege">ウイルスを除去する</a>
    </div>
    <div id="alert" class="modal">
      <div class="modal-content black-text">
        <h4>警告</h4>
        <p>お使いの端末はウイスルからウイルスが発見されました。次のページからウイルスを除去してください。</p>
      </div>
      <div class="modal-footer">
        <button id="close" class="btn btn-laege">OK</button>
      </div>
    </div>
    <!--JavaScript at end of body for optimized loading-->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0-beta/js/materialize.min.js"></script>
    <script>
      function play_se(){
        // SEとバイブレーションの制御
        var voice = new Audio('voice.mp3');
        var warning = new Audio('warning.mp3');
        warning.play();
        voice.play();
        navigator.vibrate([200, 100, 200, 100, 200, 100, 200]);
      }


      $(function(){
        // ブラウザバック禁止
        history.pushState(null, null, null);
        $(window).on("popstate", function(e){
          if (!e.originalEvent.state){
            play_se();
            history.pushState(null, null, null);
            return;
          }
        });

        // モーダル初期化
        $('.modal').modal({dismissible: false});
        $('#alert').modal('open');
        $('#close').click(function(){
          $('#alert').modal('close');
          play_se();
        });

        var device = navigator.userAgent.match(/Android|iPhone|iPad/);
        if (device == null){
          device = '端末';
        }
        $('#device').text(device);

        var time = 300;
        setInterval(function(){
          time--;
          $('#timer').text(time);
        }, 1000);
      });
    </script>
  </body>
</html>
