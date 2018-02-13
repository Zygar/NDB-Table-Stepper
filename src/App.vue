<template>
    <main id="App"  :class="'table-step-'+step">
        <header>
            <div class="stepper">
                <div><button v-if="step >= 1" @click="decrementStep()">⬅</button></div>
                <div class="current-step"><span v-if="step >=1">{{step}}</span> <span v-else>Click arrow to start</span></div>
                <div><button v-if="step <= 6" @click="incrementStep()">➡</button></div>
            </div>
            
            <div class="stepper-highlight  step-content">
                
                <p v-if="step == 0">Using our Rawhiti Wines example, let’s step through a very simplified flow of costs from the production of wine through to the sale of the finished product and where each step would be recorded in the income statement and the statement of financial position.</p>
                <p v-if="step == 1">Purchase grapes and other raw materials (enough to produce 50 units), $500 (add to raw materials inventory)</p>
                <p v-if="step == 2">Incur  other  manufacturing costs through the production process, for example, wine-maker costs, bottles and labels (enough to produce  40 units), $600 (add to work in process inventory)</p>
                <p v-if="step == 3">Recognise a portion  of the raw material consumed in the current work in process of 15 cases of wine being made, $150 (transfer from raw materials inventory to work in process inventory)</p>
                <p v-if="step == 4"> 12 cases of wine are bottled and ready for sale, collate the full unit costs of getting the wine to finished state, $300 (transfer from  work in process inventory to finished goods inventory)</p>
                <p v-if="step == 5">Sell 10 cases of wine, $450 (recorded  as sales in the income statement)</p>
                <p v-if="step == 6">Expense the cost of those 10 cases of wine, $250 (transfer from finished goods inventory to cost of goods sold in the income statement</p>
                <p v-if="step == 7">All done! Review the completed statements below.</p>
            </div>
        </header>
        <div class="tables">
            <section id="financial-position"> 
                <h2>Statement of Financial Position</h2>
                <table>
                    <!-- Head -->
                    <tr class="table-header">
                        <td class="line-description"></td>
                        <td>Debit</td>
                        <td>Credit</td>
                    </tr>
                    <!-- Part One -->

                    <tr class="header-row">
                        <td class="line-description"></td>
                        <td colspan="2">Raw material inventory</td>
                    </tr>
                    
                    <tr class="step-highlight  step-1">
                        <td class="line-description"><span class="step" v-if="step >= 1">[1] 50 units of raw material</span></td>
                        <td><span class="step" v-if="step >= 1" >500</span></td>
                        <td></td>
                    </tr>

                    <tr class="step-highlight  step-3">
                        <td class="line-description"><span class="step" v-if="step >= 3">[3] 50 units of raw material</span></td>
                        <td></td>
                        <td><span class="step" v-if="step >= 3">150</span></td>
                    </tr>
                    <tr class="step-highlight  step-3  close-bal">
                        <td class="line-description">Close bal</td>
                        <td><span class="step"  v-if="step >=3">350</span></td>
                        <td></td>
                    </tr>
                    <!-- Part Two -->
                    <tr class="header-row">
                        <td class="line-description"></td>
                        <td colspan="2">Work in process inventory</td>
                    </tr>
                    <tr class="step-highlight  step-2">
                        <td class="line-description"><span class="step" v-if="step >= 2">[2] 40 units worth - other manufacturing</span></td>
                        <td><span class="step"  v-if="step >= 2">600</span></td>
                        <td></td>
                    </tr>
                    <tr class="step-highlight  step-3">
                        <td class="line-description"><span class="step" v-if="step >= 3">[3] 15 units worth of raw material</span></td>
                        <td><span class="step"  v-if="step >= 3">150</span></td>
                        <td></td>
                    </tr>
                    <tr class="step-highlight  step-4">
                        <td class="line-description"><span class="step" v-if="step >= 4">[4] 12 units finished</span></td>
                        <td><span class="step"  v-if="step >= 4">300</span></td>
                        <td></td>
                    </tr>
                    <tr class="step-highlight  step-4  close-bal">
                        <td class="line-description">Close bal</td>
                        <td><span class="step"  v-if="step >=4">450</span></td>
                        <td></td>
                    </tr>
                    <!-- Part Three -->
                    <tr class="header-row">
                        <td class="line-description"></td>
                        <td colspan="2">Finished goods inventory</td>
                    </tr>
                    <tr class="step-highlight  step-4">
                        <td class="line-description"><span class="step" v-if="step >= 4">[4] 12 units available</span></td>
                        <td><span class="step"  v-if="step >= 4">300</span></td>
                        <td></td>
                    </tr>
                    <tr class="step-highlight  step-6">
                        <td class="line-description"><span class="step"  v-if="step >= 6">[6] 10 units sold</span></td>
                        <td></td>
                        <td><span class="step"  v-if="step >= 6">250</span></td>
                    </tr>
                    <tr class="step-highlight  step-6  close-bal">
                        <td class="line-description">Close bal</td>
                        <td><span class="step"  v-if="step >=6">50</span></td>
                        <td></td>
                    </tr>
                    <!-- Part Four -->
                    <tr class="header-row">
                        <td class="line-description"></td>
                        <td colspan="2">Bank</td>
                    </tr>
                    <tr class="step-highlight  step-1">
                        <td class="line-description"><span class="step" v-if="step >= 1">Step 1</span></td>
                        <td></td>
                        <td><span class="step" v-if="step >= 1">500</span></td>
                    </tr>
                    <tr class="step-highlight  step-2">
                        <td class="line-description"><span class="step" v-if="step >= 2">Step 2</span></td>
                        <td></td>
                        <td><span class="step" v-if="step >= 2">600</span></td>
                    </tr>
                    <tr class="step-highlight  step-5">
                        <td class="line-description"><span class="step" v-if="step >= 5">Step 5</span></td>
                        <td><span class="step" v-if="step >= 5">450</span></td>
                        <td></td>
                    </tr>
                    <tr class="step-highlight  step-5  close-bal">
                        <td class="line-description">Close bal</td>
                        <td></td>
                        <td><span class="step"  v-if="step >=5">650</span></td>
                    </tr>
                </table>
            </section> 
            <section id="income-statement">
                <h2>Income Statement</h2>
                <table> <!-- Head -->
                    <tr class="table-header">
                        <td class="line-description"></td>
                        <td>Debit</td>
                        <td>Credit</td>
                    </tr>
                    <!-- Part One -->

                    <tr class="header-row">
                        <td class="line-description"></td>
                        <td colspan="2">Sales</td>
                    </tr>
                    
                    <tr class="step-highlight  step-5">
                        <td class="line-description"><span class="step" v-if="step >= 5">[5] 10 units</span></td>
                        <td></td>
                        <td ><span class="step" v-if="step >= 5">450</span></td>
                    </tr>
                    <tr class="header-row">
                        <td class="line-description"></td>
                        <td colspan="2">Cost of Goods Sold</td>
                    </tr>
                    <tr class="step-highlight  step-6">
                        <td class="line-description"><span class="step" v-if="step >= 6">[6] 10 units</span></td>
                        <td><span class="step" v-if="step >= 6">250</span></td>
                        <td></td>
                    </tr>

                </table>
            </section>    
        </div>
        
    </main>
</template>

<script>
import eventHub from './eventHub.js';
import data from './content/_data.js';

export default {
    name: 'app', 
    components: {  },
    data () { 
        let data = {step: 0}
        return data
    }, 
    computed: {
    },
    methods: { 
        incrementStep() {
            if (this.step <= 6) {
                this.step ++    
            }
            
        },
        decrementStep() {
            if (this.step >= 1) {
                this.step --
            }

        }
    }
}
</script>

<style type="text/css">
    
</style>
