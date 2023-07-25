<script lang="ts" setup>
import { Icon } from '@iconify/vue';
import {
  useDashboard,
  LoadingStatus,
  type ChainConfig,
} from '@/stores/useDashboard';
import ChainSummary from '@/components/ChainSummary.vue';
import { computed, ref } from 'vue';
import { useBlockchain } from '@/stores';

const dashboard = useDashboard();

const keywords = ref('');
const chains = computed(() => {
  if (keywords.value) {
    return Object.values(dashboard.chains).filter(
      (x: ChainConfig) => x.chainName.indexOf(keywords.value) > -1
    );
  } else {
    return Object.values(dashboard.chains);
  }
});
const chainStore = useBlockchain()
</script>
<template>
  <div class="">
    <div class="flex md:!flex-row flex-col items-center justify-center mb-6 mt-14 gap-2">
      <div class="w-16 rounded-full">
		<svg version="1.0" svg id="Layer_1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 150.000000 150.000000"><circle cx="191.3254" cy="191.3254" r="191.3254" fill="#fff"/><path d="m191.3254,27.08419C100.61745,27.08419,27.08419,100.61751,27.08419,191.3254s73.53326,164.24121,164.24121,164.24121,164.24121-73.53326,164.24121-164.24121S282.03334,27.08419,191.3254,27.08419Zm104.58002,189.44122c-1.08002,16.20001-12.23999,29.52002-12.23999,29.52002l19.43994,21.23999-36.71997,34.56-18.71997-19.08002c-13.32001,10.08002-31.32001,13.14001-31.32001,13.14001v28.62h-49.67999v-29.88c-8.28003,2.16003-31.32001-11.88-31.32001-11.88l-20.52002,19.44-33.47998-34.91998,18.71716-19.8454c-8.27997-9.35999-14.39716-33.07458-14.39716-33.07458h-26.28003v-48.60004l28.79999-.35999c2.88-19.79999,11.52002-32.40002,11.52002-32.40002l-18.35999-18.71997,34.91998-34.56,19.79999,18.71997c14.76001-7.56,30.60004-12.59998,30.60004-12.59998l.35999-27.72003h50.03998l.35999,28.08002c14.40002,3.60004,31.67999,11.88,31.67999,11.88l20.16003-18.71997,34.56,36.35999-19.44,18.71997c8.28003,15.48004,12.23999,32.04004,12.23999,32.04004h26.64001v50.03998h-27.35999Z" fill="#141a46"/><circle cx="191.3254" cy="191.32541" r="57.78002" fill="#141a46"/></svg>
      </div>
      <h1 class="text-primary dark:invert text-3xl md:!text-6xl font-bold">
        Cogwheel Explorer
      </h1>
    </div>
    <div class="text-center text-base">
      <p class="mb-1">
        Cogwheel Explorer serves as a highly efficient and sophisticated platform,
		designed to cater to your asset management needs with utmost precision and convenience.
      </p>
      <h2 class="mb-6">Provided to you by your favorate validator Cogwheel⚙️</h2>
    </div>
    <div
      v-if="dashboard.status !== LoadingStatus.Loaded"
      class="flex justify-center"
    >
      <progress class="progress progress-info w-80 h-1"></progress>
    </div>

    <div class="flex items-center rounded-lg bg-base-100  border border-gray-200 dark:border-gray-700 mt-10">
      <Icon icon="mdi:magnify" class="text-2xl text-gray-400 ml-3"/>
      <input :placeholder="$t('pages.search_placeholder')" class="px-4 h-10 bg-transparent flex-1 outline-none text-base" v-model="keywords" />
      <div class="px-4 text-base hidden md:!block">{{ chains.length }}/{{ dashboard.length }}</div>
    </div>

    <div
      class="grid grid-cols-1 gap-4 mt-6 md:!grid-cols-3 lg:!grid-cols-4 2xl:!grid-cols-5"
    >
      <ChainSummary
        v-for="(chain, index) in chains"
        :key="index"
        :name="chain.chainName"
      />
    </div>
  </div>
</template>

<style scoped>
 .logo path{
  fill: #171d30;
}
</style>
