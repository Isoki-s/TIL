
# axiosを利用してAPIからデータ取得

```js
mounted: function() {
  axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
  .then(function(response){ // 成功した場合の処理
    this.bpi = response.data.bpi
  }.bind(this))
  .catch(function(error){ // エラーハンドリング
    this.hasError = true
  }.bind(this))
  .finally(function(){ // 読み込み完了後の処理
    this.loading = false
  }.bind(this))
}
```

## HTML

```html
<div id="app">
  <h2>Bitcoin price</h2>
  <section v-if="hasError">
    Error
  </section>
  <section  v-else>
    <div v-if="loading">Loading</div>
    <div v-eles>
      <ul v-cloak>
        <li v-for="(rate, currency) in bpi">
          {{currency}} : {{rate.rate_float | currencyDecimal}}
        </li>
      </ul>
    </div>
  </section>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/axios@0.18.0/dist/axios.min.js"></script>
```

## JS

```javascript
var app = new Vue ({
	// option
  el: '#app',
  data: {
  	bpi: null,
    hasError: false,
    loading: true
  },
  mounted: function() {
  	axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
    .then(function(response){
      this.bpi = response.data.bpi
    }.bind(this))
    .catch(function(error){
    	// colsole.log(error);
      this.hasError = true
    }.bind(this))
    .finally(function(){
    	this.loading = false
    }.bind(this))
  },
  filters: {
  	currencyDecimal(value){
    	return value.toFixed(2)
    }
  }
})
```

# jsfiddle
https://jsfiddle.net/isoki/pjteugba/93/