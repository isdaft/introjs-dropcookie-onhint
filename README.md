# introjs-dropcookie-onhint
drop a cookie when hint is clicked to hide after viewed

# Get intro.js v2 
https://github.com/usablica/intro.js

# Modify Intro.js core file @ Line 1458
Just copy the below text over 1458 and down

## Updates
-add randomized string to each cookie name so that they are not replaced

##Example Usage HTML/JS

```
function checkCookieIntro(){
            var keyValuePairs = document.cookie.split(';');
            //console.log(keyValuePairs);
            for(var i = 0; i < keyValuePairs.length; i++) {
            	if (keyValuePairs[i].match(/=.*=/)) { // Check if there are 2 equals
    			keyValuePairs[i] = keyValuePairs[i].replace('=', ''); // Remove the first one
				}
                var name = keyValuePairs[i].substring(0, keyValuePairs[i].indexOf('='));
                var value = keyValuePairs[i].substring(keyValuePairs[i].indexOf('=')+1);
                var locate = window.location.href.split("/").pop();
                
                var name_check = "WebsiteProgram_" + locate;
                name_check = name_check.replace('=', '');
                //console.log("Name: " + name);
                //console.log("Value: " + value);
                //console.log("Locate: " + locate);
                //console.log("name_check: " + name_check);
                //console.log("right before indexof");
                if (name.indexOf(name_check) >= 0) {
                  
                    if (document.body.querySelector('.introjs-hint[data-step="' + value + '"]') != null) {
                        document.body.querySelector('.introjs-hint[data-step="' + value + '"]').classList.add('introjs-hidehint');
                    }
                }
            }
        }
```

## Replace Code Line 1458 (or that general region :P)

```
    var closeButton = document.createElement('a');
    closeButton.className = 'introjs-button';
    closeButton.innerHTML = this._options.hintButtonLabel;
    closeButton.onclick = console.log("button closed, stepid: " + stepId);
    closeButton.onclick = hintClickDropCookie(stepId);
    closeButton.onclick = _hideHint.bind(this, stepId);
    
    function hintClickDropCookie(step_Id) {
      
      function randomString(length, chars) {
      	var result = '';
    	for (var i = length; i > 0; --i) result += chars[Math.floor(Math.random() * chars.length)];
		 return result;
	  }
      var rString = randomString(4, '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ');
      
      var cookiePrefix = "ProgramHintNumbers_";
      cookiePrefix = cookiePrefix + step_Id;
      function setCookie(c_name,value,exdays, ra){
        //var exdate=new Date(); //code for an exp date
        //exdate.setDate(exdate.getDate() + exdays);
        //var c_value=escape(value) + ((exdays==null) ? "" : "; expires="+exdate.toUTCString());
        document.cookie=ra + "_" + c_name + "=" + step_Id;
        
      }
    
      setCookie(cookiePrefix, "1",90, rString);
      
      //console.log("cookie set for hint: " + cookiePrefix);
      
      
    }
```
