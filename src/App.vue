<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

const textRef = ref(null);
const animatedText1 = ref(null);
const secondScreenRef = ref(null);
const textContainerRef = ref(null);
const animatedText3 = ref(null)

const link = (link) => {
  // router.push(link);
  window.open(link, '_blank');

}

const animateScrollHint = () => {
  const tl = gsap.timeline({ repeat: -1 });
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

const animateText2 = () => {
  const tl = gsap.timeline();
  tl.from(animatedText1.value, {
    opacity: 0,
    y: 50,
    duration: 1,
    ease: "power4.out"
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

// Listen for window scroll events
window.addEventListener('scroll', () => {
  moveTextOnScroll();
});

const moveTextOnScroll = () => {
  const scrollTop = window.scrollY;
  const scrollHeight = document.documentElement.scrollHeight;
  const clientHeight = document.documentElement.clientHeight;
  const scrollPercentage = (scrollTop / (scrollHeight - clientHeight)) * 300;
  const textOffset = scrollPercentage * 0.5;
  gsap.to(textContainerRef.value.children[0], { x: textOffset, duration: 0.5, ease: 'power1.out' });
  gsap.to(textContainerRef.value.children[1], { x: -textOffset, duration: 0.5, ease: 'power1.out' });
  gsap.to(textContainerRef.value.children[2], { x: textOffset, duration: 0.5, ease: 'power1.out' });
  gsap.to(textContainerRef.value.children[3], { x: -textOffset, duration: 0.5, ease: 'power1.out' });
}

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
          <div class="first__screen__scroll">
            <p class="first__screen__scroll__p" ref="animatedText3" >Scroll to explore 	&#8595;	</p>
          </div>
        </div>
        <div class="first__screen__text">
          <h1 ref="textRef">web developer</h1>
        </div>
      </div>
    </section>
    <section class="second_screen" ref="secondScreen">
      <div class="text-container" ref="textContainerRef">
        <p>SASS + NODE + GIT + VUE + REACT + CSS + BOOTSTRAP + ANGULAR +</p>
        <p>TYPESCRIPT + TAILWIND + API + JAVASCRIPT + SQL + NEST + REDUX +</p>
        <p>HTML + UI/UX + POSTMAN + WORDPRESS + TILDA + MONGODB +</p>
        <p>WEBPACK + GULP + RESPONSIVE + MOBILE-FIRST + SEO + NPM + ES6</p>
      </div>
    </section>
    <section class="third_screen">
      <h1>As a front-end developer, I specialize in utilizing HTML, CSS, JavaScript, React, Vue, and Angular to create visually appealing and user-friendly web applications. With expertise in version control systems like Git, I ensure efficient collaboration and seamless development processes.</h1>
      <hr>
      <div class="third_screen__texts df">
        <p>things i can help you with...</p>
        <ul class="third_screen__texts_ul">
          <li>I HAVE A PASSION FOR HELPING SMALL BUSINESSES PROVIDE THEIR CLIENTS WITH THE BEST WEB
            EXPERIENCES. SPECIALIZING IN CRAFTING UNIQUE, FUNCTIONAL, AND AESTHETICALLY PLEASING WEBSITES, I AM DEDICATED TO BRINGING YOUR IDEAS INTO THE DIGITAL ERA.</li>
          <li>LET'S COLLABORATE TO TRANSFORM YOUR VISION INTO A CUTTING-EDGE ONLINE PRESENCE, USHERING YOUR BUSINESS INTO THE MODERN DIGITAL ERA WITH STYLE AND INNOVATION</li>
        </ul>
        <ul>
          <li>Linkedin</li>
          <li>behance</li>
          <li>email</li>
        </ul>
      </div>
    </section>
    <section class="fourth__screen">
      <div class="fourth__screen__container">
        <p>selected works</p>
        <div class="fourth__screen__works df">
          <div @click="link('https://gis-mining.ru/')" class="fourth__screen__work">
            <div class="fourth__screen__work__img df_jcc_aic">
              <img src="./assets/gis-ming.png" alt="">
            </div>
            <div class="fourth__screen__work__text">
              <h3>Gis Ming</h3>
              <p>Web development</p>
            </div>
          </div>
          <div @click="link('https://gremir.ru/')" class="fourth__screen__work">
            <div class="fourth__screen__work__img fourth__screen__work__img2 df_jcc_aic">
              <img src="./assets/gremir.png" alt="">
            </div>
            <div class="fourth__screen__work__text">
              <h3>GREMIR.RU</h3>
              <p>Web development</p>
            </div>
          </div>
          <div @click="link('https://flats-moscow.netlify.app/invest-pro-bussines.tilda.ws/index.html')" class="fourth__screen__work">
            <div class="fourth__screen__work__img fourth__screen__work__img3 df_jcc_aic">
              <img src="./assets/moscow.png" alt="">
            </div>
            <div class="fourth__screen__work__text">
              <h3>MOSCOW new building</h3>
              <p>Web development</p>
            </div>
          </div>
          <div @click="link('https://plastic-clinic.net/')" class="fourth__screen__work">
            <div class="fourth__screen__work__img fourth__screen__work__img4 df_jcc_aic">
              <img src="./assets/plastic-clinic.png" alt="">
            </div>
            <div class="fourth__screen__work__text">
              <h3>plastic clinic</h3>
              <p>Web development</p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="fifth__screen">
      <div class="fifth__screen__text">
        <p>how i work</p>
        <h1>Having thrived as a freelance front-end developer for over a year, I've cultivated invaluable expertise across a spectrum of platforms and technologies. From Bitrix to Tilda.  Let's collaborate to transform your digital aspirations into reality, drawing from my rich tapestry of experience to craft bespoke solutions that leave a lasting impact! </h1>
      </div>
      <div class="fifth__screen__faqs">
        <div class="fifth__screen__faq df">
          <p>01</p>
          <p>research and planning</p>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aperiam ipsum maxime mollitia numquam optio, repellendus.</p>
        </div>
        <div class="fifth__screen__faq df">
          <p>02</p>
          <p>research and planning</p>
          <p>Dive into client requirements, conduct thorough research, and strategize to outline a roadmap for project development.</p>
        </div>
        <div class="fifth__screen__faq df">
          <p>03</p>
          <p>research and planning</p>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aperiam ipsum maxime mollitia numquam optio, repellendus.</p>
        </div>
        <div class="fifth__screen__faq df">
          <p>04</p>
          <p>research and planning</p>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aperiam ipsum maxime mollitia numquam optio, repellendus.</p>
        </div>
        <div class="fifth__screen__faq df">
          <p>05</p>
          <p>research and planning</p>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aperiam ipsum maxime mollitia numquam optio, repellendus.</p>
        </div>
      </div>
    </section>
    <section class="contacts__screen df">
      <div class="contacts__screen__text">
        <p>are you interest in collaborating to elevate your brand in the digital era? <br> let's get to work</p>
        <a href="">xxafiz69@gmail.com</a>
      </div>
      <div class="contacts__screen__link df">
        <ul >
          <li><span>navigation</span></li>
          <li><a href="">about</a></li>
          <li><a href="">work</a></li>
          <li><a href="">services</a></li>
        </ul>
        <ul>
          <li><span>socials</span></li>
          <li><a href="">telegram</a></li>
          <li><a href="">instagram</a></li>
          <li><a href="">linkedin</a></li>
        </ul>
        <ul>
          <li><span>resources</span></li>
          <li><a href="">Github</a></li>
          <li><a href="">hh.ru</a></li>
          <li><a href="">codewars</a></li>
        </ul>
      </div>
    </section>
    <section class="footer__screen">
      <h1>drop me a line</h1>
      <hr>
      <ul class="df">
        <li>©	hoshimov abdulhafiz</li>
        <li>Uzbekistan (GMT +5)</li>
        <li><a href="">back to top</a></li>
        <li>©2024 all rights reserved</li>
      </ul>
      <hr>
    </section>
  </main>
</template>
