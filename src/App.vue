<template>
  <v-app>
    <v-app-bar title="Moral Quarrel">
      <v-btn icon="mdi-play mdi-rotate-180" @click="backClick"></v-btn>
      <v-btn icon="mdi-play" @click="forwardClick"></v-btn>
      <v-btn icon="mdi-scale-balance" @click="finishClick"></v-btn>
    </v-app-bar>

    <v-main>
      <v-container class="background-image-outer">
        <v-card class="mx-auto my-16" max-width="480" v-if="!showFinish">
          <v-card-text>
            <p class="text-h5 text--primary">
              {{ cards[cardIndex].text }}
            </p>
            <br />
            <p
              class="text-h6 text--primary"
              v-for="(choice, choiceIndex) in cards[cardIndex].choices"
              :key="choiceIndex"
            >
              {{ choiceNames[choiceIndex] + ") " + choice.text }}
            </p>
          </v-card-text>
          <v-card-actions>
            <v-btn @click="pickChoice(cards[cardIndex].choices[0])">Pick {{ choiceNames[0] }}</v-btn>
            <v-btn @click="pickChoice(cards[cardIndex].choices[1])">Pick {{ choiceNames[1] }}</v-btn>
          </v-card-actions>
        </v-card>
        <v-card class="mx-auto my-16" max-width="480" v-else>
          <v-card-text>
            <p class="text-h5 text--primary">Finished</p>
            <br />
            <p class="text-h6 text--primary" v-for="(choice, choiceIndex) in this.choices" :key="choiceIndex">
              {{ choice.text }}
            </p>
          </v-card-text>
        </v-card>
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

const choiceNames = ["A", "B"];
const cards = shuffle([
  {
    text: "A magical genie offers you one of two very specific wishes. A, you can live one life that lasts 1000 years, or B, you can live ten lives that last 100 years. Which do you choose?",
    choices: shuffle([
      { text: "You can live one life that lasts 1000 years", isThoughtful: true },
      { text: "You can live ten lives that last 100 years", isPlayful: true },
    ]),
  },
  {
    text: "You are a Royal Guard on the lookout for an evil sorcerer that has been terrorizing villagers. When you finally apprehend this sorcerer you discover he is Charles, your childhood best friend. Do you...",
    choices: shuffle([
      { text: "Throw your friend in the castle dungeon", isThoughtful: true },
      { text: "Tell Charles to leave town, and never return", isPlayful: true },
    ]),
  },
  {
    text: "Would you rather...",
    choices: shuffle([
      { text: "Have a pet dragon", isThoughtful: true },
      { text: "Be a dragon", isPlayful: true },
    ]),
  },
  {
    text: "Would you rather...",
    choices: shuffle([
      { text: "Have noodles for hands that don't allow you to pick up anything", isThoughtful: true },
      { text: "Have a tail that never stops loudly tapping against the ground", isPlayful: true },
    ]),
  },
  {
    text: "Would you rather...",
    choices: shuffle([
      { text: "Constantly reek of syrup and not smell it", isThoughtful: true },
      { text: "Constantly smell reeking syrup", isPlayful: true },
    ]),
  },
  {
    text: "A rich merchant inadvertently drops one shiny, gold coin on the ground. You see a poor, hungry orphan pick it you. Do you...",
    choices: shuffle([
      { text: "Convince the orphan to be honest and return the coin", isThoughtful: true },
      { text: "Turn your head the other way and let the orphan keep the coin", isPlayful: true },
    ]),
  },
  {
    text: "You have been hunting for your starving family all day and only managed to catch a small goose. On your way back home, a hungry beggar offers you magic beans in return for the goose. The beggar tells you that the beanstalk that sprouts from his beans will lead you to a chest that produces unlimited food. He would go after it himself, but his legs are too tired and old. Do you...",
    choices: shuffle([
      { text: "Kindly reject the offer and bring your starving family their dinner", isThoughtful: true },
      { text: "Let the beggar eat the goose, and plant the beans in your yard", isPlayful: true },
    ]),
  },
  {
    text: "You are the kingdom's wizard doctor. In the middle of the night, an honorable knight and a despicable thief arrive at your door. The thief's injuries are much more severe than the knight's. Do you...",
    choices: shuffle([
      { text: "Heal the thief first", isThoughtful: true },
      { text: "Heal the knight first", isPlayful: true },
    ]),
  },
  {
    text: "You are poor, and a thief pickpockets your only coin, forcing you to go hungry for the night. A few days later you see the same thief get robbed of his dinner by two bandits. You chase after the bandits and get back the stolen food. Do you...",
    choices: shuffle([
      { text: "Keep the food, teaching the thief a lesson", isThoughtful: true },
      { text: "Return the food to the thief", isPlayful: true },
    ]),
  },
  {
    text: "Your best friend is planning to marry the love of their life. On the day of the wedding, you discover that their fiancé is a gremlin, using a magic spell to disguise themselves as a human. The gremlin assures you it loves your friend, and begs you to keep their secret. Do you...",
    choices: shuffle([
      { text: "Tell your friend anyway", isThoughtful: true },
      { text: "Keep their secret", isPlayful: true },
    ]),
  },
  {
    text: "You have a job you love as the Royal Love Doctor, but during an appointment, your best friend's husband admits to you that he is in love with another woman. Do you...",
    choices: shuffle([
      { text: "Break the confidentiality policy and tell your friend, potentially getting fired?", isThoughtful: true },
      {
        text: "Advise the man to go back to his wife and hope your friend does not find out you knew he had eyes for another?",
        isPlayful: true,
      },
    ]),
  },
]);

export default {
  name: "App",
  methods: {
    backClick() {
      if (this.cardIndex > 0) {
        this.cardIndex--;
      }
    },
    forwardClick() {
      const lastIndex = this.cards.length - 1;
      if (this.cardIndex === lastIndex) {
        this.showFinish = true;
        return;
      }
      if (this.cardIndex < lastIndex) {
        this.cardIndex++;
      }
    },
    finishClick() {
      this.showFinish = true;
    },
    pickChoice(choice) {
      this.choices.push(choice);
      this.forwardClick();
    },
  },
  data() {
    return {
      showFinish: false,
      cardIndex: 0,
      cards,
      choiceNames,
      choices: [],
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
