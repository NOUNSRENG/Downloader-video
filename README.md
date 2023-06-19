# Downloader-video
<!DOCTYPE html>
<html>
<head>
    <style>
    
    </style>
  <title> Downloader-web</title>
  <style>
  .btn {
    background-color: yellow;
    color: #fff;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.2s ease-in-out;
  }
  
  .btn:active {
    background-color: green;
  }
  
    form {
        
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    input[type="text"] {
      padding: 10px 100px;
      margin-bottom: 10px;
    }

    button[type="submit"] {
      background-color: green;
      color: white;
      padding: 10px 30px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
  </style>
  <script src="https://cdn.jsdelivr.net/npm/video.js/dist/video.min.js"></script>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/video.js/dist/video-js.min.css">
</head>
<body>
  <form onsubmit="downloadVideo(event)">
    <label for="video-url">Video URL:</label>
    <input type="text" id="video-url" name="video-url">
    
    <label for="video-resolution">Video Resolution:</label>
    <select id="video-resolution" name="video-resolution">
      <option value="720p">720p</option>
      <option value="1080p" selected>1080p</option>
    </select>
    
    <label for="subtitle-language">Subtitle Language:</label>
    <select id="subtitle-language" name="subtitle-language">
      <option value="en" selected>English</option>
      <option value="fr">French</option>
      <option value="km">Cambodia</option>
    </select>
    
    <button type="submit">Download</button>
  </form>

  <div class="video-container">
    <video id="video-player" class="video-js vjs-default-skin vjs-big-play-centered"></video>
  </div>

  <script>
    function downloadVideo(event) {
      event.preventDefault();
  
      var url = document.getElementById("video-url").value;
      var resolution = document.getElementById("video-resolution").value;
      var language = document.getElementById("subtitle-language").value;

      var player = videojs("video-player", {
        sources: [{
          src: url,
          type: "video/mp4"
        }]
      });

      player.addRemoteTextTrack({
        kind: "captions",
        label: language,
        srcLang: language,
        src: "https://example.com/subtitles_" + language + ".vtt"
      });

      var downloadUrl = "https://example.com/download.php?url=" + encodeURIComponent(url) + "&resolution=" + encodeURIComponent(resolution) + "&language=" + encodeURIComponent(language);

      window.location.href = downloadUrl;
    }
  </script>
</body>
</html>

