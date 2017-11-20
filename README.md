# LotteryZhuanpan
抽奖大转盘jq

**引入插件**

    `<script src="js/awardRotate.js"></script>`

效果图1：
![](https://i.imgur.com/I7PmLSM.png)
效果图2：
![](https://i.imgur.com/H7nzUzT.gif)

核心代码：

    $(function(){
			var bRotate = false;
			var item = 2;//控制奖品
			var rotateTimeOut = function (){
				$('#rotate').rotate({
					angle:0,
					animateTo:2160,
					duration:8000,
					callback:function (){
						alert('网络超时，请检查您的网络设置！');
					}
				});
			};
			
			var rotateFn = function (awards, angles, txt){
				bRotate = !bRotate;
				$('#rotate').stopRotate();
				$('#rotate').rotate({
					angle:0,
					animateTo:angles+1800,
					duration:8000,
					callback:function (){
						var money = item==0?50:((item==1)?280:600);
						var invest = item==0?1:((item==1)?5:10);
						$(".money").text(money);
						$(".invest").text(invest);
						// alert(txt);
						console.log(txt)
						bRotate = !bRotate;//
					}
				})
			};
			var canclick=3;//控制可抽奖次数
			$('.pointer').click(function (){
				
				if(canclick<1){
					return false;
				}
				console.log(canclick)
				if($(this).hasClass('before')){//控制是否可点击
					return false;
				}
				if($(this).hasClass('end')){//控制是否可点击
					return false;	
				}
				$(this).addClass("aniPause");
				if(bRotate)return;
				//item = rnd(0,3);//取0-3的随机整数
				// item=3;//控制奖品
				switch (item) {
					case 0:
					//var angle = [26, 88, 137, 185, 235, 287, 337];
					rotateFn(0, 0, '迷你月饼');
					break;
					case 1:
					//var angle = [88, 137, 185, 235, 287];
					rotateFn(1, 120, '法式月饼');
					break;
					case 2:
					//var angle = [137, 185, 235, 287];
					rotateFn(2, 240, '冰皮月饼');
					break;
				}
				canclick--;
			});

			function rnd(n, m){
				return Math.floor(Math.random()*(m-n+1)+n)
			}

		})