<template>
  <div :class="`${maincls} ${overflowcls}`">
    <section class="flex flex-col items-center h-full">
      <h1 class="text-3xl font-bold font-poppins lg:mt-36 lg:mb-5 mt-14 w-2/4">
        Web Dev <span class="text-accent">Resources</span> for Everyone:
      </h1>
      <div class="w-2/4">
        <p class="text-accent text-lg">I need...</p>
        <div class="inline-block relative w-full">
          <select class="select border-gray-400 mt-5 text-gray"
            name="Category" title="Category" v-model="selectChoice">
            <option disabled value selected>Select a Category</option>
            <option value="Design">Design</option>
            <option value="Styles">Styles</option>
            <option value="Tools">Tools</option>
            <option value="Hosting">Hosting</option>
            <option value="CodeChallenges">CodeChallenges</option>
            <option value="Ports">Ports</option>
            <option value="Other">Other</option>
          </select>
           <div class="pointer-events-none absolute right-0 top-8 flex items-center px-2 text-gray">
             <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
              <path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/>
              </svg>
          </div>
        </div>
      </div>
      <span class="justify-self-end mt-auto">Inspired by
        <a href="https://gitexplorer.com" class="underline text-accent">GitExplorer</a>
      </span>
    </section>
    <section>
      <div class="m-5 bg-light rounded p-10 h-full lg:overflow-y-scroll">
        <p v-text="text" v-if="!selectChoice" class="p-5"></p>
        <ol v-else-if="filteredLinks.length > 0" class="p-5 list-decimal">
          <li v-for="link,index in filteredLinks" :key="index">
            <a class="p-2 hover:underline" :href="link[1]" target="_blank">{{link[0]}}</a>
          </li>
        </ol>
        <p v-else>No Links found</p>
      </div>
    </section>
  </div>
</template>

<script>
import links from './links';

export default {
  name: 'App',
  data() {
    return {
      overflowcls: 'lg:overflow-hidden h-screen',
      maincls: 'main lg:grid-cols-2 lg:grid-rows-1 sm:grid-cols-1 sm:grid-rows-2',
      text: 'Select a Category from the Dropdown',
      selectChoice: '',
      links,
    };
  },
  computed: {
    filteredLinks() {
      const allLinks = this.links;
      // Get the specified section
      const filtered = allLinks[this.selectChoice];
      const KeyValueArrays = [];
      // Create an array in for form of [key,value]
      if (filtered) {
        Object.keys(filtered).forEach((link, index) => {
          KeyValueArrays.push([link, Object.values(filtered)[index]]);
        });
      }
      return KeyValueArrays;
    },
  },
};
</script>

<style></style>
