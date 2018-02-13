<template>
    <main id="App"  :class="'table-step-'+step">
        <header>We'll put the step-by-step thing here and make it fixed <input type="number" v-model="step" name=""></header>
        <section> 
            <h2>Statement of Financial Position</h2>
            <table >
                <!-- Head -->
                <tr>
                    <td class="line-description"></td>
                    <td>Debit</td>
                    <td>Credit</td>
                </tr>
                <!-- Part One -->

                <tr>
                    <td class="line-description"></td>
                    <td colspan="2">Raw material inventory</td>
                </tr>
                
                <tr class="step-1">
                    <td class="line-description"><span class="step" v-if="step >= 1">[1] 50 units of raw material</span></td>
                    <td><span class="step" v-if="step >= 1" >500</span></td>
                    <td></td>
                </tr>

                <tr class="step-3">
                    <td class="line-description"><span class="step" v-if="step >= 3">[3] 50 units of raw material</span></td>
                    <td></td>
                    <td><span class="step" v-if="step >= 3">150</span></td>
                </tr>
                <tr>
                    <td class="line-description">Close bal</td>
                    <td>350</td>
                    <td></td>
                </tr>
                <!-- Part Two -->
                <tr>
                    <td class="line-description"></td>
                    <td colspan="2">Work in process inventory</td>
                </tr>
                <tr class="step-2">
                    <td class="line-description"><span class="step" v-if="step >= 2">[2] 40 units worth - other manufacturing</span></td>
                    <td><span class="step"  v-if="step >= 2">600</span></td>
                    <td></td>
                </tr>
                <tr class="step-3">
                    <td class="line-description"><span class="step" v-if="step >= 3">[3] 15 units worth of raw material</span></td>
                    <td><span class="step"  v-if="step >= 3">150</span></td>
                    <td></td>
                </tr>
                <tr class="step-4">
                    <td class="line-description"><span class="step" v-if="step >= 4">[4] 12 units finished</span></td>
                    <td><span class="step"  v-if="step >= 4">300</span></td>
                    <td></td>
                </tr>
                <tr>
                    <td class="line-description">Close bal</td>
                    <td>450</td>
                    <td></td>
                </tr>
                <!-- Part Three -->
                <tr>
                    <td class="line-description"></td>
                    <td colspan="2">Finished goods inventory</td>
                </tr>
                <tr class="step-4">
                    <td class="line-description"><span class="step" v-if="step >= 4">[4] 12 units available</span></td>
                    <td><span class="step"  v-if="step >= 4">300</span></td>
                    <td></td>
                </tr>
                <tr class="step-6">
                    <td class="line-description"><span class="step"  v-if="step >= 6">[6] 10 units sold</span></td>
                    <td></td>
                    <td><span class="step"  v-if="step >= 6">250</span></td>
                </tr>
                <tr>
                    <td class="line-description">Close bal</td>
                    <td>50</td>
                    <td></td>
                </tr>
                <!-- Part Four -->
                <tr>
                    <td class="line-description"></td>
                    <td colspan="2">Bank</td>
                </tr>
                <tr class="step-1">
                    <td class="line-description">Step 1</td>
                    <td></td>
                    <td>500</td>
                </tr>
                <tr class="step-2">
                    <td class="line-description">Step 2</td>
                    <td></td>
                    <td>600</td>
                </tr>
                <tr class="step-5">
                    <td class="line-description">Step 5</td>
                    <td>450</td>
                    <td></td>
                </tr>
                <tr>
                    <td class="line-description">Close bal</td>
                    <td>50</td>
                    <td></td>
                </tr>
            </table>
        </section> 
        <section>
            <h2>Income Statement</h2>
            <table> <!-- Head -->
                <tr>
                    <td class="line-description"></td>
                    <td>Debit</td>
                    <td>Credit</td>
                </tr>
                <!-- Part One -->

                <tr>
                    <td class="line-description"></td>
                    <td colspan="2">Sales</td>
                </tr>
                
                <tr class="step-5">
                    <td class="line-description">[5] 10 units</td>
                    <td></td>
                    <td>450</td>
                </tr>
                <tr>
                    <td class="line-description"></td>
                    <td colspan="2">Cost of Goods Sold</td>
                </tr>
                <tr class="step-6">
                    <td class="line-description">[6] 10 units</td>
                    <td>250 </td>
                    <td></td>
                </tr>

            </table>
        </section>
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
    }
}
</script>

<style type="text/css">
    
</style>
