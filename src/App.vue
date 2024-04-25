<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

const textRef = ref(null);
const animatedText1 = ref(null);
const animatedText3 = ref(null);

const animateText2 = () => {
  const tl = gsap.timeline();
  tl.from(animatedText1.value, {
    opacity: 0,
    y: 50,
    duration: 1,
    ease: "power4.out"
  });
};

const animateScrollHint = () => {
  const tl = gsap.timeline({ repeat: -1, yoyo: true });
  tl.fromTo(animatedText3.value, {
    opacity: 0,
    y: -20,
  }, {
    opacity: 1,
    y: 20,
    duration: 1,
    ease: "power1.inOut",
  }).to(animatedText3.value, {
    opacity: 0,
    y: -20,
    duration: 1,
    ease: "power1.inOut",
  });
};

const animateText = () => {
  const tl = gsap.timeline();
  const letters = textRef.value.textContent.split('');
  textRef.value.textContent = '';

  letters.forEach((letter, index) => {
    const span = document.createElement('span');
    span.textContent = letter;
    span.style.display = 'inline-block';
    span.style.opacity = 0;
    span.style.transform = 'translateY(-100%)';

    textRef.value.appendChild(span);

    tl.to(span, {
      opacity: 1,
      y: 0,
      duration: 0.2,
      ease: 'power4.out',
      delay: index * 0.01
    });
  });
};

onMounted(() => {
  animateText();
  animateText2();
  animateScrollHint();
});
</script>

<template>
  <main class="screen">
    <section class="first__screen">
      <header>
        <ul class="first__screen__ul df">
          <li>Hoshimov <br> Abdulhafiz</li>
          <li>Front-end <br>  Developer</li>
          <li>Available for <br> freelance work</li>
          <li><button><a href="#">Contact</a></button></li>
        </ul>
      </header>
      <div class="first__screen__about__scroll__text">
        <div class="first__screen__about__scroll df">
          <div class="first__screen__about">
            <p class="first__screen__about__p" ref="animatedText1">
              As a passionate front-end developer, I specialize in crafting innovative and user-friendly web applications. I pride myself on delivering high-quality solutions that meet the unique requirements of clients and users alike.
            </p>
          </div>
          <div class="first__screen__scroll" ref="animatedText3">
            <p class="first__screen__scroll__p">Scroll to explore 	&#8595;	</p>
          </div>
        </div>
        <div class="first__screen__text">
          <h1 ref="textRef">web developer</h1>
        </div>
      </div>
    </section>
  </main>
</template>
