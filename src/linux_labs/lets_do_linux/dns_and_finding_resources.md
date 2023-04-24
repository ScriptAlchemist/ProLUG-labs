# DNS and finding resources

### Check all DNS tools to find resources

```admonish summary
🐧 Your team is going to be doign some DNS work and you have to
figure out how o use the tools in your Linux system

🐧 Use host, dig, nslookup and figure out what type of  information
they show you

🐧 Check the contents of `/etc/resolv.conf`

🐧 Do a traceroute to 8.8.8.8 and 1.1.1.1
```

---

### 1. Use the host command to `www.google.com`

~~~admonish example title="Input"
```bash
host www.google.com
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ host www.google.com
www.google.com has address 172.253.115.106
www.google.com has address 172.253.115.99
www.google.com has address 172.253.115.104
www.google.com has address 172.253.115.147
www.google.com has address 172.253.115.103
www.google.com has address 172.253.115.105
www.google.com has IPv6 address 2607:f8b0:4004:c06::68
www.google.com has IPv6 address 2607:f8b0:4004:c06::63
www.google.com has IPv6 address 2607:f8b0:4004:c06::69
www.google.com has IPv6 address 2607:f8b0:4004:c06::93
```
~~~

#### 💬 What information are you seeing? How many IP addresses are there? How many are IPv4 and IPv6?

```text,editable
// What do you think?


```

### 2. Use the dig command against `www.google.com`

~~~admonish example title="Input"
```bash
dig www.google.com
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ dig www.google.com

; <<>> DiG 9.16.1-Ubuntu <<>> www.google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 44512
;; flags: qr rd ra; QUERY: 1, ANSWER: 6, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;www.google.com.                        IN      A

;; ANSWER SECTION:
www.google.com.         60      IN      A       172.253.115.106
www.google.com.         60      IN      A       172.253.115.99
www.google.com.         60      IN      A       172.253.115.104
www.google.com.         60      IN      A       172.253.115.105
www.google.com.         60      IN      A       172.253.115.147
www.google.com.         60      IN      A       172.253.115.103

;; Query time: 4 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Mon Apr 24 11:27:20 UTC 2023
;; MSG SIZE  rcvd: 139

```
~~~

#### 💬 How many A records do you see?

#### 💬 What server was used for the DNS query?


```text,editable
// What do you think?


```

#### 💬 This prompts you to wonder where you system gets it's configuration for DNS.

### 3. Check the `/etc/resolve.conf` to see where system is looking at DNS

~~~admonish example title="Input"
```bash
cat /etc/resolv.conf
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ cat /etc/resolv.conf
# This file is managed by man:systemd-resolved(8). Do not edit.
#
# This is a dynamic resolv.conf file for connecting local clients directly to
# all known uplink DNS servers. This file lists all configured search domains.
#
# Third party programs must not access this file directly, but only through the
# symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a different way,
# replace this symlink by a static file or a different symlink.
#
# See man:systemd-resolved.service(8) for details about the supported modes of
# operation for /etc/resolv.conf.

nameserver 8.8.8.8
nameserver 1.1.1.1
```
~~~

### 4. What nameservers does you system try to use? Enter those into `/root/nameservers`

~~~admonish example title="Input"
```bash
cat /etc/resolv.conf | grep nameserver > /root/nameservers
```
~~~

#### 💬 Traceroute must be installed on this system

### 5. Use traceroute to see if you can map the hops from you to `www.google.com`

~~~admonish example title="Input"
```bash
traceroute www.google.com
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ traceroute www.google.com
traceroute to www.google.com (172.253.115.105), 30 hops max, 60 byte packets
 1  172.30.1.1 (172.30.1.1)  0.329 ms  0.193 ms  0.135 ms
 2  ns1005533.ip-135-148-34.us (135.148.34.20)  0.172 ms  0.360 ms  0.294 ms
 3  135.148.34.252 (135.148.34.252)  0.815 ms  0.745 ms  0.997 ms
 4  10.23.178.2 (10.23.178.2)  0.938 ms  0.897 ms  0.819 ms
 5  10.244.5.60 (10.244.5.60)  0.903 ms 10.244.5.70 (10.244.5.70)  0.979 ms 10.244.5.58 (10.244.5.58)  0.996 ms
 6  10.244.64.48 (10.244.64.48)  0.320 ms 10.244.64.52 (10.244.64.52)  0.315 ms 10.244.64.50 (10.244.64.50)  0.276 ms
 7  10.244.120.4 (10.244.120.4)  0.911 ms 10.244.120.2 (10.244.120.2)  0.957 ms 10.244.120.4 (10.244.120.4)  0.935 ms
 8  was-nva1-sbb1-nc5.va.us (178.32.135.154)  2.186 ms  1.715 ms was-cva1-sbb1-nc5.va.us (178.32.135.210)  1.487 ms
 9  * * *
10  google.as15169.va.us (192.99.146.115)  3.353 ms  3.336 ms *
11  * * *
12  108.170.246.33 (108.170.246.33)  2.838 ms 142.251.77.64 (142.251.77.64)  1.597 ms 108.170.246.33 (108.170.246.33)  2.820 ms
13  108.170.246.49 (108.170.246.49)  2.058 ms 108.170.246.2 (108.170.246.2)  4.852 ms 108.170.246.66 (108.170.246.66)  2.211 ms
14  * 216.239.63.235 (216.239.63.235)  2.949 ms 142.251.49.73 (142.251.49.73)  2.710 ms
15  142.251.247.191 (142.251.247.191)  2.680 ms 142.251.49.199 (142.251.49.199)  3.166 ms 142.250.210.27 (142.250.210.27)  3.604 ms
16  * * 142.251.77.138 (142.251.77.138)  3.275 ms
17  172.253.72.202 (172.253.72.202)  3.826 ms 172.253.67.50 (172.253.67.50)  3.157 ms 142.251.52.184 (142.251.52.184)  3.339 ms
18  172.253.66.201 (172.253.66.201)  2.424 ms 172.253.66.157 (172.253.66.157)  3.393 ms 172.253.66.201 (172.253.66.201)  2.574 ms
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  bg-in-f105.1e100.net (172.253.115.105)  2.780 ms  2.516 ms  2.632 ms
```
~~~

#### 💬 What output do you see?

#### 💬 Are all the addresses shown?

#### 💬 What is the highest latency you see between hops?

```text,editable
// What do you think?


```

---

#### Change the order in which your system looks up resources

```admonish summary
🐧 Now you've looked around with the tools that you have. Let's
figure out the order you system looks up resources in

🐧 Inspect the `/etc/nsswitch.conf` file to see how your system looks
up hosts

🐧 Verify that your system look at files before DNS by adding a
record for `www.google.com` that points to `www.yahoo.com`

🐧 Change the order of host lookup in `/etc/nsswitch.conf` to see the
system properly resolve `www.google.com`
```

