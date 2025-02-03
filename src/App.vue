<script setup>
import "./assets/main.css";
import { onMounted } from "vue";
import Vara from "vara";

const photo1 = new URL("/src/assets/photo1.png", import.meta.url).href;
const photo2 = new URL("/src/assets/photo2.png", import.meta.url).href;
const photo3 = new URL("/src/assets/photo3.png", import.meta.url).href;

onMounted(() => {
  var SatisfySL =
    "https://rawcdn.githack.com/akzhy/Vara/ed6ab92fdf196596266ae76867c415fa659eb348/fonts/Satisfy/SatisfySL.json";
  var winWidth = window.innerWidth;
  var ratio = winWidth / 1920;
  var fontSize = {
    small: 12,
    medium: 14,
  };
  var played = [0, 0, 0];
  var vara = [];
  var bodyFontSize = Math.max(16 * ratio, 10);
  var posX = Math.max(80 * ratio, 50);
  document.body.style.fontSize = bodyFontSize + "px";

  fontSize.small = Math.max(fontSize.small * ratio, winWidth < 700 ? 10 : 8);
  fontSize.medium = Math.max(fontSize.medium * ratio, winWidth < 700 ? 12 : 10);

  vara[0] = new Vara(
    "#vara-container",
    SatisfySL,
    [
      {
        text: "6 Jun 2021",
        textAlign: "right",
        y: 20,
        x: winWidth < 700 ? -30 : -50,
        delay: 500,
        duration: 1500,
        fontSize: fontSize.small,
      },
      {
        text: "Our story began when we met in a camping 4 years ago..",
        y: 40,
        x: posX,
        duration: 4000,
      },
      {
        text: "That day marked our destiny..",
        id: "sphinx",
        x: posX,
        y: 20,
        delay: 1000,
        duration: 4500,
      },
    ],
    {
      strokeWidth: 2,
      fontSize: fontSize.medium,
      autoAnimation: false,
    }
  );

  vara[1] = new Vara(
    "#vara-container2",
    SatisfySL,
    [
      {
        text: "6 Jun 2021 -> Today",
        textAlign: "right",
        delay: 500,
        y: 20,
        x: winWidth < 700 ? -30 : -50,
        duration: 1500,
        fontSize: fontSize.small,
      },
      {
        text: "...and since that day, we were inseparable soulmates..",
        y: 40,
        x: posX,
        duration: 4000,
      },
      {
        text: "and here comes a new milestone in our adventure..",
        y: 20,
        x: posX,
        duration: 3500,
      },
    ],
    {
      strokeWidth: 2,
      fontSize: fontSize.medium,
      autoAnimation: false,
    }
  );

  vara[2] = new Vara(
    "#vara-container3",
    SatisfySL,
    [
      {
        text: "9 Apr 2025",
        textAlign: "right",
        delay: 500,
        y: 20,
        x: winWidth < 700 ? -30 : -50,
        duration: 1500,
        fontSize: fontSize.small,
      },
      { text: "We're getting married!", y: 30, x: posX, duration: 4000 },
      {
        text: "April 9th, 2025   5pm",
        y: 20,
        x: posX,
        color: "#d62626",
        duration: 3500,
      },
      {
        text: "Marassim wedding hall, Teniour km  10, Sfax, Tunisia",
        y: 20,
        x: posX,
        duration: 3500,
      },
      {
        text: "Save the date!",
        y: 20,
        x: posX,
        color: "#d62626",
        duration: 3500,
      },
    ],
    {
      strokeWidth: 2,
      fontSize: fontSize.medium,
      autoAnimation: false,
    }
  );

  vara[2].ready(function () {
    document.querySelectorAll(".front:not(.last)").forEach((element) => {
      element.addEventListener("click", function () {
        var ix = Array.from(
          element.closest(".paper").parentNode.children
        ).indexOf(element.closest(".paper"));
        document.querySelector(".book").classList.add("open");
        element.closest(".paper").classList.add("open");
        if (!played[ix]) {
          vara[ix].playAll();
          vara[ix].animationEnd(function (i, o) {
            played[ix] = 1;
            if (i == "link") {
              var group = o.container;
              var rect = document.createElementNS(
                "http://www.w3.org/2000/svg",
                "rect"
              );
              rect.setAttribute("x", 0);
              rect.setAttribute("y", 0);
              rect.setAttribute(
                "width",
                o.container.getBoundingClientRect().width
              );
              rect.setAttribute(
                "height",
                o.container.getBoundingClientRect().height
              );
              rect.setAttribute("fill", "transparent");
              group.appendChild(rect);
              rect.style.cursor = "pointer";
              rect.addEventListener("click", function () {
                console.log(true);
                document.querySelector("#link").click();
              });
            }
          });
        }
      });
    });

    document.querySelectorAll(".back").forEach((element) => {
      element.addEventListener("click", function () {
        var parentPaper = element.closest(".paper");
        if (
          Array.from(parentPaper.parentNode.children).indexOf(parentPaper) === 0
        ) {
          document.querySelector(".book").classList.remove("open");
        }
        parentPaper.classList.remove("open");
      });
    });
  });
});
</script>

<template>
  <div class="v-center"></div>
  <div id="container">
    <div class="book">
      <div class="first paper">
        <div class="page front contents">
          <div class="intro">
            <h2>Feres</h2>
            <h2>& Nermine</h2>
            <h1>👰‍♀️🤵🏻</h1>
            <h2 class="save-the-date">Save the</h2>
            <h2 class="save-the-date">date <span class="ring">💍</span></h2>
          </div>
        </div>
        <div class="page back">
          <div class="page-back-photo">
            <img :src="photo1" />
          </div>
        </div>
      </div>
      <div class="second paper">
        <div class="page front contents">
          <div id="vara-container"></div>
        </div>
        <div class="page back">
          <div class="page-back-photo">
            <img :src="photo2" />
          </div>
        </div>
      </div>
      <div class="third paper">
        <div class="page front contents">
          <div id="vara-container2"></div>
        </div>
        <div class="page back">
          <div class="page-back-photo">
            <img :src="photo3" />
          </div>
        </div>
      </div>
      <div class="fourth paper">
        <div class="page last front contents">
          <div id="vara-container3"></div>
        </div>
        <div class="page back">
          <div class="page-back-photo">
            <img
              src="https://www.dottyaboutpaper.co.uk/cdn/shop/articles/couple-holding-wedding-bouquet-scaled_1024x1024.jpg?v=1694339675"
            />
          </div>
        </div>
      </div>
      <div class="side"></div>
      <div class="bottom"></div>
      <div class="shadow"></div>
    </div>
  </div>
</template>
