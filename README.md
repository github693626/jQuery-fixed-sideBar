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

##sidefixed.js

                (function($) {
                	$.fn.extend({
                
                		//側欄跟著捲軸 plugin
                		fixedSidebar: function(options) {
                			var $window = $(window),
                				$this = this;
                				
                
                			$window.load(function() { //等圖片載完確認區塊高度
                				var _navHeight = options['fixedNavHeight'] || 0,
                					_responsiveWidth = options['responsiveWidth'] || 0,
                					lastScrollTop = 0,
                					$container = options['wrapper'],
                					$content = options['content'];
                
                				if($container.length <= 0 || $content.length <= 0 || $window.width() < _responsiveWidth){
                					return;
                				}else{
                					myScroll($this, $content);
                				}
                
                				function myScrollTall(container, content) {
                
                					if (container.height() > content.height() + 100) { //設定100px緩衝
                						var _winST = $window.scrollTop();
                						if (_winST >= lastScrollTop) { //卷軸向下
                							if (_winST >= content.offset().top + content.height() - $window.height()) { //滑到內容底部
                								content.css({
                									'position': 'fixed',
                									'top': 'auto',
                									'bottom': '10px'
                								});
                								scrollFooter(container, content);
                							}
                
                						} else { //卷軸往上 
                
                							if (_winST <= content.offset().top - _navHeight) { //若卷軸往上滑到內容頂部 
                								if (_winST <= container.offset().top - _navHeight) { //若卷軸往上滑到網頁上方
                									content.css({
                										'position': 'static',
                										'top': 'auto',
                										'bottom': 'auto'
                									});
                								} else {
                									content.css({
                										'position': 'absolute',
                										'top': _winST - container.offset().top + _navHeight,
                										'bottom': 'auto'
                									});
                								}
                							} else {
                								content.css({
                									'position': 'absolute',
                									'top': content.offset().top - container.offset().top,
                									'bottom': 'auto'
                								});
                							}
                						}
                						lastScrollTop = _winST;
                
                					} else {
                						content.css({
                							'position': 'static',
                							'top': 'auto',
                							'bottom': 'auto'
                						});
                					}
                				}
                
                				function myScrollShort(container, content) {
                
                					var _winST = $window.scrollTop();
                					if (_winST >= container.offset().top - _navHeight) {
                						content.css({
                							'position': 'absolute',
                							'top': _winST - container.offset().top + _navHeight,
                							'bottom': 'auto'
                						});
                						scrollFooter(container, content);
                					} else {
                						content.css({
                							'position': 'static',
                							'top': 'auto',
                							'bottom': 'auto'
                						});
                					}
                
                				}
                
                				function scrollFooter(container, content) {
                					if (content.offset().top + content.height() >= container.offset().top + container.outerHeight()) {
                
                						content.css({
                							'position': 'absolute',
                							'top': 'auto',
                							'bottom': 0
                						})
                
                						$(document).ajaxComplete(function() {
                							content.css({
                								'position': 'static',
                								'top': 'auto',
                								'bottom': 'auto'
                							});
                							if ( container.offset().top + content.height() > $window.height()) { //內容是否超過window高度
                								myScrollTall(container, content);	//跟著捲軸移動
                							} else {
                								myScrollShort(container, content);  //固定在上方
                							}
                						});
                
                					}
                				}
                
                				function maxHeight(container) {
                					container.css('height', 'auto').css('height', $container.height());
                				}
                
                				function goScroll(container, content) {
                					if ( container.offset().top + content.height() > $window.height()) { //內容是否超過window高度
                						//跟著捲軸移動
                						$window.scroll(function(){
                							myScrollTall(container, content);	
                						});
                					} else {
                						//固定在上方
                						$window.scroll(function(){
                							myScrollShort(container, content);
                						});
                					}
                
                				}
                
                
                				function myScroll(container, content) {
                					
                					maxHeight(container);
                
                					//AJAX	
                					$(document).ajaxComplete(function() {
                						maxHeight(container);
                					});
                
                					container.find('iframe').load(function() {
                						maxHeight(container);
                					});
                
                					//RWD
                					content.width(container.width());
                					$window.resize(function() {
                						content.width(container.width());
                						//goScroll(container, content);	
                
                					});
                
                					goScroll(container, content);
                				
                				}
                			}).scroll();
                
                			return this;
                
                		}
                	});
                })(jQuery);
