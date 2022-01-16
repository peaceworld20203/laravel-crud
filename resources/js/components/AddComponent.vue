<template>
<div id = "databinding" style = "">
         <h1>Customer Details</h1>
         <span>First Name</span>
         <input type = "text" placeholder = "Enter First Name" v-model = "fname"/>
         <span>Last Name</span>
         <input type = "text" placeholder = "Enter Last Name" v-model = "lname"/>
         <span>Address</span>
         <input type = "text" placeholder = "Enter Address" v-model = "addr"/>
         <button v-on:click = "showdata" v-bind:style = "styleobj">Add</button>
         <br/>
         <br/>
         <customercomponent
            v-for = "(item, index) in custdet"
            v-bind:item = "item"
            v-bind:index = "index"
            v-bind:itr = "item"
            v-bind:key = "item.fname"
            v-on:removeelement = "custdet.splice(index, 1)">
         </customercomponent>
      </div>
</template>

<script type = "text/javascript">
    Vue.component('customercomponent',{
    template : '<div class = "Table"><div class = "Row"  v-bind:style = "styleobj"><div class = "Cell"><p>{{itr.fname}}</p></div><div class = "Cell"><p>{{itr.lname}}</p></div><div class = "Cell"><p>{{itr.addr}}</p></div><div class = "Cell"><p><button v-on:click = "$emit(\'removeelement\')">X</button></p></div></div></div>',
    props: ['itr', 'index'],
    data: function() {
        return {
            styleobj : {
                backgroundColor:this.getcolor(),
                fontSize : 20
            }
        }
    },
    methods:{
        getcolor : function() {
            if (this.index % 2) {
                return "#FFE633";
            } else {
                return "#D4CA87";
            }
        }
    }
    });
    var vm = new Vue({
    el: '#databinding',
    data: {
        fname:'',
        lname:'',
        addr : '',
        custdet:[],
        styleobj: {
            backgroundColor: '#2196F3!important',
            cursor: 'pointer',
            padding: '8px 16px',
            verticalAlign: 'middle',
        }
    },
    methods :{
        showdata : function() {
            this.custdet.push({
                fname: this.fname,
                lname: this.lname,
                addr : this.addr
            });
            this.fname = "";
            this.lname = "";
            this.addr = "";
        }
    }
    });
</script>