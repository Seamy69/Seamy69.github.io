
<html>
<head>

<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width,initial-scale=0.3">


<link rel="stylesheet" href="./KatKrewBot\CSS\default.css">
<link rel="stylesheet" href="./KatKrewBot\CSS\rest.css" media="screen, projection">

<style>
	.tabs a.make-kinda-visible {
		color: #fff;
		background-color: #1e2125;
	}

	.tabs a.make-kinda-visible:hover {
		color: #eee;
	}

	.tabs a.make-kinda-visible.active {
		background-color: #111315;
	}
</style>

<script>
    function toggleTable(table,e) {
	
	var lMenu = document.getElementById(e);
	document.getElementById("MENU1").className = "make-kinda-visible";
	document.getElementById("MENU2").className = "make-kinda-visible";
	document.getElementById("MENU3").className = "make-kinda-visible";
	
	lMenu.className = "make-kinda-visible active";
	
    var lTable = document.getElementById(table);
	document.getElementById("CMD_EVERYONE").style.display = "none";
	document.getElementById("CMD_COMMANDER").style.display = "none";
	document.getElementById("CMD_ADMIN").style.display = "none";
	
    lTable.style.display = (lTable.style.display == "inline-block") ? "none" : "inline-block";
	}
</script>
   
</head>

<body>

<div class="row">
<div class="col s8 offset-s2">
<div class="card col-s12">
<div class="col s12">

<ul class="tabs" style="width: 100%;">
	<li class="tab col s3"><a id="MENU1" class="make-kinda-visible active" onclick="toggleTable('CMD_EVERYONE',id);">Everyone</a></li>
	<li class="tab col s3"><a id="MENU2" class="make-kinda-visible" onclick="toggleTable('CMD_COMMANDER', id);">Bot Commander</a></li>
	<li class="tab col s3"><a id="MENU3" class="make-kinda-visible" onclick="toggleTable('CMD_ADMIN', id);">Admin</a></li>
</ul>

