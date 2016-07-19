# jQuery-fixed-sideBar

##載入

        <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.0/jquery.min.js"></script>
        <script src="sidefixed.js"></script>
        
##HTML

        <header>
        	<nav class="navigation"></nav>
        </header>
        <div class="container">
        	<div class="mainContainer">
        		<div class="mainContent">
        			(1)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<br><br>
        			(2)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<br><br>
        			(3)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<br><br>
        			(4)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<br><br>
        			(5)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<br><br>
        			(6)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<br><br>
        			(7)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<div class="box"></div>
        
        		</div>
        	</div><!--"mainContent-->
        	
        	<div class="sideContainer">
        		<div  class="sideContent">
        			(1)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<br><br>
        			(2)test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text test text 
        			<br><br>

        		</div>	
        	</div>
        	<div style="clear:both"></div>
        </div>		
        <footer></footer>

##CSS

    		html,body{ padding: 0; margin: 0; }
    		header,
    		footer{ max-width: 990px; clear: both;	 margin: 0 auto; height: 100px; background-color: #ccc; }
    		.navigation{ width: 100%; height: 45px; position:fixed; left: 0; top: 0; background-color: #000; z-index: 999;}
    		.container{max-width: 990px; margin: 0  auto; }
    		.mainContainer{width: 74.2%; float: left;margin-top: 10px; margin-bottom: 12px;  box-sizing: border-box; position: relative;}
    		
    		.sideContainer{ float: right; margin: 10px 0 12px 0;  width: 240px; position: relative;}
    		.mainContent{ background: #ddd; width: 100%;height:4000px;}
    		.sideContent{  width:240px;  height:1000px; background-color: #aaa; border-bottom: 1px solid #000;}
    		
    		.article{ padding-bottom:50px;}
    		@media screen and (max-width: 990px){
    			.mainContainer{ width: 100%; height:auto!important;}
    			.sideContainer{display:none; height:auto!important; } 
    		}
##JS

    $(function(){
    	$(".sideContainer").fixedSidebar({ 
    		wrapper:$('.container'),
    		content:$('.sideContent'),
    		fixedNavHeight : 45,
    		responsiveWidth : 768
    	});
    });
