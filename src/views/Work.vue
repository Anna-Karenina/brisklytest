<template>
  <form class="wrapper" @submit.prevent="onSubmit">
    <div class="papper">
      <AutomaticlyWorkCheckbox 
        @setAutomaticly='setAutomaticlyChange'
      />
      <BarCodeInput 
        v-on:inputChange = "handleChange"
      />
    </div>
    <ButtonBlock 
      v-if="!isAutomaticly"
      v-on:ScanButtonHandler = 'onSubmit'
      v-on:SaveButtonHandler = 'generatePDF'/>
     <barcode 
      format = 'EAN13'
      elementTag= 'img'
      ref = 'barcoderef'
      v-if='showBarCode'
      v-bind:value="value" />
  </form>
</template>

<script>
import AutomaticlyWorkCheckbox from '@/components/AutomaticlyWorkCheckbox'
import BarCodeInput from '@/components/BarCodeInput'
import ButtonBlock from '@/components/ButtonBlock'
import VueBarcode from 'vue-barcode';
import jspdf from 'jspdf'
export default {
  components: {
    AutomaticlyWorkCheckbox,
    BarCodeInput,
    ButtonBlock,
    barcode: VueBarcode
  },
  data(){
    return{
      stikers:[],
      value: "",
      showBarCode: false,
      isAutomaticly: false
    }
  },
  methods:{
    onSubmit(){
      if(this.value.trim()){
        const newStiker = { 
          id: Date.now(),
          value: this.value,
          printed: false
        }
        this.stikers.push(newStiker)
        //Если понадобится сохранять стикеры 
        this.showBarCode = true 
      }
    },
    handleChange(event){
      const {value} = event.target;
        if(value.length > 12 && this.isAutomaticly){
          this.value = value
          this.onSubmit()
          setTimeout(()=>{
            this.generatePDF()
          }, 100)
        }
      this.value = value
    },
    setAutomaticlyChange({isAutomaticly}){
      this.isAutomaticly = isAutomaticly //значение из деструктив обьекта который приходит в качестве аргумента
    },
    generatePDF(){
      const svgStr = this.$refs.barcoderef.$el.children[0].attributes[1].value
      //не чего лучше этого костыля  я не придумал
      const doc = new jspdf()
      const img = doc.extractImageFromDataUrl(svgStr)
        doc.addImage(img.data, 67,15)
        doc.save('barcode.pdf')
    }
  }
}
</script>

<style scoped>
.wrapper{
  display: flex;
  height: 100%;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.papper{
  width: 40%;
  padding: 2rem 2rem;
   box-shadow:  
    0 4px 5px 0 rgba(0,0,0,0.14), 
    0 1px 10px 0 rgba(0,0,0,0.12), 
    0 2px 4px -1px rgba(0,0,0,0.3);
}
</style>