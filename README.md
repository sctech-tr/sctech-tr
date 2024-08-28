### visitor counter!
![Visitor Count](https://profile-counter.glitch.me/sctech-tr/count.svg)

[![wakatime](https://wakatime.com/badge/user/7dfbf33e-5d18-47f8-a436-063b5f5bece2.svg)](https://wakatime.com/@7dfbf33e-5d18-47f8-a436-063b5f5bece2)

<table><tbody><tr><td><a href="https://octo-ring.com/"><img src="https://octo-ring.com/static/img/widget/top.png" width="99%" alt="Octo Ring logo" align="top"></a><br><a href="https://octo-ring.com/p/sctech-tr/prev"><img src="https://octo-ring.com/static/img/widget/prev.png" width="33%" alt="previous" align="top" title="previous profile"></a><a href="https://octo-ring.com/p/sctech-tr/random"><img src="https://octo-ring.com/static/img/widget/random.png" width="33%" alt="random" align="top" title="random profile"></a><a href="https://octo-ring.com/p/sctech-tr/next"><img src="https://octo-ring.com/static/img/widget/next.png" width="33%" alt="next" align="top" title="next profile"></a><br><a href="https://octo-ring.com/"><img src="https://octo-ring.com/static/img/widget/bottom.png" width="99%" alt="check out other GitHub profiles in the Octo Ring" align="top"></a></td></tr></tbody></table>

<img src="https://github-profile-trophy.vercel.app/?username=sctech-tr&theme=discord&no-bg=false" />

![Jokes Card](https://readme-jokes.vercel.app/api?theme=synthwave&borderColor=white)

<table
  id="player"
  style="
    background-color: #111;
    color: #fff;
    font-family: Helvetica, Arial;
    font-size: 5vmin;
    border-radius: 10px;
    filter: opacity(0.8);
    width: 100%;
    height: 100%;
  "
>
  <tr height="100%">
    <td width="20%" align="center">
      <img
        id="player-album-art"
        style="margin: 1em; max-height: 50vmin; border-radius: 10px"
      />
    </td>
    <td width="80%">
      <div style="margin: 1em 1em 1em 0">
        <div id="player-song" style="font-size: 2em"></div>
        <div
          id="player-artist"
          style="font-size: 1.3em; margin-bottom: 1em"
        ></div>
        <a
          id="player-song-link"
          href=""
          target="_blank"
          style="
            color: #fff;
            text-decoration: none;
            border: 1px solid #fff;
            border-radius: 10px;
            padding: 0.2em;
            margin-right: 0.2em;
          "
        >
          🎵 Song
        </a>
        <a
          id="player-artist-link"
          href=""
          target="_blank"
          style="
            color: #fff;
            text-decoration: none;
            border: 1px solid #fff;
            border-radius: 10px;
            padding: 0.2em;
            margin-right: 0.2em;
          "
        >
          🧑‍🎤 Artist</a
        >
        <a
          id="player-album-link"
          href=""
          target="_blank"
          style="
            color: #fff;
            text-decoration: none;
            border: 1px solid #fff;
            border-radius: 10px;
            padding: 0.2em;
            margin-right: 0.2em;
          "
        >
          💽 Album</a
        >
        <a
          id="player-mp3-link"
          href=""
          target="_blank"
          style="
            color: #fff;
            text-decoration: none;
            border: 1px solid #fff;
            border-radius: 10px;
            padding: 0.2em;
            margin-right: 0.2em;
          "
        >
          📻 MP3</a
        >
        <div id="player-status" style="margin: 2em 0 1em 0"></div>
        <div
          id="player-time"
          style="position: relative; float: right; top: -2em; font-weight: bold"
        ></div>
        <div
          id="player-progress-back"
          style="border: 0.15em solid #eee; height: 1em; border-radius: 10px"
        >
          <div
            id="player-progress"
            style="
              background-color: #eee;
              border: 0.1em solid transparent;
              height: 0.75em;
              border-radius: 10px;
              transition: width 0.2s;
            "
          ></div>
        </div>
        <div style="float: right; font-size: 0.9em">
          👾
          <a
            href="https://github.com/Naushikha/Spotify-Widget"
            target="_blank"
            style="color: white"
            >Spotify-Widget</a
          >
          by
          <a href="https://naushikha.com" target="_blank" style="color: white">Naushikha</a> 💀
        </div>
      </div>
    </td>
  </tr>
  <div
    id="player-background"
    class="background"
    style="
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      z-index: -10;
      background-position: center center;
      background-size: 100%;
      filter: blur(2em);
      position: absolute;
      transition: background-image 0.5s ease-in;
    "
  ></div>
</table>

<script>
  var serviceHost = "https://spotify-widget.gamerselimiko.workers.dev";
  var spotifyUser = "sctech-tr";

  var songData, progressSeconds, totalSeconds, progressInterval;

  function updatePlayer() {
    fetch(`${serviceHost}/get-now-playing`)
      .then((response) => response.json())
      .then((data) => {
        if (data.hasOwnProperty("ERROR")) {
          document.getElementById(
            "player-song"
          ).innerHTML = `${spotifyUser} isn't playing anything.`;
          document.getElementById("player-artist").innerHTML = "  ";
          return;
        }
        songData = data;
        document.getElementById("player-song").innerHTML = data.item.name;
        document.getElementById("player-artist").innerHTML =
          data.item.artists[0].name;
        document.getElementById("player-status").innerHTML = data.is_playing
          ? `▶️ ${spotifyUser}'s now playing...`
          : `⏸ ${spotifyUser} has paused.`;
        document
          .getElementById("player-album-art")
          .setAttribute("src", data.item.album.images[1].url);
        document
          .getElementById("player-progress")
          .setAttribute(
            "style",
            document.getElementById("player-progress").getAttribute("style") +
              `width: ${(data.progress_ms * 100) / data.item.duration_ms}%`
          );

        document.getElementById(
          "player-background"
        ).style.backgroundImage = `url(${data.item.album.images[1].url})`;

        // Set the links to spotify stuff
        document
          .getElementById("player-song-link")
          .setAttribute("href", data.item.external_urls.spotify);
        document
          .getElementById("player-artist-link")
          .setAttribute("href", data.item.artists[0].external_urls.spotify);
        document
          .getElementById("player-album-link")
          .setAttribute("href", data.item.album.external_urls.spotify);
        document
          .getElementById("player-mp3-link")
          .setAttribute("href", data.item.preview_url);

        // Hide mp3 link if the song does not provide that
        if (data.item.preview_url == null) {
          document
            .getElementById("player-mp3-link")
            .setAttribute("style", "display: none;");
        }

        // Timer to show updates on progress bar and time
        // https://stackoverflow.com/questions/5517597/plain-count-up-timer-in-javascript
        progressSeconds = Math.ceil(songData.progress_ms / 1000);
        totalSeconds = Math.ceil(songData.item.duration_ms / 1000);
        // Process progress only if a song is in 'playing' state
        if (songData.is_playing) {
          progressInterval = setInterval(setProgress, 1000);
        } else {
          setProgress();
        }

        // Hide all the extra things in mobile (<410px)
        if (document.getElementById("player").clientWidth < 410) {
          // Hide links
          document.getElementById("player-song-link").style.display = "none";
          document.getElementById("player-artist-link").style.display = "none";
          document.getElementById("player-album-link").style.display = "none";
          document.getElementById("player-mp3-link").style.display = "none";

          // Hide duration
          document.getElementById("player-time").style.display = "none";
        }
      });
  }

  function setProgress() {
    if (progressSeconds > totalSeconds) {
      clearInterval(progressInterval);
      updatePlayer();
      return;
    }
    ++progressSeconds;
    var totalLabel =
      pad(parseInt(totalSeconds / 60)) + ":" + pad(totalSeconds % 60);
    var progressLabel =
      pad(parseInt(progressSeconds / 60)) + ":" + pad(progressSeconds % 60);
    document.getElementById("player-time").innerHTML =
      progressLabel + " / " + totalLabel;
    document.getElementById("player-progress").style.width = `${
      (progressSeconds * 100) / totalSeconds
    }%`;
  }

  function pad(val) {
    var valString = val + "";
    if (valString.length < 2) {
      return "0" + valString;
    } else {
      return valString;
    }
  }

  // Load player for the first time
  updatePlayer();
</script>

![Metrics](/github-metrics.svg)
