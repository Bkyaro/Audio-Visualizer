export const WindowResizeMixin = {
	data() {
		return {
			width: window.innerWidth,
			height: window.innerHeight,
		};
	},

	methods: {
		handleResize() {
			this.width = window.innerWidth;
			this.height = window.innerHeight;
		},
	},

	created() {
		window.addEventListener("resize", this.handleResize);
	},

	beforeDestroy() {
		window.removeEventListener("resize", this.handleResize);
	},

	mounted() {
		// 初始化时触发一次 handleResize 以确保尺寸正确
		this.handleResize();
	},
};

// 使用方式
// 在你的组件中混入这个 mixin
export default {
	mixins: [WindowResizeMixin],

	// 其他组件属性和方法...
};
