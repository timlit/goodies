# Radio stations of Kyrgizstan



 <H1 id="header" onclick="playToggle()">Выбери станцию > / •  </H1>
 <div id="radioframe" visibility = "hidden"> <audio  id= "radio"   preload = "none">
Your browser does not support the audio element.</audio></div>  

<div>                         
<ul id="radioList"></ul>
</div>
<style>#radioList{font-size: 1.5em;}</style>

<script src="jquery-3.6.1.min.js">
</script>
<script>
//https://edutechwiki.unige.ch/en/HTML5_audio_and_video
/*
http://www.mediaelementjs.com/
https://github.com/videojs/video.js
https://videojs.com/forest


*/
var playtimeStart;
var playtimeEnd;
var playSign  = "› "; // |> > ›
var pauseSign = "• "; // || • ‖
var tagId
var tag
//
var radio = document.getElementById("radio"); 
//var radio = new Audio();
radio.preload="metadata";
setTimeout(() => {

  console.log(radio);
}, "5000")

var listdiv = '';
const list = radioList();
//_showRadioList();
list.forEach(showRadioList);

function _showRadiolist() {
	list.forEach(showRadioList);
}


function timeDif(dateStart, dateFinish){

	//var dateStart = new Date(2000, 0, 1,  9, 0); // 9:00 AM
	//var dateFinish = new Date(2000, 0, 1, 17, 0); // 5:00 PM

	// the following is to handle cases where the times are on the opposite side of
	// midnight e.g. when you want to get the difference between 9:00 PM and 5:00 AM

	if (dateFinish < dateStart) {
		dateFinish.setDate(dateFinish.getDate() + 1);
	}

	var diff = dateFinish - dateStart;


	var msec = diff;
	var hh = Math.floor(msec / 1000 / 60 / 60);
	msec -= hh * 1000 * 60 * 60;
	var mm = Math.floor(msec / 1000 / 60);
	msec -= mm * 1000 * 60;
	var ss = Math.floor(msec / 1000);
	msec -= ss * 1000;
	// diff = 28800000 => hh = 8, mm = 0, ss = 0, msec = 0
}

function playStation(nmb){
	//openwindow();
	if(nmb==tagId) return;
	var list = radioList();
	var candy = list[nmb].split("--");
	
	radio.src = candy[1].trim();		
	tagId = nmb;
	tag = candy[0].trim();
	playAudio();
	
}

function showRadioList(item, index, arr){
	//arr[index] = item 
	var pc = arr[index];
	var candy = pc.split("--");
	//radio.src = candy[1].trim();
	var tpl = '<li onclick="playStation(2)">Сүйүнчү </li>';
	listdiv += '<li onclick="playStation(' + index + ')">' + candy[0].trim() + ' </li>' ;
	
	document.getElementById("radioList").innerHTML = listdiv;

}

function radioList(){
	var list = [ 	
"	Марал Радиосу	--	http://212.42.115.186:8000/;stream.mp3	",
"	iRadio	--	http://212.112.123.200:8000/stream.ogg	",
"	Алмаз Бишкек 102.1 FM	--	http://almazfm.ddns.net:8888/;	",
"	Тумар FM	--	https://radio.tumar.fm:8005/stream	",
"	STUDIO 21	--	https://cdn.radioplayer.kg:8443/studio2164	",
"	Радио ОК	--	https://stream.okradio.kg:8005/stream	",
"	Manas FM	--	http://live.mediamanas.kg:8000/online	",
"	Санжыра радиосу	--	http://212.112.106.69:8000/sanjyra	",
"	Ретро FM Кыргызстан	--	https://cdn.radioplayer.kg:8443/retro128	",
"	Хит FM Кыргызстан	--	https://cdn.radioplayer.kg:8443/hitfm64	",
"	Кыргызстан Обондору	--	https://cdn.radioplayer.kg:8443/obondoru64	",
"	Кыргызстан Обондору GOLD	--	https://player.europa.kg:1075/stream?ver=74042	",
"	Кыргызстан Обондору FOLK	--	https://player.europa.kg:1105/stream?ver=162814	",
"	Сүйүнчү FM	--	https://cdn.radioplayer.kg:8443/suiunchu64	",

//"	БИРИНЧИ РАДИ	--	http://onlineradio.ktrk.kg:8080	",
//"	МИҢ КЫЯЛ FM	--	http://onlineradio.ktrk.kg:8081	",
//"	Кыргыз Радиосу	--	http://onlineradio.ktrk.kg:8083	",


"	Европа Плюс Кыргызстан	--	https://cdn.radioplayer.kg:8443/europa64	",
//"	Алмаз FM	--	http://almazfm.ddns.net:8888/	",
//"	Радио Пирамида	--	http://212.112.114.197:8000/	",
"	РАДИО ТАТИНА	--	http://s0.radioheart.ru:8000/RH20675	",
"	РАДИО ЛЮКС	--	https://player.europa.kg:1045/stream	",
"	FEVER	--	http://a.streamsin.space:8000/fever	",
"	IRADIO.ONE: 80's channel	--	http://a.streamsin.space:8000/80s	",
"	Emotions	--	http://a.streamsin.space:8000/emotions	",
"	Романтика	--	https://pub0101.101.ru:8000/stream/air/aac/64/101	",
"	Авторадио Киргизия	--	http://212.112.106.66:8080/	",

"	Радио Sputnik Кыргызстан	--	https://icecast-rian.cdnvideo.ru/voicekgz	",
"	ТНТ Music Radio	--	https://tntradio.hostingradio.ru:8027/tntradio128.mp3	",
"	Радио Рекорд Кыргызстан	--	http://31.186.50.67:8000/record.mp3	",
	];
	return list;
}

