<script setup>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

const textRef = ref(null);
const textContainer = ref(null);
const animatedText1 = ref(null);
const secondScreenRef = ref(null);
const textContainerRef = ref(null);
const animatedText3 = ref(null);
const marqueeColor = ref('grey');
const textColor = ref('grey');
const isHovered = ref([false, false, false, false])
const cards = ref([
  {
    id: 1,
    title: "Landing Page Development ★ Landing Page Development ★ Landing Page Development ★ Landing Page Development ★ Landing Page Development",
    description: "Optimizing landing pages for user engagement and conversion using HTML, CSS, and JavaScript.",
    direction: "left"
  },
  {
    id: 2,
    title: "CRM ★ CRM ★ CRM ★ CRM ★ CRM ★ CRM ★ CRM ★ CRM ★ CRM ★ CRM ★ CRM ★ CRM",
    description: "Implementing the front-end interface for CRM systems used to manage customer interactions and data.",
    direction: "right"
  },
  {
    id: 3,
    title: "E-commerce Website ★ E-commerce Website ★ E-commerce Website ★ E-commerce Website ★ E-commerce Website ★",
    description: "Building the front-end of e-commerce platforms to showcase products and facilitate online transactions.",
    direction: "left"
  },
  {
    id: 4,
    title: "Web Application Refactoring ★ Web Application Refactoring ★ Web Application Refactoring ★ Web Application Refactoring ★ Web Application Refactoring ★",
    description: "Refactoring existing front-end codebase to improve performance, maintainability, and scalability.",
    direction: "right"
  }
])

