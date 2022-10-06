<template>
  <v-app>
    <v-app-bar title="ThirtySix">
      <v-btn icon="mdi-fast-forward mdi-rotate-180" @click="prevSet"></v-btn>
      <v-btn icon="mdi-play mdi-rotate-180" @click="questionIndex > 0 && questionIndex--"></v-btn>
      <v-btn icon="mdi-play" @click="questionIndex < sets[setIndex].length - 1 && questionIndex++"></v-btn>
      <v-btn icon="mdi-fast-forward" @click="nextSet"></v-btn>
    </v-app-bar>

    <v-main>
      <v-container class="background-image-outer">
        <v-container
          class="background-image"
          :style="{ backgroundImage: 'url(\'images/' + setBackgrounds[setIndex] + '\')' }"
        >
          <v-card
            class="mx-auto my-16"
            max-width="480"
            v-if="sets[setIndex][questionIndex]"
            :title="`Set ${setNumberNames[setIndex]}`"
            :subtitle="`Question ${questionIndex + 1}`"
          >
            <v-card-text>
              <p class="text-h5 text--primary">
                {{ sets[setIndex][questionIndex] }}
              </p>
            </v-card-text>
          </v-card>
        </v-container>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
function shuffle(array) {
  let currentIndex = array.length,
    randomIndex;

  // While there remain elements to shuffle.
  while (currentIndex !== 0) {
    // Pick a remaining element.
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex--;

    // And swap it with the current element.
    [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
  }

  return array;
}

const setBackgrounds = shuffle([
  "alvin-mahmudov-PSw1Ju18Rf4-unsplash-xs.jpg",
  "atharva-dharmadhikari-XnH8c4so-wE-unsplash-xs.jpg",
  "clay-banks-fqgt7A43-K0-unsplash-xs.jpg",
  "gaspar-zaldo-Z9NAI0mf1KA-unsplash-xs.jpg",
  "heather-mount-8c3zjKrkkBA-unsplash-xs.jpg",
  "jacob-rank-pGKyqck99cg-unsplash-xs.jpg",
  "jonathan-borba-KvMBOln0_u8-unsplash-xs.jpg",
  "kenny-eliason-n2VvngfbXtU-unsplash-xs.jpg",
  "margarida-afonso-AkbqqbAV1lU-unsplash-xs.jpg",
  "morgan-sessions-6fDYNGgjqpM-unsplash-xs.jpg",
  "sandy-millar-JQlZccfmCgQ-unsplash-xs.jpg",
  "scott-broome-BcVvVvqiCGA-unsplash-xs.jpg",
  "tim-mossholder-EgAduzpSvdE-unsplash-xs.jpg",
]).slice(0, 3);

const setNumberNames = ["One", "Two", "Three"];

const sets = [
  shuffle([
    "Given the choice of anyone in the world, whom would you want as a dinner guest?",
    "Would you like to be famous? In what way?",
    "Before making a telephone call, do you ever rehearse what you are going to say? Why?",
    "What would constitute a “perfect” day for you?",
    "When did you last sing to yourself? To someone else?",
    "If you were able to live to the age of 90 and retain either the mind or body of a 30-year-old for the last 60 years of your life, which would you want?",
    "Do you have a secret hunch about how you will die?",
    "Name three things you and your partner appear to have in common.",
    "For what in your life do you feel most grateful?",
    " If you could change anything about the way you were raised, what would it be?",
    " Take four minutes and tell your partner your life story in as much detail as possible.",
    " If you could wake up tomorrow having gained any one quality or ability, what would it be?",
  ]),
  shuffle([
    "If a crystal ball could tell you the truth about yourself, your life, the future or anything else, what would you want to know?",
    "Is there something that you’ve dreamed of doing for a long time? Why haven’t you done it?",
    "What is the greatest accomplishment of your life?",
    "What do you value most in a friendship?",
    "What is your most treasured memory?",
    "What is your most terrible memory?",
    "If you knew that in one year you would die suddenly, would you change anything about the way you are now living? Why?",
    "What does friendship mean to you?",
    "What roles do love and affection play in your life?",
    "Alternate sharing something you consider a positive characteristic of your partner. Share a total of five items.",
    "How close and warm is your family? Do you feel your childhood was happier than most other people’s?",
    "How do you feel about your relationship with your mother?",
  ]),
  shuffle([
    "Make three true “we” statements each. For instance, “We are both in this room feeling ... “",
    "Complete this sentence: “I wish I had someone with whom I could share ... “",
    "If you were going to become a close friend with your partner, please share what would be important for him or her to know.",
    "Tell your partner what you like about them; be very honest this time, saying things that you might not say to someone you’ve just met.",
    "Share with your partner an embarrassing moment in your life.",
    "When did you last cry in front of another person? By yourself?",
    "Tell your partner something that you like about them already.",
    "What, if anything, is too serious to be joked about?",
    "If you were to die this evening with no opportunity to communicate with anyone, what would you most regret not having told someone? Why haven’t you told them yet?",
    "Your house, containing everything you own, catches fire. After saving your loved ones and pets, you have time to safely make a final dash to save any one item. What would it be? Why?",
    "Of all the people in your family, whose death would you find most disturbing? Why?",
    "Share a personal problem and ask your partner’s advice on how he or she might handle it. Also, ask your partner to reflect back to you how you seem to be feeling about the problem you have chosen.",
  ]),
];

export default {
  name: "App",
  methods: {
    prevSet() {
      if (this.setIndex > 0) {
        this.setIndex--;
        this.questionIndex = 0;
      }
    },
    nextSet() {
      if (this.setIndex < this.sets.length - 1) {
        this.setIndex++;
        this.questionIndex = 0;
      }
    },
  },
  data() {
    return {
      setIndex: 0,
      questionIndex: 0,
      sets,
      setNumberNames,
      setBackgrounds,
    };
  },
};
</script>

<style>
html {
  overflow: hidden !important;
}
.v-application.v-layout {
  background: radial-gradient(circle, rgba(121, 43, 129, 1) 0%, rgba(121, 37, 37, 1) 100%);
}
.v-app-bar,
.v-card {
  opacity: 0.85;
}
.background-image-outer {
  height: 100%;
  max-width: 960px;
}
.background-image-outer.v-container {
  padding: 0;
}
.background-image {
  height: 100%;
  background-position: center top;
  background-size: 960px auto;
  background-repeat: no-repeat;
  background-attachment: fixed;
}
@media (max-width: 960px) {
  .background-image {
    background-size: auto auto;
  }
}
* {
  touch-action: none;
  pointer-events: none;
}
input,
button,
a {
  pointer-events: auto;
}
</style>
