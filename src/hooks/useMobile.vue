export default {
	data() {
		return {
			isMobile: this.checkIsMobile(),
			resizeHandler: null,
		};
	},

	methods: {
		checkIsMobile() {
			const userAgent = window.navigator.userAgent || "";
			const isMobileByUserAgent = Boolean(
				userAgent.match(
					/Android|BlackBerry|iPhone|iPad|iPod|Opera Mini|IEMobile/i
				)
			);
			return isMobileByUserAgent || window.innerWidth < 500;
		},

		handleResize() {
			this.isMobile = window.innerWidth < 500;
		},
	},

	created() {
		// 初始化时判断是否为移动设备并添加窗口大小改变事件监听器
		this.isMobile = this.checkIsMobile();
		this.resizeHandler = () => this.handleResize();
		window.addEventListener("resize", this.resizeHandler);
	},

	beforeDestroy() {
		// 组件卸载时移除窗口大小改变事件监听器
		window.removeEventListener("resize", this.resizeHandler);
	},

	mounted() {
		// Vue 2 中没有立即执行的 watch，因此在 mounted 钩子中手动触发一次更新
		this.handleResize();
	},
};
