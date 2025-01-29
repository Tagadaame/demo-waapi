<template>
    <section class="w-3/5 mx-auto">
        <div v-for="(item, index) in accordionItems" :key="index">
            <details ref="details" class="mb-2">
                <summary class="bg-tealight relative w-full font-bold cursor-pointer border-4 border-transparent focus:border-tealight text-white p-2">{{ item.summary }}</summary>
                <div class="content p-3 border-2 border-tealight border-t-0 bg-white">
                    <p>{{ item.content }}</p>
                </div>
            </details>
        </div>
    </section>
</template>
  
<script setup>

  const accordionItems = [
    {
      summary: 'Pourquoi les WAAPI sont cool',
      content: 'vous devriez désormais le savoir...',
    },
    {
        summary: 'Pourquoi les WAAPI sont performantes',
        content: 'Relire la slide 3...',
    },
    {
        summary: 'Pourquoi les WAAPI sont faciles à utiliser',
        content: 'Même moi je me débrouille avec...',
    }
  ];
  
  const accordion = ref([]);
  
  class Accordion {
    constructor(el) {
      this.el = el;
      this.summary = el.querySelector('summary');
      this.content = el.querySelector('.content');
      this.animation = null;
      this.isClosing = false;
      this.isExpanding = false;
      this.summary.addEventListener('click', (e) => this.onClick(e));
    }
  
    onClick(e) {
      e.preventDefault();
      this.el.style.overflow = 'hidden';
      if (this.isClosing || !this.el.open) {
        this.open();
      } else if (this.isExpanding || this.el.open) {
        this.shrink();
      }
    }
  
    shrink() {
      this.isClosing = true;
      const startHeight = `${this.el.offsetHeight}px`;
      const endHeight = `${this.summary.offsetHeight}px`;
  
      if (this.animation) {
        this.animation.cancel();
      }
  
      this.animation = this.el.animate(
        {
          height: [startHeight, endHeight]
        },
        {
          duration: 400,
          easing: 'ease-out'
        }
      );
  
      this.animation.onfinish = () => this.onAnimationFinish(false);
      this.animation.oncancel = () => (this.isClosing = false);
    }
  
    open() {
      this.el.style.height = `${this.el.offsetHeight}px`;
      this.el.open = true;
      window.requestAnimationFrame(() => this.expand());
    }
  
    expand() {
      this.isExpanding = true;
      const startHeight = `${this.el.offsetHeight}px`;
      const endHeight = `${this.summary.offsetHeight + this.content.offsetHeight}px`;
  
      if (this.animation) {
        this.animation.cancel();
      }
  
      this.animation = this.el.animate(
        {
          height: [startHeight, endHeight]
        },
        {
          duration: 400,
          easing: 'ease-out'
        }
      );
  
      this.animation.onfinish = () => this.onAnimationFinish(true);
      this.animation.oncancel = () => (this.isExpanding = false);
    }
  
    onAnimationFinish(open) {
      this.el.open = open;
      this.animation = null;
      this.isClosing = false;
      this.isExpanding = false;
      this.el.style.height = this.el.style.overflow = '';
    }
  }
  
  onMounted(() => {
    accordion.value = document.querySelectorAll('details');
    accordion.value.forEach((el) => new Accordion(el));
  });
</script>
  

