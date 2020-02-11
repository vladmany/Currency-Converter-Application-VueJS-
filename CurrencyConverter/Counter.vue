<template>
	<div id="counter">
		<div class="change-currency">
			<span>Your currency: </span>
			<select v-model="currency">
				<option>EUR</option>
				<option>USD</option>
				<option>UAH</option>
				<option>RUB</option>
			</select>
		</div>
		<div class="counters-wrapper">
			<button>
				<span>EUR</span>
				<span v-if="currency=='USD'">{{ baseUSD.rates["EUR"].toFixed(2) }}</span>
			</button>
			<button>
				<span>USD</span>
				<span v-if="currency=='USD'">{{ baseUSD.rates["USD"].toFixed(2) }}</span>
			</button>
			<button>
				<span>UAH</span>
				<span v-if="currency=='USD'">{{ baseUSD.rates["UAH"].toFixed(2) }}</span>
			</button>
			<button>
				<span>RUB</span>
				<span v-if="currency=='USD'">{{ baseUSD.rates["RUB"].toFixed(2) }}</span>
			</button>
		</div>
	</div>
</template>

<script>
export default {
  props: {
    eBaseEUR: {
    	retes: Object // eslint-disable-line no-mixed-spaces-and-tabs
    },
    eBaseUSD: {
    	retes: Object // eslint-disable-line no-mixed-spaces-and-tabs
    },
    eBaseUAH: {
    	retes: Object // eslint-disable-line no-mixed-spaces-and-tabs
    },
    eBaseRUB: {
    	retes: Object // eslint-disable-line no-mixed-spaces-and-tabs
    }
  },
  name: "Counter",
  data() {
  	return {  // eslint-disable-line no-mixed-spaces-and-tabs
  		currency: "USD", // eslint-disable-line no-mixed-spaces-and-tabs
  		baseEUR: {}, // eslint-disable-line no-mixed-spaces-and-tabs
  		baseUSD: {}, // eslint-disable-line no-mixed-spaces-and-tabs
  		baseUAH: {}, // eslint-disable-line no-mixed-spaces-and-tabs
  		baseRUB: {}, // eslint-disable-line no-mixed-spaces-and-tabs
  		xhr: new XMLHttpRequest() // eslint-disable-line no-mixed-spaces-and-tabs
  

  	} // eslint-disable-line no-mixed-spaces-and-tabs
  },
  created() {
  	this.getUSD() // eslint-disable-line no-mixed-spaces-and-tabs
  },
  methods: {
  	getUSD(){ // eslint-disable-line no-mixed-spaces-and-tabs
		this.xhr.open('GET', 'https://openexchangerates.org/api/latest.json?app_id=5954f5892b0c4406ac65618a72c8aa14', false);
		this.xhr.send();

		// 4. Если код ответа сервера не 200, то это ошибка
		if (this.xhr.status != 200) {
		  this.baseUSD = { // eslint-disable-line no-mixed-spaces-and-tabs
		  	rates: { // eslint-disable-line no-mixed-spaces-and-tabs
		  		"EUR": "none", // eslint-disable-line no-mixed-spaces-and-tabs
		  		"USD": "none", // eslint-disable-line no-mixed-spaces-and-tabs
		  		"UAH": "none", // eslint-disable-line no-mixed-spaces-and-tabs
		  		"RUB": "none" // eslint-disable-line no-mixed-spaces-and-tabs
		  	} // eslint-disable-line no-mixed-spaces-and-tabs 
		  } // eslint-disable-line no-mixed-spaces-and-tabs
		} else { // eslint-disable-line no-mixed-spaces-and-tabs
			this.baseUSD = JSON.parse(this.xhr.responseText) // eslint-disable-line no-mixed-spaces-and-tabs
		}
  	} // eslint-disable-line no-mixed-spaces-and-tabs
  }
}
</script>
<!--  eslint-disable no-mixed-spaces-and-tabs -->
<style type="text/css" scoped>
	.change-currency {
		max-width: 500px;
		display: flex;
		justify-content: flex-end;
		margin-bottom: 50px;
	}	
	.change-currenct span {
		/*float: right;*/
	}
	.counters-wrapper {
		display: flex;
	}
	.counters-wrapper button {
		display: flex;
		flex-direction: column;
		width: 60px;
		height: 40px;
  		align-items: center; 
  		justify-content: center;
  		border-radius: 15px;
  		border-width: 0px;
  		background-color: gray;
  		margin-right: 25px;
  		outline: none; 	
	}
	.counters-wrapper button:hover {
		cursor: pointer;
	}
	.counters-wrapper button span {
		color: #00FF00;
		font-weight: bold;
	}
</style>
<!--  eslint-disable no-mixed-spaces-and-tabs -->