</div>
<div class="hoverable col s12" id="CMD_EVERYONE" style="display:inline-block" >

	<h5>Available to everyone:</h5>
	<table class="bordered striped">
	<thead>
		<tr>
		<th data-field="cmd">Command</th>
		<th data-field="desc">Description</th>
		<th data-field="ex">Example</th>
		</tr>
	</thead>
	<tbody>
		<tr>
		<td>~commands</td>
		<td>Sends a message with a link to this site</td>
		<td>~commands</td>
		</tr>

		<tr>
		<td>~idea <span style="color: #419837;">idea/feedback</span></td>
		<td>Send Ideas for Commands or Feedback</td>
		<td>~idea <span style="color: #419837;">Qwer gives everyone 10$</span></td>
		</tr>

		<tr>
		<td>~sites</td>
		<td>Lillys Site`s like YT, Twitch...</td>
		<td>~sites</td>
		</tr>

		<tr>
		<td>~add</td>
		<td>Want to add Lilly as Friend? this is your List</td>
		<td>~add</td>
		</tr>

		<tr>
		<td>~wishlist</td>
		<td>Lillys Amazon-Wishlist</td>
		<td>~wishlist</td>
		</tr>

		<tr>
		<td>~polls</td>
		<td>Active Polls</td>
		<td>~polls</td>
		</tr>

		<tr>
		<td>~gameserver</td>
		<td>IPs of the KatKrew Gamesservers Special thanks to Haikaido64</td>
		<td>~gameserver</td>
		</tr>

		<tr>
		<td>
		~weather<br>
		~weather <span style="color: #419837;">City/Land</span><br>
		~weather <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@User</span></td>
		<td>Display weather of your saved location or searched location or the saved location from @User (see ~setlocation)</td>
		<td>
		~weather<br>
		~weather <span style="color: #419837;">Norristown,PA</span><br>
		~weather <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@Qwer</span></td>
		</tr>
		
		<tr>
		<td>
		~weather10<br>
		~weather10 <span style="color: #419837;">City/Land</span><br>
		~weather10 <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@User</span></td>
		<td>Display a 10 day weather forecast of your saved location or searched location or <br>the saved location from @User (see ~setlocation)</td>
		<td>
		~weather10<br>
		~weather10 <span style="color: #419837;">Norristown,PA</span><br>
		~weather10 <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@Qwer</span></td>
		</tr>

		<tr>
		<td>
		~time<br>
		~time <span style="color: #419837;">City/State/Land</span><br>
		~time <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@User</span></td>
		<td>Display the local Time of your saved location or searched location or the saved location from @User (see ~setlocation)</td>
		<td>
		~time<br>
		~time <span style="color: #419837;">Norristown,PA</span><br>
		~time <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@Qwer</span></td>
		</tr>

		<tr>
		<td>
		~setlocation <span style="color: #419837;">City/State(Land)</span>
		<td>set(saves) your location for the commands ~weather, ~weather10 and ~time</td>
		<td>
		~setlocation <span style="color: #419837;">Norristown,PA</span>
		</tr>
		
		<tr>
		<td>
		~r6c <span style="color: #419837;">Uplayname</span><br>
		~r6r <span style="color: #419837;">Uplayname</span>
		<td>
		Display Rainbow6 Stats (Casual)<br>
		Display Rainbow6 Stats (Ranked)
		</td>
		<td>
		~r6c <span style="color: #419837;">Q_W_E_R</span><br>
		~r6r <span style="color: #419837;">Q_W_E_R</span>
		</tr>

		<tr>
		<td>
		~owc <span style="color: #419837;">Battletag#6969</span><br>
		~owr <span style="color: #419837;">Battletag#6969</span>
		<td>
		Display Overwatch Stats (Casual)<br>
		Display Overwatch Stats (Ranked)
		</td>
		<td>
		~owc <span style="color: #419837;">Cluepex#2250</span><br>
		~owr <span style="color: #419837;">Cluepex#2250</span>
		</tr>

		<tr>
		<td>
		~avatar<br>
		~avatar <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@User</span>
		<td>
		Post a link to the Avatar<br>
		</td>
		<td>
		~avatar<br>
		~avatar <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@Qwer</span>
		</tr>

		<tr>
		<td>~cat</td>
		<td>Random Cat picture from http://random.cat/</td>
		<td>~cat</td>
		</tr>

		<tr>
		<td>~krew</td>
		<td>Random KatKrew Pic</td>
		<td>~krew</td>
		</tr>

		<tr>
		<td>~lilly</td>
		<td>Random GIF/Oddshot/Pic of Lilly (to add Links see ~addlilly in Commands for the roles Bot Commander or Admin)</td>
		<td>~lilly</td>
		</tr>

		<tr>
		<td>~lillyc</td>
		<td>Shows the number of Links that are available for the ~lilly command</td>
		<td>~lillyc</td>
		</tr>

		<tr>
		<td>~say <span style="color: #419837;">text</span></td>
		<td>Make KatKrewBot say something</td>
		<td>~say <span style="color: #419837;">blablablabla</span></td>
		</tr>

		<tr>
		<td>~choice <span style="color: #419837;">choice1;choice2;...</span></td>
		<td>Decide between some choices</td>
		<td>~choice <span style="color: #419837;">dance;sleep;repeat</span></td>
		</tr>

		<tr>
		<td>~8ball <span style="color: #419837;">Question?</span></td>
		<td>Get a question answered 8-Ball style</td>
		<td>~8ball <span style="color: #419837;">Should i dye my hair?</span></td>
		</tr>

		<tr>
		<td>~coin</td>
		<td>Throw a coin</td>
		<td>~coin</td>
		</tr>

		<tr>
		<td>~rektlong</td>
		<td>REKT list (long)</td>
		<td>~rektlong</td>
		</tr>

		<tr>
		<td>~weed</td>
		<td>Smoke some weed</td>
		<td>~weed</td>
		</tr>

		<tr>
		<td>~snake</td>
		<td>Random picture of Snake</td>
		<td>~snake</td>
		</tr>

		<tr>
		<td>~ayy</td>
		<td>AYYLMAO ASCII-Art</td>
		<td>~ayy</td>
		</tr>

		<tr>
		<td>~kirby</td>
		<td>Kriby ASCII-Art</td>
		<td>~kirby</td>
		</tr>

		<tr>
		<td>~kappa</td>
		<td>KAPPA ASCII-Art</td>
		<td>~kappa</td>
		</tr>

		<tr>
		<td>~catbox</td>
		<td>CATINBOX ASCII-Art</td>
		<td>~catbox</td>
		</tr>
	</tbody>
	</table>
</div>

<div class="hoverable col s12" id="CMD_COMMANDER" style="display:none">
	<h5>Bot Commanders only:</h5>
	<p>Commands for Users with the role "Bot Commander"</p>
	<table class="bordered striped">
	<thead>
		<tr>
		<th data-field="cmd">Command</th>
		<th data-field="desc">Description</th>
		<th data-field="ex">Example</th>
		</tr>
	</thead>
	<tbody>

		<tr>
		<td>~tweetfeed <span style="color: #419837;">Twittername</span></td>
		<td>Activates TweetFeed for the given Twittername in the active Channel</td>
		<td>~tweetfeed <span style="color: #419837;">RealKittyRawr</span></td>
		</tr>

		<tr>
		<td>~tweetfeedRT <span style="color: #419837;">Twittername</span></td>
		<td>Activates TweetFeed + ReTweetFeed for the given Twittername in the active Channel</td>
		<td>~tweetfeedRT <span style="color: #419837;">RealKittyRawr</span></td>
		</tr>

		<tr>
		<td>~twitchfeed <span style="color: #419837;">Twittername</span></td>
		<td>Activates TwitchFeed for the given Twitchname in the active Channel</td>
		<td>~twitchfeed <span style="color: #419837;">kittyrawr</span></td>
		</tr>

		<tr>
		<td>~addlilly <span style="color: #0f96ca;"><i>Link1 Link2</i></span></td>
		<td>Adds 1 or more links of a GIF/Oddshot/Pic with Lilly to the Random List</td>
		<td>~addlilly <span style="color: #0f96ca;"><i>http://imgur.com/Pe2CtUY</i></span></td>
		</tr>

		<tr>
		<td>~remlilly <span style="color: #0f96ca;"><i>Link1 Link2</i></span></td>
		<td>Removes 1 or more links from the Random List</td>
		<td>~remlilly <span style="color: #0f96ca;"><i>http://imgur.com/Pe2CtUY</i></span></td>
		</tr>

		<tr>
		<td>~mute <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@User</span></td>
		<td>Mute User</td>
		<td>~mute <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@Qwer</span></td>
		</tr>

		<tr>
		<td>~unmute <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@User</span></td>
		<td>Unmute User</td>
		<td>~unmute <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@Qwer</span></td>
		</tr>

		<tr>
		<td>~mutechannel</td>
		<td>Deactivate Commands in this channel</td>
		<td>~mutechannel</td>
		</tr>

		<tr>
		<td>~unmutechannel</td>
		<td>Activate Commands in this channel</td>
		<td>~unmutechannel</td>
		</tr>

		<tr>
		<td>~prune <span style="color: #30f7ef;">number</span></td>
		<td>Deletes # of Messages</td>
		<td>~prune <span style="color: #30f7ef;">10</span></td>
		</tr>
	</tbody>
	</table>
</div>



<div class="hoverable col s12" id="CMD_ADMIN" style="display:none">
	<h5>Admin only:</h5>
	<p>Commands for Users with the role "Admin"</p>
	<table class="bordered striped">
	<thead>
		<tr>
		<th data-field="cmd">Command</th>
		<th data-field="desc">Description</th>
		<th data-field="ex">Example</th>
		</tr>
	</thead>
	<tbody>
		<tr>
		<td>~kick <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@User</span></td>
		<td>Kick User</td>
		<td>~kick <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@Qwer</span></td>
		</tr>

		<tr>
		<td>~ban <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@User</span></td>
		<td>Bans User only Server-Owner can unban!</td>
		<td>~ban <span style="color: #7289da; background-color: rgba(115,139,215,.1); font-weight: 600;">@Qwer</span></td>
		</tr>
	</tbody>
	</table>
</div>

</div>
</div>
</div>

<footer class="page-footer">
	  <div class="container">
		<div class="row">
		  <div class="col l6 s12">
			<h5 class="black-text">Channels this bot is active in:</h5>
			SpaceCandi: <a class="black-text" target="_blank" href="https://www.twitch.tv/spacecandi"><b>SpaceCandi</b></a><br>
			</p>
		  </div>
		</div>
	  </div>
</footer>
</body>
</html>
