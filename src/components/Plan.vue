<template>
  <div class="plan">
    <img :src="activeItem.image" alt="">
    <section class="challenges">
      <span>{{ planData.tag }}</span>
      <h3>{{ planData.title }}</h3>
      <div v-for="(item, index) in planData.items" :key="index" class="dropdown" @click="toggleDropdown(index)" :class="{ active: index === activeIndex }">
        <h4 class="dropdown_title">{{ item.title }}</h4>
        <p class="dropdown_content">{{ item.text }}
          <img :src="activeItem.image" alt="" :class="{ active: index === activeIndex }">
        </p>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Plan',
  data() {
    return {
      activeIndex: -1, // Индекс текущего активного элемента
      planData: {
        tag: '',
        title: '',
        items: [],
      },
    };
  },
  computed: {
    activeItem() {
      if (this.activeIndex !== -1) {
        return this.planData.items[this.activeIndex];
      }
      return {};
    },
  },
  mounted() {
    this.loadData();
  },
  methods: {
    async loadData() {
      try {
        const response = await axios.get('https://eoyge3duj7xtdqd.m.pipedream.net/');
        console.log(response.data);
        this.planData = response.data;
        // Если нет активных элементов, устанавливаем первый элемент активным
        if (this.activeIndex === -1 && this.planData.items.length > 0) {
          this.activeIndex = 0;
        }
      } catch (error) {
        console.error('Error loading data:', error);
      }
    },
    toggleDropdown(index) {
        this.activeIndex = index; // Иначе, устанавливаем новый активный элемент
    },
  },
};
</script>