const link = (link) => {
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

window.addEventListener('blur', () => {
  document.title = 'where are you? 😢'
})

window.addEventListener('focus', () => {
  document.title = 'Abdulhafiz Hoshimov'
})

const customCursor = () => {
  const cursor = document.querySelector('.cursor');
  const cursorTailCount = 5; // Number of tail elements
  const cursorTailElements = [];

  // Create cursor tail elements
  for (let i = 0; i < cursorTailCount; i++) {
    const tailElement = document.createElement("div");
    tailElement.classList.add("cursor-tail");
    document.body.appendChild(tailElement);
    cursorTailElements.push(tailElement);
  }

  function updateCursorTail(event) {
    const mouseX = event.clientX;
    const mouseY = event.clientY;

    for (let i = cursorTailElements.length - 1; i > 0; i--) {
      const prevX = cursorTailElements[i - 1].style.left;
      const prevY = cursorTailElements[i - 1].style.top;
      cursorTailElements[i].style.left = prevX;
      cursorTailElements[i].style.top = prevY;
    }

    cursorTailElements[0].style.left = mouseX + "px";
    cursorTailElements[0].style.top = mouseY + "px";
  }

  // Track mouse movement and update cursor tail
  document.addEventListener('mousemove', e => {
    cursor.setAttribute("style", "top: " + (e.pageY - 10) + "px; left: " + (e.pageX - 10) + "px;");
    updateCursorTail(e);
  });

  document.addEventListener('click', e => {
    cursor.classList.add("expand");
    setTimeout(() => {
      cursor.classList.remove("expand");
    }, 500);
  });
};


const handleHover = (index) => {
  isHovered.value[index] = true;
};

const handleLeave = (index) => {
  isHovered.value[index] = false;
};



onMounted(() => {
  animateText();
  animateText2();
  animateScrollHint();
  customCursor();
});



</script>

<template>
  <main class="screen">
    <div class="cursor"></div>
    <section id="first__screen" class="first__screen">
      <header>
        <ul class="first__screen__ul df">
          <li  data-aos="fade-down">Hoshimov <br> Abdulhafiz</li>
          <li  data-aos="fade-down">Front-end <br>  Developer</li>
          <li  data-aos="fade-down">Available for <br> freelance work</li>
          <li  data-aos="fade-down"><button><a href="#contacts">Contact</a></button></li>
        </ul>
      </header>
      <div class="first__screen__about__scroll__text">
        <div class="first__screen__about__scroll df">
          <div class="first__screen__about">
            <p class="first__screen__about__p" ref="animatedText1">
              Hi, i am abdulhafiz i have started my programming experience in 2020. Starting studying in education center. Being the best student in education center for a years in 2022 i have started my trip to freelance plaatforms and have worked for more than year. I AM
            </p>
          </div>
          <div class="first__screen__scroll">
            <p class="first__screen__scroll__p" ref="animatedText3" >Scroll to explore 	&#8595;	</p>
          </div>
        </div>
        <div class="first__screen__text" ref="textContainer">
          <h1 ref="textRef">web developer</h1>
        </div>
      </div>
    </section>
    <section class="second_screen">
      <h1>What do i actually do</h1>
      <div class="second_screen_cards">
        <div class="second_screen_card" @mouseover="handleHover" @mouseleave="handleLeave">

        </div>
        <div class="second_screen_card" v-for="(card, index) in cards"  @mouseover="handleHover(index)" @mouseleave="handleLeave(index)">
          <marquee ref="marquee" behavior="alternate" scrollamount="25" :direction="card.direction" :class="{'hovered': isHovered[index]}" class="marquee">
            {{ card.title }}
          </marquee>
          <p :class="{'text-hovered': isHovered[index]}">{{card.description}}</p>
        </div>
      </div>
    </section>
    <section class="third_screen">
      <h1  data-aos="fade-right">As a front-end developer, I specialize in utilizing HTML, CSS, JavaScript, React and Vue to create visually appealing and user-friendly web applications. With expertise in version control systems like Git, I ensure efficient collaboration and seamless development processes.</h1>
      <hr>
      <div class="third_screen__texts df">
        <p data-aos="fade-right">things i can help you with...</p>
        <ul class="third_screen__texts_ul" data-aos="fade-down">
          <li>I HAVE A PASSION FOR HELPING SMALL BUSINESSES PROVIDE THEIR CLIENTS WITH THE BEST WEB
            EXPERIENCES. SPECIALIZING IN CRAFTING UNIQUE, FUNCTIONAL, AND AESTHETICALLY PLEASING WEBSITES, I AM DEDICATED TO BRINGING YOUR IDEAS INTO THE DIGITAL ERA.</li>
          <li>LET'S COLLABORATE TO TRANSFORM YOUR VISION INTO A CUTTING-EDGE ONLINE PRESENCE, USHERING YOUR BUSINESS INTO THE MODERN DIGITAL ERA WITH STYLE AND INNOVATION</li>
        </ul>
        <ul  data-aos="fade-left">
          <li><a href="https://github.com/abdulhafiz7156" target="_blank">GIthub</a></li>
          <li><a href="https://t.me/abdulhafiz_dev" target="_blank">Telegram</a></li>
          <li><a href="https://mail.google.com/mail/mu/mp/694/" target="_blank" title="xxafiz69@gmail.com">email</a></li>
        </ul>
      </div>
    </section>
    <section id="works" class="fourth__screen">
      <div class="fourth__screen__container">
        <p>selected works</p>
        <div class="fourth__screen__works df">
          <div  data-aos="fade-right" @click="link('https://gis-mining.ru/')" class="fourth__screen__work">
            <div class="fourth__screen__work__img df_jcc_aic">
              <img src="./assets/gis-ming.png" alt="">
            </div>
            <div class="fourth__screen__work__text">
              <h3>Gis Ming</h3>
              <p>Web development</p>
            </div>
          </div>
          <div  data-aos="fade-left" @click="link('https://gremir.ru/')" class="fourth__screen__work">
            <div class="fourth__screen__work__img fourth__screen__work__img2 df_jcc_aic">
              <img src="./assets/gremir.png" alt="">
            </div>
            <div class="fourth__screen__work__text">
              <h3>GREMIR.RU</h3>
              <p>Web development</p>
            </div>
          </div>
          <div  data-aos="fade-right" @click="link('https://flats-moscow.netlify.app/invest-pro-bussines.tilda.ws/index.html')" class="fourth__screen__work">
            <div class="fourth__screen__work__img fourth__screen__work__img3 df_jcc_aic">
              <img src="./assets/moscow.png" alt="">
            </div>
            <div class="fourth__screen__work__text">
              <h3>MOSCOW new building</h3>
              <p>Web development</p>
            </div>
          </div>
          <div  data-aos="fade-left" @click="link('https://plastic-clinic.net/')" class="fourth__screen__work">
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
    <section id="services" class="fifth__screen">
      <div class="fifth__screen__text">
        <p  data-aos="fade-up">how i work</p>
        <h1  data-aos="fade-right">Having thrived as a freelance front-end developer for over a year, I've cultivated invaluable expertise across a spectrum of platforms and technologies. From Bitrix to Tilda.  Let's collaborate to transform your digital aspirations into reality, drawing from my rich tapestry of experience to craft bespoke solutions that leave a lasting impact! </h1>
      </div>
      <div class="fifth__screen__faqs">
        <div  data-aos="fade-up" class="fifth__screen__faq df">
          <p>01</p>
          <p>research and planning</p>
          <p>Dive into client requirements, conduct thorough research, and strategize to outline a roadmap for project development.</p>
        </div>
        <div  data-aos="fade-up" class="fifth__screen__faq df">
          <p>02</p>
          <p>Wireframing and Prototyping</p>
          <p>Translate ideas into wireframes and interactive prototypes, refining designs based on user feedback and iterative improvements..</p>
        </div>
        <div  data-aos="fade-up" class="fifth__screen__faq df">
          <p>03</p>
          <p>Design and Development</p>
          <p>Bring designs to life with clean, efficient code, ensuring seamless functionality and optimal user experience across various devices and platforms.</p>
        </div>
        <div  data-aos="fade-up" class="fifth__screen__faq df">
          <p>04</p>
          <p>Testing and Refinement</p>
          <p>Rigorously test the developed applications, debugging and fine-tuning to enhance performance and usability.</p>
        </div>
        <div  data-aos="fade-up" class="fifth__screen__faq df">
          <p>05</p>
          <p>Handover and Support</p>
          <p>Provide comprehensive documentation, conduct client training sessions, and offer ongoing support to ensure smooth operation and maintenance of the developed solutions.</p>
        </div>
      </div>
    </section>
    <section id="contacts" class="contacts__screen df">
      <div class="contacts__screen__text">
        <p data-aos="fade-down">are you interest in collaborating to elevate your brand in the digital era? <br> let's get to work</p>
        <a href="">xxafiz69@gmail.com</a>
      </div>
      <div class="contacts__screen__link df">
        <ul data-aos="fade-down">
          <li><span>navigation</span></li>
          <li><a href="#first__screen">about</a></li>
          <li><a href="#works">work</a></li>
          <li><a href="#services">services</a></li>
        </ul>
        <ul data-aos="fade-down">
          <li><span>socials</span></li>
          <li><a href="https://t.me/abdulhafiz_dev" target="_blank">telegram</a></li>
          <li><a href="https://www.instagram.com/abdulhaf1z_dev/"  target="_blank">instagram</a></li>
          <li><a href="https://www.linkedin.com/in/abdulhafiz-hoshimov-09366a268/" target="_blank">linkedin</a></li>
        </ul>
        <ul data-aos="fade-down">
          <li><span>resources</span></li>
          <li><a href="https://github.com/abdulhafiz7156" target="_blank">Github</a></li>
          <li><a href="https://hh.ru"  target="_blank" title="Abdulhafiz Hoshimov Obidjonovich">hh.ru</a></li>
          <li><a href="https://www.codewars.com/users/xxafiz" target="_blank">codewars</a></li>
        </ul>
      </div>
    </section>
    <section class="footer__screen">
      <div class="footer__screen__h1">
        <h1 data-aos="zoom-in-up">drop me a line</h1>
      </div>
      <hr>
      <ul class="df">
        <li>©	hoshimov abdulhafiz</li>
        <li>Uzbekistan (GMT +5)</li>
        <li><a href="#first__screen">back to top</a></li>
        <li>©2024 all rights reserved</li>
      </ul>
      <hr>
    </section>
  </main>
</template>