function openwindow()
{
var newwindow= window.open('', '', 'width=300, height=300');
newwindow.document.write("<p>This is My Web Page</p>");
}


function playToggle() {
if(tagId=== undefined) return;
  if(radio.paused){playAudio();}else{pauseAudio(); }
}

function playAudio() { 
	radio.play(); 
	radio.onloadedmetadata = function() {
	
    /*
	console.log(radio.mediaGroup);
	console.log(radio.controller);
    console.log(radio.currentTime);
    console.log(radio.defaultPlaybackRate);
    console.log(radio.crossOrigin);
    console.log(radio.currentSrc);
	*/
    //alert(radio.textTracks);
    //alert("Metadata for video loaded");
}
	
	//console.log(radio.audio);
  document.getElementById("header").innerHTML = playSign + tag ;
} 

function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

//getAudioMetaData("https://radio.tumar.fm:8005/stream");
//sleep(10);

function getAudioMetaData(src) {
    return new Promise(function(resolve) {
        radio = new Audio();

        $(radio).on("loadedmetadata", function() {
            resolve(radio);
        });

        radio.preload = 'metadata';
        radio.src = src;
		//console.log(radio.networkState);
    });
}

function radioMeta(){
$(a1).bind('loadedmetadata', function(e){
        //alert('a1 ' + a1.duration + ' ' + a1.networkState);
    });

    $(a1).bind('canplay', function(e){
        alert('a1z ' + ' ' + a1.networkState);
    });

    $(a1).attr('preload', 'metadata');
    a1.preload = 'metadata';
    //alert(a1.duration);
    //a1.play();
    a1.load();
    $('div').click(function(e){
        alert('a1z ' + ' ' + a1.networkState);
    });
}

function pauseAudio() { 
  //playerClear();
  radio.pause(); 
  document.getElementById("header").innerHTML = pauseSign + tag ;
} 

function playerClear(){
	radio.pause();
	radio.source = null;
	//console.log(radio.volume);
	radio.volume = 1;
	radio.currentTime = 0;
	<!-- radio.load(); -->
}

			
/*
https://top-radio.ru/bishkek
https://unicode-table.com/en/html-entities/
https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement/Audio
https://learn.microsoft.com/en-us/aspnet/core/blazor/components/event-handling?source=recommendations&view=aspnetcore-6.0
https://learn.microsoft.com/en-us/aspnet/core/blazor/components/lifecycle?view=aspnetcore-6.0#when-parameters-are-set-setparametersasync
https://learn.microsoft.com/en-us/dotnet/maui/fundamentals/shell/lifecycle

	
<div id="radioframe" visibility = "hidden"> <audio  id= "radio"   preload = "none">
Your browser does not support the audio element.</audio></div>  

  <button id="PlayPause" onclick="playAudio()" type="button">PlayPause</button>
  <button onclick="pauseAudio()" type="button">Pause</button><br> 

//https://github.com/jucrouzet/icecast.js
//http://www.schillmania.com/projects/soundmanager2/
https://eshaz.github.io/icecast-metadata-js/demo.html
*/
</script>
