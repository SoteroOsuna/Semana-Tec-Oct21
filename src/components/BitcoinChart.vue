<template>
    <v-container>
        <p>Aquí va a ir mi gráfica de bitcoin con {{cripto}} {{moneda}} {{plazo}}</p>
        <apexchart width="500" type="area" :options="options" :series="series"></apexchart>

    </v-container>
</template>

<script>
export default {
    props: ['cripto','moneda','plazo'],

    watch:{
        cripto:function(newCripto,oldCripto){
            console.log(newCripto)
            console.log(oldCripto)
            this.cargarDatos();
        },
        moneda:function(newCripto,oldCripto){
            console.log(newCripto)
            console.log(oldCripto)
            this.cargarDatos();
        },
        plazo:function(newCripto,oldCripto){
            console.log(newCripto)
            console.log(oldCripto)
            this.cargarDatos();
        }
    },
    methods:{

        cargarDatos(){
            //TODO implementar aquí su llamada deberemos cambiar la data de categories y de data
            var datos = []
            this.axios.get('https://api.coingecko.com/api/v3/coins/'+this.cripto+'/market_chart?vs_currency='+this.moneda+'&days='+this.plazo).then((response)=>{
                console.log(response);
                response.data.prices.forEach( element => {
                  datos.push(element)
                });
                this.series = [{
                  data: datos
                }];
                console.log(this.series.data);
            })
        }
    },

    data: ()=>({
      options: {
        chart: {
          id: 'vuechart-example'
        },
      },
      xaxis: {
        type: 'datetime',
        labels: {
          
        }
      },
      series: [{
        name: 'graficaCripto',
        data: [1,2,3,4,5]
      }]
    })
}
</script>
