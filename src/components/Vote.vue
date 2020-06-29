<template>
    <div>
        <h3>{{title}}</h3>
        <div>
            <p>支持人数: {{supNum}}</p>
            <p>反对人数: {{oppNum}}</p>
            <p>支持率: {{ratio}}</p>
            <button @click="change(0)">支持</button>
            <button @click="change(1)">反对</button>
        </div>
    </div>
</template>
<script>
import { watchEffect, ref, reactive, toRefs, readonly, computed, watch } from 'vue'
export default {
    props: {
        title: String
    },
    // props和beforeCreate之间，不能{title}解构
    setup(props) {
       
        //ref一般处理简单值 defineproperty
        // let state = ref({
        //     supNum: 0,
        //     oppNum: 0
        // });
        // function change(lx) {
        //     lx === 0 ? state.value.supNum++ : state.value.oppNum++;
        // }
        // 基于proxy代理的响应式数据
         let state = reactive({
            supNum: 0,
            oppNum: 0
        });
         // props基于proxy代理的响应式数据
        // watchEffect(() => {
        //     console.log(state.supNum);
        // });
        // watch(
        //     () => state.supNum,
        //     () => {
        //         console.log(state.supNum);
        //     }
        // );
        

        function change(lx) {
            lx === 0 ? state.supNum++ : state.oppNum++;
        }
        console.log(toRefs(state));
        // let xxx = reactive({
        //     x: 1,
        //     y: {
        //         m: 's'
        //     }
        // });
        // let xxx2 = readonly(xxx);
        // xxx2.y.m = 's';//警告，不能修改
        let ratio = computed({
            get: () => {
                let total = state.supNum + state.oppNum;
                return total === 0 ? '--' : ((state.supNum / total) * 100).toFixed(2) + '%';
            },
            set: val => {
                console.log(val);
            }
        })
        return  {
            ...toRefs(state),
            ratio,
            change
        }
    }
}
</script>