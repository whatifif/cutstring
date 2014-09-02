## JQuery Plugin: cutstring ##

## This plugin enables multibyte string such as utf-8 to be cut cleanly at the length of your choice.##




    /*
    * jQuery.fn.cutString( options);
    *
    * Cut and set the string of jQuery object to the size of options.length.
    * This is useful to cut the multibyte string (UTF8)without breaking the char at the end.
    * The sizes of the cut strings look similar even though ASCII and multibytes are mixed.
    *
    * $('.element').cutString({length:20, ellipsisText: '...'});
    *
    * Version 1.0.0
    * */
    
    
    Code Download code
    
    (function($){
    $.fn.cutString=function(options){
	    var defaults = {  
    			   length: 20,  
    			   ellipsisText: "..."  
    			  };  
    	  
    	var options = $.extend(defaults, options);  
    	return this.each(function(){
    		   obj = $(this);  
    		   var str = obj.html().trim(),
    			   strLen=str.length,
    			   optLen=options.length,
    			   len=0;
    		  function cut(){
    	for (var i=0; i < strLen; i++) {
    	len += (str.charCodeAt(i) > 128) ? 2 : 1;
    	if (len > optLen) return str.substring(0,i) + options.ellipsisText;
    	}
    			   return str;
    		  }   
    		   obj.html(cut());   
    	});
	
    };
    })(jQuery);


## Simple usage 1 ##
**HTML**


    some long string mixed with ASCII and multibytes like Korean, Chinese, Japanese
    
    another long string mixed with ASCII and multibytes 한글은 과학적이고 아름다운 소리글자입니다.
    
    한글은 과학적이고 아름다운 소리글자입니다. another long string. 
 

**jQuery**


    $('div').cutString({length:20});

**Return**

20 characters remain and the rests are cut off from the original string.
Result


    some long string mix...
    
    another long string ...
    
    한글은 과학적이고 아...
 



## Simple usage 2 ##
**HTML**

    some long string mixed with ASCII and multibytes like Korean, Chinese, Japanese
    
    another long string mixed with ASCII and multibytes 한글은 과학적이고 아름다운 소리글자입니다.
    
    한글은 과학적이고 아름다운 소리글자입니다. another long string. 
 

**jQuery**


    $('div').cutString({length:20, ellipsisText:'-more'});

**Return**

20 characters remain and the rests are cut off from the original string. New ellipsisText is attached.

    some long string mix-more
    
    another long string -more
    
    한글은 과학적이고 아-more
 




