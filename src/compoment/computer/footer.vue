<template>
	<div class="footerContainer">
		<div class="qrcode">
			<p>
				<img src="" />
			</p>
			<div>{{ qtext[lang] }}</div>
		</div>

		<p>
			<span @click="showQrcode($event)">{{ ftext[lang] }}</span>
		</p>
		Powered By ThreeJs,Vuejs
		<div class="ba">京ICP备2022032913号-1</div>
		<div class="ba">
			<a
				href="https://www.beian.gov.cn/portal/registerSystemInfo?recordcode=11011402013386"
				target="_blank"
				>北京市昌平驻区大队公安备案号:11011402013386</a
			>
		</div>
	</div>
</template>

<script>
import QRcode from "qrcode";

export default {
	name: "reFooter",
	data() {
		return {
			lang: 0,
			ftext: ["点击访问手机版", "Click Here To Visit Mobile Version"],
			qtext: ["扫描访问手机端", "Use Ur Phone Scan Here"],
		};
	},
	methods: {
		showQrcode(_e) {
			_e.stopPropagation();
			var disp = function () {
				$(".qrcode").hide();
				$(document).unbind("click", disp);
			};

			if ($(".qrcode").css("display") === "none") {
				$(".qrcode").show();
				$(".qrcode").css("top", $(window).height() / 2 - $(".qrcode").height() / 2 + "px");
				$(".qrcode").css("left", $(window).width() / 2 - $(".qrcode").width() / 2 + "px");
				$(document).click(disp);

				QRcode.toDataURL(window.location.origin + "/mobile", function (err, url) {
					$(".qrcode img").attr("src", url);
				});
			} else {
				$(".qrcode").hide();
			}
		},
	},
};
</script>

<style lang="stylus" scoped>
.footerContainer
  position: fixed
  bottom: 1.428571rem
  left: 0px
  width: 100%
  text-align: center
  color: #fff
  z-index: 10
  font-size: 1rem

  span
    cursor: pointer

  p
    margin-bottom: 1.428571rem

  .qrcode
    display: none
    width: 26.214286rem
    overflow: hidden
    position: fixed
    top: 0px
    left: 0px
    background-color: #fff
    padding-bottom: 3.214286rem
    padding-top: 3.214286rem
    border-radius: 1.428571rem

    p
      text-align: center

      img
        margin: auto

    div
      font-size: 1.714286rem
      margin-top: .714286rem
      text-align: center
      color: #454545

	.ba
		font-size:.357143rem

		a
			color:#fff
</style>