### 6. Print out `/etc/nsswitch.conf`

~~~admonish example title="Input"
```bash
cat /etc/nsswitch.conf
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ cat /etc/nsswitch.conf 
# /etc/nsswitch.conf
#
# Example configuration of GNU Name Service Switch functionality.
# If you have the `glibc-doc-reference' and `info' packages installed, try:
# `info libc "Name Service Switch"' for information about this file.

passwd:         files systemd
group:          files systemd
shadow:         files
gshadow:        files

hosts:          files dns
networks:       files

protocols:      db files
services:       db files
ethers:         db files
rpc:            db files

netgroup:       nis
```
~~~

#### 💬 What are the values in the hosts: entry?

### 7. Test your connection to `www.google.com` with curl

~~~admonish example title="Input"
```bash
curl www.google.com | grep -Ei 'yahoo|google'
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ curl www.google.com | grep -Ei 'yahoo|google'
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="en"><head><meta content="Search the world's information, including webpages, images, videos and more. Google has many special features to help you find exactly what you're looking for." name="description"><meta content="noodp" name="robots"><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="IjzW5Y8RmVESmT0mXulCJw">(function(){window.google={kEI:'7mtGZPP4Ds-p5NoPmsKCgA0',kEXPI:'0,1359409,6059,206,4804,2316,383,246,5,1129120,1197711,180,380600,16114,19397,9287,22430,1362,12314,4751,12834,4998,13228,3847,35735,5581,2891,3926,213,8221,76014,432,3,346,1244,1,16918,2650,4,1528,2304,29062,13063,13660,2980,1457,16786,5806,2551,4094,7596,1,14262,24780,1,3111,2,14022,2373,342,21266,1758,5679,1021,31121,4568,6259,23418,1252,5835,14968,4332,7484,445,2,2,1,26632,8155,7381,2,3,15965,872,6578,3048,10008,7,1922,9779,36154,6305,20198,20137,14,82,2932,13582,3692,109,363,2049,850,3909,1097,1747,2038,15203,4387,988,3030,5629,481,9706,1804,823,3976,2935,495,1150,1093,493,1360,1032,9480,2995,6849,416,2171,3609,3049,2129,2365,648,14,340,1295,1093,19,495,4197,2,1838,304,891,3576,1442,1129,777,5326,1666,507,1463,1973,1365,804,884,264,3,2824,344,173,119,344,196,911,1,1224,2012,688,329,379,2,297,1644,123,49,1015,1,728,766,225,717,55,198,402,214,5,181,403,577,2855,737,36,126,573,5,864,38,104,214,280,102,577,572,406,151,120,256,253,179,571,206,2,10,3,655,74,1142,604,5206696,189,2,70,5995623,2803220,3311,141,795,19735,1,1,346,5008,30,43,10,2,32,9,1,5,1,12,6,1,123,21,2,2,1,58,23945117,4042143,1964,1007,15665,2894,6250,15739,1326,400,714,328,121,1412168,146986,21413709,2198897,361,83,95,132,554,505,384,568,86,1,1026,29,2,325,19,1697,299,413,1657,1615,1142,123,62',kBL:'WWhe',kOPI:89978449};google.sn='webhp';google.kHL='en';})();(function(){
var e=this||self;var g,h=[];function k(a){for(var c;a&&(!a.getAttribute||!(c=a.getAttribute("eid")));)a=a.parentNode;return c||g}function l(a){for(var c=null;a&&(!a.getAttribute||!(c=a.getAttribute("leid")));)a=a.parentNode;return c}function m(a){/^http:/i.test(a)&&"https:"===window.location.protocol&&(google.ml&&google.ml(Error("a"),!1,{src:a,glmm:1}),a="");return a}
function p(a,c,b,f){var d="";-1===c.search("&ei=")&&(d="&ei="+k(b),-1===c.search("&lei=")&&(b=l(b))&&(d+="&lei="+b));b="";e._cshid&&-1===c.search("&cshid=")&&"slh"!==a&&(b="&cshid="+e._cshid);return"/"+(f||"gen_204")+"?atyp=i&ct="+String(a)+"&cad="+(c+d)+"&zx="+String(Date.now())+b};g=google.kEI;google.getEI=k;google.getLEI=l;google.ml=function(){return null};google.log=function(a,c,b,f,d){b||(b=p(a,c,f,d));if(b=m(b)){a=new Image;var n=h.length;h[n]=a;a.onerror=a.onload=a.onabort=function(){delete h[n]};a.src=b}};google.logUrl=function(a){return p("",a)};}).call(this);(function(){google.y={};google.sy=[];google.x=function(a,b){if(a)var c=a.id;else{do c=Math.random();while(google.y[c])}google.y[c]=[a,b];return!1};google.sx=function(a){google.sy.push(a)};google.lm=[];google.plm=function(a){google.lm.push.apply(google.lm,a)};google.lq=[];google.load=function(a,b,c){google.lq.push([[a],b,c])};google.loadAll=function(a,b){google.lq.push([a,b])};google.bx=!1;google.lx=function(){};}).call(this);google.f={};(function(){
</style><style>body,td,a,p,.h{font-family:arial,sans-serif}body{margin:0;overflow-y:scroll}#gog{padding:3px 8px 0}td{line-height:.8em}.gac_m td{line-height:17px}form{margin-bottom:20px}.h{color:#1558d6}em{font-weight:bold;font-style:normal}.lst{height:25px;width:496px}.gsfi,.lst{font:18px arial,sans-serif}.gsfs{font:17px arial,sans-serif}.ds{display:inline-box;display:inline-block;margin:3px 0 4px;margin-left:4px}input{font-family:inherit}body{background:#fff;color:#000}a{color:#4b11a8;text-decoration:none}a:hover,a:active{text-decoration:underline}.fl a{color:#1558d6}a:visited{color:#4b11a8}.sblc{padding-top:5px}.sblc a{display:block;margin:2px 0;margin-left:13px;font-size:11px}.lsbb{background:#f8f9fa;border:solid 1px;border-color:#dadce0 #70757a #70757a #dadce0;height:30px}.lsbb{display:block}#WqQANb a{display:inline-block;margin:0 12px}.lsb{background:url(/images/nav_logo229.png) 0 -261px repeat-x;border:none;color:#000;cursor:pointer;height:30px;margin:0;outline:0;font:15px arial,sans-serif;vertical-align:top}.lsb:active{background:#dadce0}.lst:focus{outline:none}</style><script nonce="IjzW5Y8RmVESmT0mXulCJw">(function(){window.google.erd={jsr:1,bv:1781,de:true};
var h=this||self;var k,l=null!=(k=h.mei)?k:1,n,p=null!=(n=h.sdo)?n:!0,q=0,r,t=google.erd,v=t.jsr;google.ml=function(a,b,d,m,e){e=void 0===e?2:e;b&&(r=a&&a.message);if(google.dl)return google.dl(a,e,d),null;if(0>v){window.console&&console.error(a,d);if(-2===v)throw a;b=!1}else b=!a||!a.message||"Error loading script"===a.message||q>=l&&!m?!1:!0;if(!b)return null;q++;d=d||{};b=encodeURIComponent;var c="/gen_204?atyp=i&ei="+b(google.kEI);google.kEXPI&&(c+="&jexpid="+b(google.kEXPI));c+="&srcpg="+b(google.sn)+"&jsr="+b(t.jsr)+"&bver="+b(t.bv);var f=a.lineNumber;void 0!==f&&(c+="&line="+f);var g=
a.fileName;g&&(0<g.indexOf("-extension:/")&&(e=3),c+="&script="+b(g),f&&g===window.location.href&&(f=document.documentElement.outerHTML.split("\n")[f],c+="&cad="+b(f?f.substring(0,300):"No script found.")));c+="&jsel="+e;for(var u in d)c+="&",c+=b(u),c+="=",c+=b(d[u]);c=c+"&emsg="+b(a.name+": "+a.message);c=c+"&jsst="+b(a.stack||"N/A");12288<=c.length&&(c=c.substr(0,12288));a=c;m||google.log(0,"",a);return a};window.onerror=function(a,b,d,m,e){r!==a&&(a=e instanceof Error?e:Error(a),void 0===d||"lineNumber"in a||(a.lineNumber=d),void 0===b||"fileName"in a||(a.fileName=b),google.ml(a,!1,void 0,!1,"SyntaxError"===a.name||"SyntaxError"===a.message.substring(0,11)||-1!==a.message.indexOf("Script error")?3:0));r=null;p&&q>=l&&(window.onerror=null)};})();</script></head><body bgcolor="#fff"><script nonce="IjzW5Y8RmVESmT0mXulCJw">(function(){var src='/images/nav_logo229.png';var iesg=false;document.body.onload = function(){window.n && window.n();if (document.images){new Image().src=src;}
})();</script><div id="mngb"><div id=gbar><nobr><b class=gb1>Search</b> <a class=gb1 href="http://www.google.com/imghp?hl=en&tab=wi">Images</a> <a class=gb1 href="http://maps.google.com/maps?hl=en&tab=wl">Maps</a> <a class=gb1 href="https://play.google.com/?hl=en&tab=w8">Play</a> <a class=gb1 href="https://www.youtube.com/?tab=w1">YouTube</a> <a class=gb1 href="https://news.google.com/?tab=wn">News</a> <a class=gb1 href="https://mail.google.com/mail/?tab=wm">Gmail</a> <a class=gb1 href="https://drive.google.com/?tab=wo">Drive</a> <a class=gb1 style="text-decoration:none" href="https://www.google.com/intl/en/about/products?tab=wh"><u>More</u> &raquo;</a></nobr></div><div id=guser width=100%><nobr><span id=gbn class=gbi></span><span id=gbf class=gbf></span><span id=gbe></span><a href="http://www.google.com/history/optout?hl=en" class=gb4>Web History</a> | <a  href="/preferences?hl=en" class=gb4>Settings</a> | <a target=_top id=gb_70 href="https://accounts.google.com/ServiceLogin?hl=en&passive=true&continue=http://www.google.com/&ec=GAZAAQ" class=gb4>Sign in</a></nobr></div><div class=gbh style=left:0></div><div class=gbh style=right:0></div></div><center><br clear="all" id="lgpd"><div id="lga"><img alt="Google" height="92" src="/images/branding/googlelogo/1x/googlelogo_white_background_color_272x92dp.png" style="padding:28px 0 14px" width="272" id="hplogo"><br><br></div><form action="/search" name="f"><table cellpadding="0" cellspacing="0"><tr valign="top"><td width="25%">&nbsp;</td><td align="center" nowrap=""><input name="ie" value="ISO-8859-1" type="hidden"><input value="en" name="hl" type="hidden"><input name="source" type="hidden" value="hp"><input name="biw" type="hidden"><input name="bih" type="hidden"><div class="ds" style="height:32px;margin:4px 0"><input class="lst" style="margin:0;padding:5px 8px 0 6px;vertical-align:top;color:#000" autocomplete="off" value="" title="Google Search" maxlength="2048" name="q" size="57"></div><br style="line-height:0"><span class="ds"><span class="lsbb"><input class="lsb" value="Google Search" name="btnG" type="submit"></span></span><span class="ds"><span class="lsbb"><input class="lsb" id="tsuid_1" value="I'm Feeling Lucky" name="btnI" type="submit"><script nonce="IjzW5Y8RmVESmT0mXulCJw">(function(){var id='tsuid_1';document.getElementById(id).onclick = function(){if (this.form.q.value){this.checked = 1;if (this.form.iflsig)this.form.iflsig.disabled = false;}
else top.location='/doodles/';};})();</script><input value="AOEireoAAAAAZEZ5_p2BEYJPRurP18-6pS39ZrNCXtzo" name="iflsig" type="hidden"></span></span></td><td class="fl sblc" align="left" nowrap="" width="25%"><a href="/advanced_search?hl=en&amp;authuser=0">Advanced search</a></td></tr></table><input id="gbv" name="gbv" type="hidden" value="1"><script nonce="IjzW5Y8RmVESmT0mXulCJw">(function(){var a,b="1";if(document&&document.getElementById)if("undefined"!=typeof XMLHttpRequest)b="2";else if("undefined"!=typeof ActiveXObject){var c,d,e=["MSXML2.XMLHTTP.6.0","MSXML2.XMLHTTP.3.0","MSXML2.XMLHTTP","Microsoft.XMLHTTP"];for(c=0;d=e[c++];)try{new ActiveXObject(d),b="2"}catch(h){}}a=b;if("2"==a&&-1==location.search.indexOf("&gbv=2")){var f=google.gbvu,g=document.getElementById("gbv");g&&(g.value=a);f&&window.setTimeout(function(){location.href=f},0)};}).call(this);</script></form><div id="gac_scont"></div><div style="font-size:83%;min-height:3.5em"><br><div id="prm"><style>.szppmdbYutt__middle-slot-promo{font-size:small;margin-bottom:32px}.szppmdbYutt__middle-slot-promo a.ZIeIlb{display:inline-block;text-decoration:none}.szppmdbYutt__middle-slot-promo img{border:none;margin-right:5px;vertical-align:middle}</style><div class="szppmdbYutt__middle-slot-promo" data-ved="0ahUKEwjzp5DjuML-AhXPFFkFHRqhANAQnIcBCAQ"><a class="NKcBbd" href="https://www.google.com/url?q=https://artsandculture.google.com/experiment/zgFx1tMqeIZyTw%3Futm_source%3Dgoogle%26utm_medium%3Dhppromo%26utm_campaign%3Dcallinginourcorals&amp;source=hpp&amp;id=19034922&amp;ct=3&amp;usg=AOvVaw0nMWsnMoeASDuSYrKnPMNj&amp;sa=X&amp;ved=0ahUKEwjzp5DjuML-AhXPFFkFHRqhANAQ8IcBCAU" rel="nofollow">Learn how to help restore coral reefs, simply by listening</a></div></div></div><span id="footer"><div style="font-size:10pt"><div style="margin:19px auto;text-align:center" id="WqQANb"><a href="/intl/en/ads/">Advertising</a><a href="/services/">Business Solutions</a><a href="/intl/en/about.html">About Google</a></div></div><p style="font-size:8pt;color:#70757a">&copy; 2023 - <a href="/intl/en/policies/privacy/">Privacy</a> - <a href="/intl/en/policies/terms/">Terms</a></p></span></center><script nonce="IjzW5Y8RmVESmT0mXulCJw">(function(){window.google.cdo={height:757,width:1440};(function(){var a=window.innerWidth,b=window.innerHeight;if(!a||!b){var c=window.document,d="CSS1Compat"==c.compatMode?c.documentElement:c.body;a=d.clientWidth;b=d.clientHeight}a&&b&&(a!=google.cdo.width||b!=google.cdo.height)&&google.log("","","/client_204?&atyp=i&biw="+a+"&bih="+b+"&ei="+googl.kEI);}).call(this);})();</script> <script nonce="IjzW5Y8RmVESmT0mXulCJw">(function()google.xjs={ck:'xjs.hp.cZMjK1rN2dw.L.X.O',cs:'ACT90oGdWgvp7b-1i002ub8NTEiqmwqPag',excm:[]};})();</script>  <script nonce="IjzW5Y8RmVESmT0mXulCJw">(function(){var u='/xjs/_/js/k\x3dxjs.hp.en.qkDX73W2TvU.O/am\x3dAAAAOgEAFABY/d\x3d1/ed\x3d1/rs\x3dACT90oFpp8_uyj9hwoAl3W3tvYwd1PFWOg/m\x3dsb_he,d';var amd=0;
function p(){var c=u,g=function(){};google.lx=google.stvsc?g:function(){google.timers&&google.timers.load&&google.tick&&google.tick("load","xjsls");var a=document;var b="SCRIPT";"application/xhtml+xml"===a.contentType&&(b=b.toLowerCase());b=a.createElement(b);a=null===c?"null":void 0===c?"undefined":c;if(void 0===h){var d=null;var m=e.trustedTypes;if(m&&m.createPolicy){try{d=m.createPolicy("goog#html",{createHTML:f,createScript:f,createScriptURL:f})}catch(r){e.console&&e.console.error(r.message)}h=
d}else h=d}a=(d=h)?d.createScriptURL(a):a;a=new n(a,l);b.src=a instanceof n&&a.constructor===n?a.g:"type_error:TrustedResourceUrl";var k,q;(k=(a=null==(q=(k=(b.ownerDocument&&b.ownerDocument.defaultView||window).document).querySelector)?void 0:q.call(k,"script[nonce]"))?a.nonce||a.getAttribute("nonce")||"":"")&&b.setAttribute("nonce",k);document.body.appendChild(b);google.psa=!0;google.lx=g};google.bx||google.lx()};googl.xjsu=u;e._F_jsUrl=u;setTimeout(function(){0<amd?google.caft(function(){return p()},amd):p()},0);})();window._ = window._ || {};window._DumpException = _._DumpException = function(e){throw e;};window._s = window._s || {};_s._DumpException = _._DumpException;window._qs = window._qs || {};_qs._DumpException = _._DumpException;function _F_installCss(c){}
(function(){google.jl={blt:'none',chnk:0,dw:false,dwu:true,emtn:0,end:0,ico:false,ikb:0,ine:false,injs:'none',injt:0,injth:0,injv2:false,lls:'default',pdt:0,rep:0,snet:true,strt:0,ubm:false,uwp:true};})();(function(){var pmc='{\x22d\x22:{},\x22sb_he\x22:{\x22agen\x22:true,\x22cgen\x22:true,\x22client\x22:\x22heirloom-hp\x22,\x22dh\x22:true,\x22ds\x22:\x22\x22,\x22fl\x22:true,\x22host\x22:\x22google.com\x22,\x22jsonp\x22:true,\x22msgs\x22:{\x22cibl\x22:\x22Clear Search\x22,\x22dym\x22:\x22Did you mean:\x22,\x22lcky\x22:\x22I\\u0026#39;m Feeling Lucky\x22,\x22lml\x22:\x22Learn more\x22,\x22psrc\x22:\x22This search was removed from your \\u003Ca href\x3d\\\x22/history\\\x22\\u003EWeb History\\u003C/a\\u003E\x22,\x22psrl\x22:\x22Remove\x22,\x22sbit\x22:\x22Search by image\x22,\x22srch\x22:\x22Google Search\x22},\x22ovr\x22:{},\x22pq\x22:\x22\x22,\x22rfs\x22:[],\x22sbas\x22:\x220 3px 8px 0 rgba(0,0,0,0.2),0 0 0 1px rgba(0,0,0,0.08)\x22,\x22stok\x22:\x22FNN--YlyXcWScgCAYZn3s7PjNSM\x22}}';google.pmc=JSON.parse(pmc);})();(function(){
100 17194    0 17194    0     0   305k      0 --:--:-- --:--:-- --:--:--  305k
var b=function(a){var c=0;return function(){return c<a.length?{done:!1,value:a[c++]}:{done:!0}}},e=this||self;var g,h;a:{for(var k=["CLOSURE_FLAGS"],l=e,n=0;n<k.length;n++)if(l=l[k[n]],null==l){h=null;break a}h=l}var p=h&&h[610401301];g=null!=p?p:!1;var q,r=e.navigator;q=r?r.userAgentData||null:null;function t(a){return g?q?q.brands.some(function(c){return(c=c.brand)&&-1!=c.indexOf(a)}):!1:!1}function u(a){var c;a:{if(c=e.navigator)if(c=c.userAgent)break a;c=""}return-1!=c.indexOf(a)};function v(){return g?!!q&&0<q.brands.length:!1}function w(){return u("Safari")&&!(x()||(v()?0:u("Coast"))||(v()?0:u("Opera"))||(v()?0:u("Edge"))||(v()?t("Microsoft Edge"):u("Edg/"))||(v()?t("Opera"):u("OPR"))||u("Firefox")||u("FxiOS")||u("Silk")||u("Android"))}function x(){return v()?t("Chromium"):(u("Chrome")||u("CriOS"))&&!(v()?0:u("Edge"))||u("Silk")}function y(){return u("Android")&&!(x()||u("Firefox")||u("FxiOS")||(v()?0:u("Opera"))||u("Silk"))};var z=v()?!1:u("Trident")||u("MSIE");y();x();w();var A=!z&&!w(),D=function(a){if(/-[a-z]/.test("ved"))return null;if(A&&a.dataset){if(y()&&!("ved"in a.dataset))return null;a=a.dataset.ved;return void 0===a?null:a}return a.getAttribute("data-"+"ved".replace(/([A-Z])/g,"-$1").toLowerCase())};var E=[],F=null;function G(a){a=a.target;var c=performance.now(),f=[],H=f.concat,d=E;if(!(d instanceof Array)){var m="undefined"!=typeof Symbol&&Symbol.iterator&&d[Symbol.iterator];if(m)d=m.call(d);else if("number"==typeof d.length)d={next:b(d)};else throw Error("a`"+String(d));for(var B=[];!(m=d.next()).done;)B.push(m.value);d=B}E=H.call(f,d,[c]);if(a&&a instanceof HTMLElement)if(a===F){if(c=4<=E.length)c=5>(E[E.length-1]-E[E.length-4])/1E3;if(c){c=google.getEI(a);a.hasAttribute("data-ved")?f=a?D(a)||"":"":f=(f=
a.closest("[data-ved]"))?D(f)||"":"";f=f||"";if(a.hasAttribute("jsname"))a=a.getAttribute("jsname");else{var C;a=null==(C=a.closest("[jsname]"))?void 0:C.getAttribute("jsname")}google.log("rcm","&ei="+c+"&ved="+f+"&jsname="+(a||""))}}else F=a,E=[c]}window.document.addEventListener("DOMContentLoaded",function(){document.body.addEventListener("click",G)});}).call(this);</script></body></html>
```
~~~

#### 💬 Wow that's some ugly output related to google

### 8. Let's get the host value for `www.yahoo.com`

~~~admonish example title="Input"
```bash
host www.yahoo.com
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ host www.yahoo.com
www.yahoo.com is an alias for new-fp-shed.wg1.b.yahoo.com.
new-fp-shed.wg1.b.yahoo.com has address 74.6.143.25
new-fp-shed.wg1.b.yahoo.com has address 74.6.143.26
new-fp-shed.wg1.b.yahoo.com has address 74.6.231.20
new-fp-shed.wg1.b.yahoo.com has address 74.6.231.21
new-fp-shed.wg1.b.yahoo.com has IPv6 address 2001:4998:124:1507::f001
new-fp-shed.wg1.b.yahoo.com has IPv6 address 2001:4998:44:3507::8000
new-fp-shed.wg1.b.yahoo.com has IPv6 address 2001:4998:124:1507::f000
new-fp-shed.wg1.b.yahoo.com has IPv6 address 2001:4998:44:3507::8001
```
~~~

### 9. Now, just to test that our system will use hosts first, before DNS, we're going to add a `www.yahoo.com` entry in our `/etc/hosts` file

~~~admonish example title="Input"
```bash
echo "74.6.231.21 www.google.com" >> /etc/hosts
```
~~~

### 10. Let's test a curl to `www.google.com` and see if we're still resolving to `www.google.com`

~~~admonish example title="Input"
```bash
curl www.google.com | grep -Ei 'yahoo|google'
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ curl www.google.com | grep -Ei 'yahoo|google'
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
    <title>Yahoo</title>
      !function(){if(window==window.top){var o=window.location.host;o.endsWith(".yahoo.com")&&window.location.replace("https://www.yahoo.com/"),o.endsWith(".aol.com")&&window.location.replace("https://www.aol.com/"),o.endsWith(".huffpost.com")&&window.location.replace("https://www.huffpost.com/"),o.endsWith(".engadget.com")&&window.location.replace("https://www.engadget.com/")}}();
  <!-- host machine: media-router-fp7028.prod.media.ne1.yahoo.com -->
  <!-- url: http://www.google.com/-->
          logo: 'https://s.yimg.com/rz/p/yahoo_frontpage_en-US_s_f_p_205x58_frontpage.png',
          logoAlt: 'Yahoo Logo',
        document.write('<img src="' + buildUrl('//geo.yahoo.com/b', params) + '" style="display:none;" width="0px" height="0px"/>');
        beacon.src = buildUrl('//bcn.fp.yahoo.com/p', params);
