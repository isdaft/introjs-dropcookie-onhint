# introjs-dropcookie-onhint
drop a cookie when hint is clicked to hide after viewed

# Get intro.js v2 
https://github.com/usablica/intro.js

# Modify Intro.js core file @ Line 1458
Just copy the below text over 1458 and down

```
    var closeButton = document.createElement('a');
    closeButton.className = 'introjs-button';
    closeButton.innerHTML = this._options.hintButtonLabel;
    closeButton.onclick = console.log("button closed, stepid: " + stepId);
    closeButton.onclick = hintClickDropCookie(stepId);
    closeButton.onclick = _hideHint.bind(this, stepId);
    
    function hintClickDropCookie(step_Id) {
      
      var cookiePrefix = "ProgramHintNumbers_";
      cookiePrefix = cookiePrefix + step_Id;
      function setCookie(c_name,value,exdays){
        //var exdate=new Date();
        //exdate.setDate(exdate.getDate() + exdays);
        //var c_value=escape(value) + ((exdays==null) ? "" : "; expires="+exdate.toUTCString());
        document.cookie=c_name + "=" + step_Id;
        
      }
    
      setCookie(cookiePrefix, "1",90);
      
      console.log("cookie set for hint: " + cookiePrefix);
      
      
    }
```
