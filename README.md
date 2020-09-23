<div align="center">

## Web Barcode


</div>

### Description

generate code 39 barcodes in html using javascript.
 
### More Info
 
a div/span element id for placement on the page.

the value to encode.

whether include check digit.

height and width of the bars.

Step 1:

Create two, one pixel, gifs (one black, one white) using your favorite paint program. Call them "b.gif" and "w.gif".

Step 2:

Copy the text below from "JS START" to "JS END" into a file called "barcode.js".

Step 3:

Place the two gifs and the .js files in the same directory and create an html file called "test.html" in this directory as well.

Step 4:

Copy the text below from "HTML START" to "HTML END" into the html file.

Step 5:

Open the html file in your favorite browser and input a value to display as a bar code.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Steve Hoyt](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/steve-hoyt.md)
**Level**          |Intermediate
**User Rating**    |4.6 (23 globes from 5 users)
**Compatibility**  |
**Category**       |[Graphics](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics__2-75.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/steve-hoyt-web-barcode__2-3284/archive/master.zip)





### Source Code

```
JS START
function Code39(strDataToEncode, blnAddCheckDigit){
var ary3of9CharSet = new Array(43);
var strChar = "";
var lngCheckDigit = 0;
var lngCharIndex = 0;
var strEncode = "";
var strEncodeFormat = "";
var i = 0;
var j = 0;
var reg = new RegExp("[a-zA-Z0-9\-._\$\/+\%]");
var cstrGuard = "010010100";
var cstrPadd = "0";
var strEncodedString = "";
// numbers 0 to 9
ary3of9CharSet[0] = "000110100";
ary3of9CharSet[1] = "100100001";
ary3of9CharSet[2] = "001100001";
ary3of9CharSet[3] = "101100000";
ary3of9CharSet[4] = "000110001";
ary3of9CharSet[5] = "100110000";
ary3of9CharSet[6] = "001110000";
ary3of9CharSet[7] = "000100101";
ary3of9CharSet[8] = "100100100";
ary3of9CharSet[9] = "001100100";
// letters A to Z
ary3of9CharSet[10] = "100001001";
ary3of9CharSet[11] = "001001001";
ary3of9CharSet[12] = "101001000";
ary3of9CharSet[13] = "000011001";
ary3of9CharSet[14] = "100011000";
ary3of9CharSet[15] = "001011000";
ary3of9CharSet[16] = "000001101";
ary3of9CharSet[17] = "100001100";
ary3of9CharSet[18] = "001001100";
ary3of9CharSet[19] = "000011100";
ary3of9CharSet[20] = "100000011";
ary3of9CharSet[21] = "001000011";
ary3of9CharSet[22] = "101000010";
ary3of9CharSet[23] = "000010011";
ary3of9CharSet[24] = "100010010";
ary3of9CharSet[25] = "001010010";
ary3of9CharSet[26] = "000000111";
ary3of9CharSet[27] = "100000110";
ary3of9CharSet[28] = "001000110";
ary3of9CharSet[29] = "000010110";
ary3of9CharSet[30] = "110000001";
ary3of9CharSet[31] = "011000001";
ary3of9CharSet[32] = "111000000";
ary3of9CharSet[33] = "010010001";
ary3of9CharSet[34] = "110010000";
ary3of9CharSet[35] = "011010000";
// allowed symbols - . _ $ / + %
ary3of9CharSet[36] = "010000101";
ary3of9CharSet[37] = "110000100";
ary3of9CharSet[38] = "011000100";
ary3of9CharSet[39] = "010101000";
ary3of9CharSet[40] = "010100010";
ary3of9CharSet[41] = "010001010";
ary3of9CharSet[42] = "000101010";
// validate data to encode
// replace spaces w/ underscores
// remove all asterisks * (we will add them later)
// force upper case per spec
while (strDataToEncode.indexOf(" ") != -1) strDataToEncode = strDataToEncode.replace(" ", "_");
while (strDataToEncode.indexOf("*") != -1) strDataToEncode = strDataToEncode.replace("*", "");
strDataToEncode = strDataToEncode.toUpperCase();
// encode data using character set
// get the check digit calculation while we're at it
for (i = 0; i < strDataToEncode.length; i++){
strChar = strDataToEncode.substr(i, 1);
if (!reg.test(strChar)){
alert("Invalid Character Specified!");
return "";
}
switch (true){
case strChar == "-": lngCharIndex = 36; break;
case strChar == ".": lngCharIndex = 37; break;
case strChar == "_": lngCharIndex = 38; break;
case strChar == "$": lngCharIndex = 39; break;
case strChar == "/": lngCharIndex = 40; break;
case strChar == "+": lngCharIndex = 41; break;
case strChar == "%": lngCharIndex = 42; break;
case !isNaN(strChar): lngCharIndex = eval(strChar); break;
default: lngCharIndex = strChar.charCodeAt(0) - 55; break;
}
lngCheckDigit += lngCharIndex;
strEncode += ary3of9CharSet[lngCharIndex];
}
// finish the check-digit
lngCheckDigit %= 43;
// should we incorporate the check digit?
if (blnAddCheckDigit != 0) strEncode += ary3of9CharSet[lngCheckDigit];
// add start/stop characters (asterisks "*")
strEncode = cstrGuard + strEncode + cstrGuard;
// now, format the output - the std aspect ratio is 3:1 per spec (used here)
//            - the minimum ratio is 2:1 fyi.
// hint -- the odd/even value of the variable "j" (found by "or-ing" by 1)
// indicates whether a bar or space should be produced. the value (1 or 0) found
// in the string variable "strEncodeFormat" at the location of "j" indicates
// whether the bar/space should be a wide or narrow element in the bar code.
for (i = 0; i < strEncode.length; i += 9){
strEncodeFormat = strEncode.substr(i, 9);
for (j = 0; j < 9; j++){
if ((j & 1) == 1){
strEncodedString += ((strEncodeFormat.substr(j, 1) == 1) ? "000" : "0");
}else{
strEncodedString += ((strEncodeFormat.substr(j, 1) == 1) ? "111" : "1");
}
}
strEncodedString += cstrPadd;
}
return strEncodedString;
}
function DisplayBarcode(div, val, checkdigit, h, w){
var val = Code39(val, checkdigit);
var htm = "";
var bit = 0;
var gif = "";
var lngPtr = 0;
if (isNaN(h)) h = 5;
if (isNaN(w)) w = 1;
if (h < 5) h = 5;
if (w < 1) w = 1;
// get a count of contiguous 1s or 0s until the current value
// being counted changes, then, if the current value is a 1, select the
// single black pixel .gif otherwise use the single white pixel .gif and
// stretch its width to the number of characters counted - not forgetting to account
// for the width of the bars the user has specified. that's it ...
for (lngPtr = 0; lngPtr < val.length; lngPtr++){
bit = eval(val.substr(lngPtr, 1));
intCharacterCount = 1;
if (lngPtr == val.length) break;
while (bit == eval(val.substr(lngPtr + 1, 1))){
intCharacterCount++;
lngPtr++;
if (lngPtr == val.length) break;
}
gif = ((bit == 1) ? "b.gif" : "w.gif");
htm += "<img src\=\"" + gif + "\" style=\"height:'" + h + "'\; width:'" + (w * intCharacterCount) + "'\;\">";
}
document.all[div].innerHTML = htm;
}
JS END
HTML START
<html>
<head>
<title>RenderBar Imaging™ Sample Code</title>
<script type="text/javascript" src="barcode.js"></script>
</head>
<body>
<font style="color:'#000099'; font-family:'Verdana, Tahoma, Arial, Sans-Sarif'; font-size:'12pt'; font-weight:'bold';">
<b>Typing into the text box below</b> and clicking the "Show Barcode" button will generate a new Code 3 of 9 bar code.
<div id="barcode" style="display:'inline'; left:'50'; position:'relative';"></div>
<input name="encode" type="text" style="width:'200';" value="RenderBar" onfocus=this.select()>
<input type="button" value="Show Barcode" onclick="DisplayBarcode('barcode', encode.value, 0, 100, 1);">
</font>
<script language="javascript">
encode.focus();
</script>
</body>
</html>
HTML END
```

