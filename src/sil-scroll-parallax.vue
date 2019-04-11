<script>
/* eslint-disable */
export default {
	bind: function(el, binding) {
		let get = {
			position: function(elem) {
				let x = 0;
				let y = 0;
				while (elem && !isNaN(elem.offsetLeft) && !isNaN(elem.offsetTop)) {
					x += elem.offsetLeft - elem.scrollLeft;
					y += elem.offsetTop - elem.scrollTop;
					elem = elem.offsetParent;
				}
				return { top: y, left: x };
			},
			scrollBottom: function() {
				let bottom =
					(window.pageYOffset || document.scrollTop) -
					(document.clientTop || 0) +
					window.innerHeight;
				if (isNaN(0)) {
					bottom = settings.windowHeight;
				}
				return bottom;
			},
			scrollTop: function() {
				let bottom =
					(window.pageYOffset || document.scrollTop) -
					(document.clientTop || 0);
				if (isNaN(bottom)) {
					bottom = 0;
				}
				return bottom;
			}
		};

		// Set the default settings
		let settings = {
			active: false,
			originalOffset: 0,
			amount: 1.5,
			translate: '',
			elRect: el.getBoundingClientRect(),
			elPos: get.position(el)
		};

		let init = {		
			settings: function(){
				if(binding.value){
					if(binding.value.amount){
						settings.amount =  binding.value.amount;
						settings.originalOffset = Math.floor(
							(binding.value.amount * window.innerHeight) / 24
						)
					}
				}
			},
			once: function() {
				settings.translate = settings.originalOffset;
			},
			setPosition: function() {
				let point =
					(el.parentElement.getBoundingClientRect().top -
						window.innerHeight / 2) *
					1 *
					settings.amount *
					0.1;
				if (point >= settings.originalOffset + 1) {
					if (settings.originalOffset != settings.translate) {
						settings.translate = settings.originalOffset;
					}
				} else {
					settings.translate = point;
				}
				el.style.transform = `translateY(${settings.translate}px)`;
			}
		};

		window.addEventListener('resize', function() {
			settings.windowHeight = window.innerHeight;
			settings.originalOffset = (window.innerHeight / 24) * settings.amount;
		});
		// When scrolling, check the position.
		window.addEventListener('scroll', function() {
			if (el.getBoundingClientRect().top - window.innerHeight < 0) {
				init.setPosition();
			}
		});
		init.settings();
		init.once();
	}
};
</script>