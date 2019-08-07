<template>
	<view class="content">
		<image src="../../static/g1.gif" mode="widthFix"></image>
		<text class="title">越宝宝，想我了吗？</text>
		<view class="operate">
			<button type="primary" class="btn" @tap="agree">想呀</button>
			<button type="warn" class="btn" @tap="disagree">不想</button>
		</view>
		<view class="message" v-for="one in love" :key="one">{{one}}</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				love:[],
				timer:{},
				loveed:{
					0:{
						"content": '越宝贝，我也非常想你，每年都想给你过不一样的七夕节，喜欢今年的七夕节礼物吗？',
						"cancelText": "不喜欢",
						"confirmText": "喜欢"
					},
					1:{
						"content": '越宝贝，两个人相伴一起走过的每个七夕节，你还记得吗？',
						"cancelText": "不记得",
						"confirmText": "记得"
					},
					2:{
						"content": '还记得咱们从相遇，相识，相知，到相爱的种种回忆吗？',
						"cancelText": "不记得",
						"confirmText": "记得"
					},
					3:{
						"content": '越宝贝，是不是我平时会让你生气？',
						"cancelText": "不是",
						"confirmText": "是的"
					},
					4:{
						"content": '气的你让我给你写检查，但是，你心里却不是这样想的，对吧？',
						"cancelText": "不对",
						"confirmText": "嗯嗯"
					},
					5:{
						"content": '我知道，你其实就是想让我为你而变得更好。',
						"cancelText": "才不是",
						"confirmText": "知道就好"
					},
					6:{
						"content": '为了让我能够更加爱你。',
						"cancelText": "想多了",
						"confirmText": "对的"
					},
					7:{
						"content": '为了让我能够成为你一辈子依靠的那个男孩。',
						"cancelText": "呵呵",
						"confirmText": "么么"
					},
					8:{
						"content": '为了你，我一定会更加努力，为了咱们的明天而奋斗！',
						"cancelText": "别了",
						"confirmText": "爱你"
					},
					9:{
						"content": '所以，你愿意一直一直陪我走下去吗?',
						"cancelText": "考虑一下",
						"confirmText": "愿意"
					},
				}
			}
		},
		onLoad() {
			this.back = uni.getBackgroundAudioManager();
			this.back.src = "http://140.143.132.225/love/pdd.mp3";
			this.back.title = "music";
			this.back.play();
		},
		onShow(){
			this.love = [];
			this.timer = {};
			let msg = {
				1000:"赵越，我爱你！",
				2000: "趙越，我愛你！（繁体）",
				3000: "Zhao Yue, I love you! (英语)",
				4000: "趙越、私はあなたを愛してる！(日语)",
				5000: "Zhao Yue, ich liebe dich! (德语)",
				6000: "Чжао Юэ, я люблю тебя! (俄语)",
				7000: "Zhao Yue, ti amo! (意大利语)",
				8000: "Zhao Yue, te amo! (西班牙语)",
				9000: "Zhao Yue, 너를 사랑해! (韩语)",
				10000: "Zhao Yue, jeg elsker dig! (丹麦语)",
				11000: "Zhao Yue, σε αγαπώ! (希腊语)",
				12000: "Zhao Yue, të dua! (阿尔巴尼亚语)",
				13000: "تشاو يوي ، أنا أحبك! (阿拉伯语)",
				14000: "Oዎ አዎ ፣ እወድሻለሁ! (阿姆哈拉语)",
				15000: "Zhao Yue, səni sevirəm! (阿塞拜疆语)",
				16000: "Zhao Yue, is breá liom tú! (爱尔兰语)",
				17000: "Zhao Yue, ma armastan sind! (爱沙尼亚语)",
				18000: "Zhao Yue, maite zaitut! (巴斯克语)",
				19000: "Чжао Юэ, я люблю цябе! (白俄罗斯语)",
				20000: "Джао Юе, обичам те! (保加利亚语)",
				21000: "Zhao Yue, kocham cię! (波兰语)",
				22000: "Zhao Yue, volim te! (波斯尼亚语)",
				23000: "ژائو یو ، من تو را دوست دارم! (波斯语)",
				24000: "Zhao Yue, ek is lief vir jou! (布尔语)",
				25000: "Zhao Yue, jeg elsker dig! (丹麦语)",
				26000: "Zhao Yue, je t'aime! (法语)",
				27000: "Zhao Yue, mahal kita! (菲律宾语)",
				28000: "Zhao Yue, rakastan sinua! (芬兰语)",
				29000: "Zhao Yue, ik hâld fan dy! (弗里西语)",
				30000: "ចាវយូខ្ញុំស្រឡាញ់អ្នកណាស់! (高棉语)",
				31000: "ჟოო იუ, მიყვარხარ! (格鲁吉亚语)",
				32000: "ઝાઓ યૂ, હું તમને પ્રેમ કરું છું! (古吉拉特语)",
				33000: "Чжао Юэ, мен сені жақсы көремін! (海地克里奥尔语)",
				34000: "Zhao Yue, ina son ku! (豪萨语)",
				35000: "Zhao Yue, ik hou van je! (荷兰语)",
				36000: "Жао Юе, мен сени сүйөм! (吉尔吉斯语)",
				37000: "Zhao Yue, te amo! (加利西亚语)",
				38000: "Zhao Yue, t'estimo! (加泰罗尼亚语)",
				39000: "Zhao Yue, miluji tě! (捷克语)",
				40000: "Ha ಾವೋ ಯು, ನಾನು ನಿನ್ನನ್ನು ಪ್ರೀತಿಸುತ್ತೇನೆ! (卡纳达语)",
				41000: "Zhao Yue, ti tengu caru! (科西嘉语)",
				42000: "Zhao Yue, volim te! (克罗地亚语)",
				43000: "Zhao Yue, ez ji te hez dikim! (库尔德语)",
				44000: "Zhao Yue, te amo! (拉丁语)",
				45000: "Zhao Yue, es tevi mīlu! (拉脱维亚语)",
				46000: "Zhao Yue, ຂ້ອຍຮັກເຈົ້າ! (老挝语)",
				47000: "Zhao Yue, aš tave myliu! (立陶宛语)",
				48000: "Zhao Yue, ech hunn dech gär! (卢森堡语)",
				49000: "Zhao Yue, te iubesc! (罗马尼亚语)",
				50000: "Zhao Yue, tiako ianao! (马尔加什语)",
				51000: "Zhao Yue, inħobbok! (马耳他语)",
				52000: "झाओ यू, मी तुझ्यावर प्रेम करतो! (马拉地语)",
				53000: "ഷാവോ യു, ഞാൻ നിന്നെ സ്നേഹിക്കുന്നു! (马拉雅拉姆语)",
				54000: "Zhao Yue, saya sayang kamu! (马来语)",
				55000: "Haао Јуе, те сакам! (马其顿语)",
				56000: "Zhao Yue, Aroha ahau ki a koe! (毛利语)",
				57000: "Жао Юэ, би чамд хайртай! (蒙古语)",
				58000: "ঝাও ইউ, আমি তোমাকে ভালবাসি! (孟加拉语)",
				59000: "Zhao နှင့် Yue, သင်တို့ကိုငါခစျြ! (缅甸语)",
				60000: "Zhao Yue, kuv hlub koj! (苗语)",
				61000: "Zhao Yue, ndiyakuthanda! (南非科萨语)",
				62000: "Zhao Yue, ngiyakuthanda! (南非祖鲁语)",
				63000: "झाओ यू, म तिमीलाई माया गर्छु! (尼泊尔语)",
				64000: "Zhao Yue, jeg elsker deg! (挪威语)",
				65000: "ਜ਼ਾਓ ਯੂ, ਮੈਂ ਤੁਹਾਨੂੰ ਪਿਆਰ ਕਰਦਾ ਹਾਂ! (旁遮普语)",
				66000: "Zhao Yue, eu te amo! (葡萄牙语)",
				67000: "ژو یو ، زه تاسو سره مینه لرم! (普什图语)",
				68000: "Zhao Yue, ndimakukondani! (齐切瓦语)",
				69000: "Zhao Yue, jag älskar dig! (瑞典语)",
				70000: "Zhao Yue, ou te alofa ia te oe! (萨摩亚语)",
				71000: "Зхао Иуе, волим те! (塞尔维亚语)",
				72000: "Zhao Yue, kea u rata! (塞索托语)",
				73000: "ෂාඕ යූ, මම ඔයාට ආදරෙයි! (僧伽罗语)",
				74000: "Zhao Yue, mi amas vin! (世界语)",
				75000: "Zhao Yue, milujem ťa! (斯洛伐克语)",
				76000: "Zhao Yue, ljubim te! (斯洛文尼亚语)",
				77000: "Zhao Yue, nakupenda! (斯瓦西里语)",
				78000: "Zhao Yue, tha gaol agam ort! (苏格兰盖尔语)",
				79000: "Zhao Yue, gihigugma ko ikaw! (宿务语)",
				80000: "Zhao Yue, waan ku jeclahay! (索马里语)",
				81000: "Чжао Юе, ман туро дӯст медорам! (塔吉克语)",
				82000: "జావో యు, నేను నిన్ను ప్రేమిస్తున్నాను! (泰卢固语)",
				83000: "ஜாவோ யூ, ஐ லவ் யூ! (泰米尔语)",
				84000: "จ่าวหยูฉันรักคุณ! (泰语)",
				85000: "Zhao Yue, seni seviyorum! (土耳其语)",
				86000: "Zhao Yue, dwi'n dy garu di! (威尔士语)",
				87000: "زاؤ یو ، میں تم سے پیار کرتا ہوں! (乌尔都语)",
				88000: "Чжао Юе, я люблю тебе! (乌克兰语)",
				89000: "Zhao Yue, men seni yaxshi ko'raman! (乌兹别克语)",
				90000: "ג'או יו, אני אוהב אותך! (希伯来语)",
				91000: "Zhao Yue, Aloha wau iā ʻoe! (夏威夷语)",
				92000: "جيء يار، مون کي توسان پيار آهي! (信德语)",
				93000: "Zhao Yue, szeretlek! (匈牙利语)",
				94000: "Zhao Yue, ndinokuda! (修纳语)",
				95000: "Zhao Yue, ես սիրում եմ քեզ: (亚美尼亚语)",
				96000: "Zhao Yue, ahụrụ m gị n'anya! (伊博语)",
				97000: "דזשאַו יו, איך ליבע איר! (意第绪语)",
				98000: "झाओ यू, आई लव यू! (印地语)",
				99000: "Zhao Yue, Abdi bogoh ka anjeun! (印尼巽他语)",
				100000: "Zhao Yue, aku mencintaimu! (印尼语)",
				101000: "Zhao Yue, aku tresna sampeyan! (印尼爪哇语)",
				102000: "Zhao Yue, Mo nifẹ rẹ! (约鲁巴语)",
				103000: "Triệu Nguyệt, anh yêu em! (越南语)",
				104000: "Zhao Yue, ég elska þig! (冰岛语)",
			};
			let ref = this;
			for(let key in msg){
				let t= setTimeout(() => {
					ref.love.push(msg[key]);
					delete ref.timer[key];
				},key);
				ref.timer[key] = t;
			}
		},
		onHide(){
			for(let key in this.timer){
				clearTimeout(this.timer[key]);
			}
		},
		methods: {
			agree: function(){
				let _this = this;
				let flag = 0;
				_this.youAndMe(_this,flag);				
			},
			youAndMe:function(_this,flag){
				uni.showModal({
					title: '',
					content: _this.loveed[flag].content,
					showCancel: true,
					cancelText: _this.loveed[flag].cancelText,
					confirmText: _this.loveed[flag].confirmText,
					success: res => {
						if(res.confirm){
							flag = flag + 1;
							if(flag < 9){
								_this.youAndMe(_this,flag);	
							}else{
								uni.showToast({
									icon:'none',
									title: '越宝贝，我就知道你一定会同意的，期待下一年的七夕！',
									duration:4000
								});
							}
						}else{
							_this.mistake();
						}
					}
				});
			},
			disagree: function(){
				this.mistake();
			},
			mistake: function(){
				let _this = this;
				uni.showModal({
					title:"我相信，你肯定是点错了！",
					content:"我再给你一次重新选择的机会！！！",
					showCancel: false,
					cancelText:"",
					confirmText:"么么哒！",
					success:function(res){
						if(res.confirm){
							_this.loveSuccess();
						}
					}
				})
			},
			loveSuccess: function(){
				uni.showToast({
					icon:'none',
					title: '越宝贝，七夕节快乐！',
					duration:4000
				});
			}
		}
	}
</script>

<style lang="less">
	@import url("index.less");
</style>