100  4863  100  4863    0     0  74815      0 --:--:-- --:--:-- --:--:-- 74815
        ats_host: 'media-router-fp7028.prod.media.ne1.yahoo.com',
```
~~~

### 11. Now we change the order so that our `/etc/nsswitch` entry for hosts shows DNS before host values

~~~admonish example title="Input"
```bash
vi /etc/nsswitch.conf

#fix the line to:
host:       dns files
```
~~~

[VIM commands](../../tools/vim/basic_vim.md)

### 12. Now test `www.google.com` again and see if you're seeing the correct output

~~~admonish example title="Input"
```bash
curl www.google.com | grep -Ei 'yahoo|google'
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ curl www.google.com | grep -Ei 'yahoo|google'
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="en"><head><meta content="Search the world's information, including webpages, images, videos and more. Google has many special features to help you find exactly what you're looking for." name="description"><meta content="noodp" name="robots"><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="sVkp7jIK8JntD0iWAfSxFw">(function(){window.google={kEI:'tW5GZP-GNtSm5NoPubuvgA0',kEXPI:'0,1303427,55982,6058,207,4804,2316,383,246,5,1129120,1197787,104,380599,16115,28684,22431,1361,12312,4753,12834,4998,13228,3847,6885,31559,885,1987,2891,3926,213,4210,3405,606,58286,2404,15324,432,3,1590,1,16916,2652,4,1528,2304,29062,9872,3191,11444,2216,2980,1457,16786,5821,2536,4094,7596,1,42154,2,14022,2373,342,3534,19490,5679,1020,25048,6075,4567,6256,23421,1252,5835,14968,4332,7484,445,2,2,1,24626,2006,8155,6680,701,2,3,15965,872,9626,10009,6,1922,28322,17611,6305,20198,20137,14,82,16514,3692,109,364,2048,5856,3785,4266,10909,3890,522,991,2265,765,6110,3226,2276,4204,1295,509,7734,495,1150,1093,2885,9480,2995,6850,415,5780,1642,1407,2129,1330,1684,13,1632,1610,1634,1,2562,2,1838,303,892,6147,5903,200,1240,426,1517,4,442,14,1966,1365,804,1148,3,37,3132,172,119,204,68,71,2235,2108,71,65,1,552,330,375,2,1945,124,45,893,125,1,728,773,218,970,514,102,5,143,441,578,3591,36,127,562,4,881,30,106,209,114,7,62,204,89,1,181,306,955,23,151,120,256,253,179,595,178,2,14,3,36,43,576,196,1624,46,1,25,5206813,2,70,415,147,5993858,2799834,4589,3311,141,795,19735,1,303,44,5007,30,21,20,3,10,35,5,3,6,14,3,7,2,41,76,25,1,23945175,4042143,1964,16672,2894,6250,14712,427,601,1326,399,714,1559604,34357,23578248,538,31,103,554,435,69,1017,1,265,149,659,2,86,115,147,539,143,2,1012,711,398,182,700,2286,345,475,29,386',kBL:'WWhe',kOPI:89978449};google.sn='webhp';google.kHL='en';})();(function(){
var e=this||self;var g,h=[];function k(a){for(var c;a&&(!a.getAttribute||!(c=a.getAttribute("eid")));)a=a.parentNode;return c||g}function l(a){for(var c=null;a&&(!a.getAttribute||!(c=a.getAttribute("leid")));)a=a.parentNode;return c}function m(a){/^http:/i.test(a)&&"https:"===window.location.protocol&&(google.ml&&google.ml(Error("a"),!1,{src:a,glmm:1}),a="");return a}
function p(a,c,b,f){var d="";-1===c.search("&ei=")&&(d="&ei="+k(b),-1===c.search("&lei=")&&(b=l(b))&&(d+="&lei="+b));b="";e._cshid&&-1===c.search("&cshid=")&&"slh"!==a&&(b="&cshid="+e._cshid);return"/"+(f||"gen_204")+"?atyp=i&ct="+String(a)+"&cad="+(c+d)+"&zx="+String(Date.now())+b};g=google.kEI;google.getEI=k;google.getLEI=l;google.ml=function(){return null};google.log=function(a,c,b,f,d){b||(b=p(a,c,f,d));if(b=m(b)){a=new Image;var n=h.length;h[n]=a;a.onerror=a.onload=a.onabort=function(){delete h[n]};a.src=b}};google.logUrl=function(a){return p("",a)};}).call(this);(function(){google.y={};google.sy=[];google.x=function(a,b){if(a)var c=a.id;else{do c=Math.random();while(google.y[c])}google.y[c]=[a,b];return!1};google.sx=function(a){google.sy.push(a)};google.lm=[];google.plm=function(a){google.lm.push.apply(google.lm,a)};google.lq=[];google.load=function(a,b,c){google.lq.push([[a],b,c])};google.loadAll=function(a,b){google.lq.push([a,b])};google.bx=!1;google.lx=function(){};}).call(this);google.f={};(function(){
</style><style>body,td,a,p,.h{font-family:arial,sans-serif}body{margin:0;overflow-y:scroll}#gog{padding:3px 8px 0}td{line-height:.8em}.gac_m td{line-height:17px}form{margin-bottom:20px}.h{color:#1558d6}em{font-weight:bold;font-style:normal}.lst{height:25px;width:496px}.gsfi,.lst{font:18px arial,sans-serif}.gsfs{font:17px arial,sans-serif}.ds{display:inline-box;display:inline-block;margin:3px 0 4px;margin-left:4px}input{font-family:inherit}body{background:#fff;color:#000}a{color:#4b11a8;text-decoration:none}a:hover,a:active{text-decoration:underline}.fl a{color:#1558d6}a:visited{color:#4b11a8}.sblc{padding-top:5px}.sblc a{display:block;margin:2px 0;margin-left:13px;font-size:11px}.lsbb{background:#f8f9fa;border:solid 1px;border-color:#dadce0 #70757a #70757a #dadce0;height:30px}.lsbb{display:block}#WqQANb a{display:inline-block;margin:0 12px}.lsb{background:url(/images/nav_logo229.png) 0 -261px repeat-x;border:none;color:#000;cursor:pointer;height:30px;margin:0;outline:0;font:15px arial,sans-serif;vertical-align:top}.lsb:active{background:#dadce0}.lst:focus{outline:none}</style><script nonce="sVkp7jIK8JntD0iWAfSxFw">(function(){window.google.erd={jsr:1,bv:1781,de:true};
var h=this||self;var k,l=null!=(k=h.mei)?k:1,n,p=null!=(n=h.sdo)?n:!0,q=0,r,t=google.erd,v=t.jsr;google.ml=function(a,b,d,m,e){e=void 0===e?2:e;b&&(r=a&&a.message);if(google.dl)return google.dl(a,e,d),null;if(0>v){window.console&&console.error(a,d);if(-2===v)throw a;b=!1}else b=!a||!a.message||"Error loading script"===a.message||q>=l&&!m?!1:!0;if(!b)return null;q++;d=d||{};b=encodeURIComponent;var c="/gen_204?atyp=i&ei="+b(google.kEI);google.kEXPI&&(c+="&jexpid="+b(google.kEXPI));c+="&srcpg="+b(google.sn)+"&jsr="+b(t.jsr)+"&bver="+b(t.bv);var f=a.lineNumber;void 0!==f&&(c+="&line="+f);var g=
a.fileName;g&&(0<g.indexOf("-extension:/")&&(e=3),c+="&script="+b(g),f&&g===window.location.href&&(f=document.documentElement.outerHTML.split("\n")[f],c+="&cad="+b(f?f.substring(0,300):"No script found.")));c+="&jsel="+e;for(var u in d)c+="&",c+=b(u),c+="=",c+=b(d[u]);c=c+"&emsg="+b(a.name+": "+a.message);c=c+"&jsst="+b(a.stack||"N/A");12288<=c.length&&(c=c.substr(0,12288));a=c;m||google.log(0,"",a);return a};window.onerror=function(a,b,d,m,e){r!==a&&(a=e instanceof Error?e:Error(a),void 0===d||"lineNumber"in a||(a.lineNumber=d),void 0===b||"fileName"in a||(a.fileName=b),google.ml(a,!1,void 0,!1,"SyntaxError"===a.name||"SyntaxError"===a.message.substring(0,11)||-1!==a.message.indexOf("Script error")?3:0));r=null;p&&q>=l&&(window.onerror=null)};})();</script></head><body bgcolor="#fff"><script nonce="sVkp7jIK8JntD0iWAfSxFw">(function(){var src='/images/nav_logo229.png';var iesg=false;document.body.onload = function(){window.n && window.n();if (document.images){new Image().src=src;}
})();</script><div id="mngb"><div id=gbar><nobr><b class=gb1>Search</b> <a class=gb1 href="http://www.google.com/imghp?hl=en&tab=wi">Images</a> <a class=gb1 href="http://maps.google.com/maps?hl=en&tab=wl">Maps</a> <a class=gb1 href="https://play.google.com/?hl=en&tab=w8">Play</a> <a class=gb1 href="https://www.youtube.com/?tab=w1">YouTube</a> <a class=gb1 href="https://news.google.com/?tab=wn">News</a> <a class=gb1 href="https://mail.google.com/mail/?tab=wm">Gmail</a> <a class=gb1 href="https://drive.google.com/?tab=wo">Drive</a> <a class=gb1 style="text-decoration:none" href="https://www.google.com/intl/en/about/products?tab=wh"><u>More</u> &raquo;</a></nobr></div><div id=guser width=100%><nobr><span id=gbn class=gbi></span><span id=gbf class=gbf></span><span id=gbe></span><a href="http://www.google.com/history/optout?hl=en" class=gb4>Web History</a> | <a  href="/preferences?hl=en" class=gb4>Settings</a> | <a target=_top id=gb_70 href="https://accounts.google.com/ServiceLogin?hl=en&passive=true&continue=http://www.google.com/&ec=GAZAAQ" class=gb4>Sign in</a></nobr></div><div class=gbh style=left:0></div><div class=gbh style=right:0></div></div><center><br clear="all" id="lgpd"><div id="lga"><img alt="Google" height="92" src="/images/branding/googlelogo/1x/googlelogo_white_background_color_272x92dp.png" style="padding:28px 0 14px" width="272" id="hplogo"><br><br></div><form action="/search" name="f"><table cellpadding="0" cellspacing="0"><tr valign="top"><td width="25%">&nbsp;</td><td align="center" nowrap=""><input name="ie" value="ISO-8859-1" type="hidden"><input value="en" name="hl" type="hidden"><input name="source" type="hidden" value="hp"><input name="biw" type="hidden"><input name="bih" type="hidden"><div class="ds" style="height:32px;margin:4px 0"><input class="lst" style="margin:0;padding:5px 8px 0 6px;vertical-align:top;color:#000" autocomplete="off" value="" title="Google Search" maxlength="2048" name="q" size="57"></div><br style="line-height:0"><span class="ds"><span class="lsbb"><input class="lsb" value="Google Search" name="btnG" type="submit"></span></span><span class="ds"><span class="lsbb"><input class="lsb" id="tsuid_1" value="I'm Feeling Lucky" name="btnI" type="submit"><script nonce="sVkp7jIK8JntD0iWAfSxFw">(function(){var id='tsuid_1';document.getElementById(id).onclick = function(){if (this.form.q.value){this.checked = 1;if (this.form.iflsig)this.form.iflsig.disabled = false;}
else top.location='/doodles/';};})();</script><input value="AOEireoAAAAAZEZ8xcw1xGsPSeDYI_9duW9e2iOOyD3C" name="iflsig" type="hidden"></span></span></td><td class="fl sblc" align="left" nowrap="" width="25%"><a href="/advanced_search?hl=en&amp;authuser=0">Advanced search</a></td></tr></table><input id="gbv" name="gbv" type="hidden" value="1"><script nonce="sVkp7jIK8JntD0iWAfSxFw">(function(){var a,b="1";if(document&&document.getElementById)if("undefined"!=typeof XMLHttpRequest)b="2";else if("undefined"!=typeof ActiveXObject){var c,d,e=["MSXML2.XMLHTTP.6.0","MSXML2.XMLHTTP.3.0","MSXML2.XMLHTTP","Microsoft.XMLHTTP"];for(c=0;d=e[c++];)try{new ActiveXObject(d),b="2"}catch(h){}}a=b;if("2"==a&&-1==location.search.indexOf("&gbv=2")){var f=google.gbvu,g=document.getElementById("gbv");g&&(g.value=a);f&&window.setTimeout(function(){location.href=f},0)};}).call(this);</script></form><div id="gac_scont"></div><div style="font-size:83%;min-height:3.5em"><br><div id="prm"><style>.szppmdbYutt__middle-slot-promo{font-size:small;margin-bottom:32px}.szppmdbYutt__middle-slot-promo a.ZIeIlb{display:inline-block;text-decoration:none}.szppmdbYutt__middle-slot-promo img{border:none;margin-right:5px;vertical-align:middle}</style><div class="szppmdbYutt__middle-slot-promo" data-ved="0ahUKEwi_tbu2u8L-AhVUE1kFHbndC9AQnIcBCAQ"><a class="NKcBbd" href="https://www.google.com/url?q=https://artsandculture.google.com/experiment/zgFx1tMqeIZyTw%3Futm_source%3Dgoogle%26utm_medium%3Dhppromo%26utm_campaign%3Dcallinginourcorals&amp;source=hpp&amp;id=19034922&amp;ct=3&amp;usg=AOvVaw0nMWsnMoeASDuSYrKnPMNj&amp;sa=X&amp;ved=0ahUKEwi_tbu2u8L-AhVUE1kFHbndC9AQ8IcBCAU" rel="nofollow">Learn how to help restore coral reefs, simply by listening</a></div></div></div><span id="footer"><div style="font-size:10pt"><div style="margin:19px auto;text-align:center" id="WqQANb"><a href="/intl/en/ads/">Advertising</a><a href="/services/">Business Solutions</a><a href="/intl/en/about.html">About Google</a></div></div><p style="font-size:8pt;color:#70757a">&copy; 2023 - <a href="/intl/en/policies/privacy/">Privacy</a> - <a href="/intl/en/policies/terms/">Terms</a></p></span></center><script nonce="sVkp7jIK8JntD0iWAfSxFw">(function(){window.google.cdo={height:757,width:1440};(function(){var a=window.innerWidth,b=window.innerHeight;if(!a||!b){var c=window.document,d="CSS1Compat"==c.compatMode?c.documentElement:c.body;a=d.clientWidth;b=d.clientHeight}a&&b&&(a!=google.cdo.width||b!=google.cdo.height)&&google.log("","","/client_204?&atyp=i&biw="+a+"&bih="+b+"&ei="+googl.kEI);}).call(this);})();</script> <script nonce="sVkp7jIK8JntD0iWAfSxFw">(function()google.xjs={ck:'xjs.hp.cZMjK1rN2dw.L.X.O',cs:'ACT90oGdWgvp7b-1i002ub8NTEiqmwqPag',excm:[]};})();</script>  <script nonce="sVkp7jIK8JntD0iWAfSxFw">(function(){var u='/xjs/_/js/k\x3dxjs.hp.en.qkDX73W2TvU.O/am\x3dAAAAOgEAFABY/d\x3d1/ed\x3d1/rs\x3dACT90oFpp8_uyj9hwoAl3W3tvYwd1PFWOg/m\x3dsb_he,d';var amd=0;
function p(){var c=u,g=function(){};google.lx=google.stvsc?g:function(){google.timers&&google.timers.load&&google.tick&&google.tick("load","xjsls");var a=document;var b="SCRIPT";"application/xhtml+xml"===a.contentType&&(b=b.toLowerCase());b=a.createElement(b);a=null===c?"null":void 0===c?"undefined":c;if(void 0===h){var d=null;var m=e.trustedTypes;if(m&&m.createPolicy){try{d=m.createPolicy("goog#html",{createHTML:f,createScript:f,createScriptURL:f})}catch(r){e.console&&e.console.error(r.message)}h=
d}else h=d}a=(d=h)?d.createScriptURL(a):a;a=new n(a,l);b.src=a instanceof n&&a.constructor===n?a.g:"type_error:TrustedResourceUrl";var k,q;(k=(a=null==(q=(k=(b.ownerDocument&&b.ownerDocument.defaultView||window).document).querySelector)?void 0:q.call(k,"script[nonce]"))?a.nonce||a.getAttribute("nonce")||"":"")&&b.setAttribute("nonce",k);document.body.appendChild(b);google.psa=!0;google.lx=g};google.bx||google.lx()};googl.xjsu=u;e._F_jsUrl=u;setTimeout(function(){0<amd?google.caft(function(){return p()},amd):p()},0);})();window._ = window._ || {};window._DumpException = _._DumpException = function(e){throw e;};window._s = window._s || {};_s._DumpException = _._DumpException;window._qs = window._qs || {};_qs._DumpException = _._DumpException;function _F_installCss(c){}
(function(){google.jl={blt:'none',chnk:0,dw:false,dwu:true,emtn:0,end:0,ico:false,ikb:0,ine:false,injs:'none',injt:0,injth:0,injv2:false,lls:'default',pdt:0,rep:0,snet:true,strt:0,ubm:false,uwp:true};})();(function(){var pmc='{\x22d\x22:{},\x22sb_he\x22:{\x22agen\x22:true,\x22cgen\x22:true,\x22client\x22:\x22heirloom-hp\x22,\x22dh\x22:true,\x22ds\x22:\x22\x22,\x22fl\x22:true,\x22host\x22:\x22google.com\x22,\x22jsonp\x22:true,\x22msgs\x22:{\x22cibl\x22:\x22Clear Search\x22,\x22dym\x22:\x22Did you mean:\x22,\x22lcky\x22:\x22I\\u0026#39;m Feeling Lucky\x22,\x22lml\x22:\x22Learn more\x22,\x22psrc\x22:\x22This search was removed from your \\u003Ca href\x3d\\\x22/history\\\x22\\u003EWeb History\\u003C/a\\u003E\x22,\x22psrl\x22:\x22Remove\x22,\x22sbit\x22:\x22Search by image\x22,\x22srch\x22:\x22Google Search\x22},\x22ovr\x22:{},\x22pq\x22:\x22\x22,\x22rfs\x22:[],\x22sbas\x22:\x220 3px 8px 0 rgba(0,0,0,0.2),0 0 0 1px rgba(0,0,0,0.08)\x22,\x22stok\x22:\x22F0z49lad-SyDvIsvu43ud0V1__U\x22}}';google.pmc=JSON.parse(pmc);})();(function(){
100 17232    0 17232    0     0   311k      0 --:--:-- --:--:-- --:--:--  317k
var b=function(a){var c=0;return function(){return c<a.length?{done:!1,value:a[c++]}:{done:!0}}},e=this||self;var g,h;a:{for(var k=["CLOSURE_FLAGS"],l=e,n=0;n<k.length;n++)if(l=l[k[n]],null==l){h=null;break a}h=l}var p=h&&h[610401301];g=null!=p?p:!1;var q,r=e.navigator;q=r?r.userAgentData||null:null;function t(a){return g?q?q.brands.some(function(c){return(c=c.brand)&&-1!=c.indexOf(a)}):!1:!1}function u(a){var c;a:{if(c=e.navigator)if(c=c.userAgent)break a;c=""}return-1!=c.indexOf(a)};function v(){return g?!!q&&0<q.brands.length:!1}function w(){return u("Safari")&&!(x()||(v()?0:u("Coast"))||(v()?0:u("Opera"))||(v()?0:u("Edge"))||(v()?t("Microsoft Edge"):u("Edg/"))||(v()?t("Opera"):u("OPR"))||u("Firefox")||u("FxiOS")||u("Silk")||u("Android"))}function x(){return v()?t("Chromium"):(u("Chrome")||u("CriOS"))&&!(v()?0:u("Edge"))||u("Silk")}function y(){return u("Android")&&!(x()||u("Firefox")||u("FxiOS")||(v()?0:u("Opera"))||u("Silk"))};var z=v()?!1:u("Trident")||u("MSIE");y();x();w();var A=!z&&!w(),D=function(a){if(/-[a-z]/.test("ved"))return null;if(A&&a.dataset){if(y()&&!("ved"in a.dataset))return null;a=a.dataset.ved;return void 0===a?null:a}return a.getAttribute("data-"+"ved".replace(/([A-Z])/g,"-$1").toLowerCase())};var E=[],F=null;function G(a){a=a.target;var c=performance.now(),f=[],H=f.concat,d=E;if(!(d instanceof Array)){var m="undefined"!=typeof Symbol&&Symbol.iterator&&d[Symbol.iterator];if(m)d=m.call(d);else if("number"==typeof d.length)d={next:b(d)};else throw Error("a`"+String(d));for(var B=[];!(m=d.next()).done;)B.push(m.value);d=B}E=H.call(f,d,[c]);if(a&&a instanceof HTMLElement)if(a===F){if(c=4<=E.length)c=5>(E[E.length-1]-E[E.length-4])/1E3;if(c){c=google.getEI(a);a.hasAttribute("data-ved")?f=a?D(a)||"":"":f=(f=
a.closest("[data-ved]"))?D(f)||"":"";f=f||"";if(a.hasAttribute("jsname"))a=a.getAttribute("jsname");else{var C;a=null==(C=a.closest("[jsname]"))?void 0:C.getAttribute("jsname")}google.log("rcm","&ei="+c+"&ved="+f+"&jsname="+(a||""))}}else F=a,E=[c]}window.document.addEventListener("DOMContentLoaded",function(){document.body.addEventListener("click",G)});}).call(this);</script></body></html>
```
~~~

#### 💬 If this works, you've successfully changed the order your system resolves names by editing `/etc/nsswitch.conf`

# Look at you, learning Linux 🐧! You looked at you DNS tools to find resources and then change the system so that it looks in different areas first

