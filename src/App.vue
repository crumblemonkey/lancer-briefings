<template>
  <Header :header="this.header" />
  <div class="content-container">
    <section class="section-container" id="missions" style="width:22.87vw; height:78.46vh; min-width:300px; min-height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/mission-icon.svg" />
        <h1>Mission Log</h1>
      </div>
      <div class="section-content-container">
        <h3>Current Assignment</h3>
        <Markdown :source="current_md" class="markdown" />
        <h3>Mission List</h3>
        <div class="mission-list-container">
          <Mission
            v-for="item in this.missions"
            :key="item.slug"
            :mission="item"
            :selected="this.mission_slug"
            @click="selectMission(item)"
          />
        </div>
      </div>
    </section>
    <section class="section-container" id="events" style="width:22.87vw; height:78.46vh; min-width:300px; min-height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/events-icon.svg" />
        <h1>Events Log</h1>
      </div>
      <div class="section-content-container">
        <Markdown :source="events" class="markdown" />
      </div>
    </section>
    <section class="section-container" id="pilots" style="width:37vw; height:78.46vh; min-width:600px; min-height:714px; max-width:850px;">
    <div style="height:52px; overflow:hidden;">
        <div class="section-header clipped-medium-backward-pilot">
          <img src="/icons/pilot-icon.svg" />
          <h1>Pilot Roster</h1>
        </div>
        <div class="rhombus-back">&nbsp;</div>
	</div>
      <div class="section-content-container">
        <div class="pilot-list-container">
          <Pilot v-for="item in this.pilots" :key="item.slug" :pilot="item" />
        </div>
      </div>
    </section>
  </div>
  <svg
    style="visibility: hidden; position: absolute;"
    width="0"
    height="0"
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
  >
    <defs>
      <filter id="round">
        <feGaussianBlur in="SourceGraphic" stdDeviation="5" result="blur" />
        <feColorMatrix
          in="blur"
          mode="matrix"
          values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -5"
          result="goo"
        />
        <feComposite in="SourceGraphic" in2="goo" operator="atop" />
      </filter>
    </defs>
  </svg>
  <audio autoplay>
    <source src="/startup.ogg" type="audio/ogg" />
  </audio>
  <Footer/>
</template>

<script>
import Header from './components/layout/Header.vue';
import Footer from './components/layout/Footer.vue';
import Mission from './components/Mission.vue';
import Pilot from './components/Pilot.vue';
import Markdown from 'vue3-markdown-it';

export default {
  components: {
    Header,
    Footer,
    Mission,
    Pilot,
    Markdown
  },

  data() {
    return {
      "mission_slug": "004",
      "current_md": "004",
      "events": "",
      "missions": [
          {
          "slug": "001",
          "name": "A Little Bit Damp",
          "status": "success"
        },
	    {
          "slug": "002",
          "name": "Signals Left Unsung",
          "status": "success"
        },
	    {
          "slug": "003",
          "name": "Operation Howling Blade",
          "status": "partial-success"
        },
        {
          "slug": "004",
          "name": "Exploring Astran IV",
          "status": "start"
        },
      ],
      "pilots": [
        {
          "callsign": "Mirage",
          "alias": "Avron Aubery",
          "code": "462370be-bd0f-41c2-b667-cc75f3a59a96///NDL-C-DEEP-STATION//377308ad-ba23-410b-ae37-68a1fb5f8db4",
          "corpro": "IPS-N",
          "frame": "Zheng",
          "mech": "A Gentalman Will Walk But Never Run"
        },
        {
          "callsign": "HB",
          "alias": "Honney",
          "code": "7cd700cc-c990-48ed-892f-e5468de724c4///NDL-C-DEEP-STATION//a98c3e28-ad4a-4f89-bcd9-501464e960da",
          "corpro": "SSC",
          "frame": "Everest",
          "mech": "Discord Kitten"
        },
        {
          "callsign": "Charon",
          "alias": "Kira Feldston",
          "code": "4be26ce9-923b-4069-b6c9-76437d4be455///NDL-C-DEEP-STATION//056940c6-8d55-4190-8e85-57caa043cb1a",
          "corpro": "SSC",
          "frame": "Viceroy",
          "mech": "Viceroy"
        },
	{
          "callsign": "HACKERMANS.omif",
          "alias": "Ecne",
          "code": "7fu24if8-389b-4903-u4i0-67298y3iu487///NDL-C-DEEP-STATION//492098u8-9g78-3948-9g09-890890g789ye",
          "corpro": "Horus",
          "frame": "Hydra",
          "mech": "Monsus The Battle Bus"
        },
	{
          "callsign": "Birdy",
          "alias": "Alison Rosalyn Hawk",
          "code": "5fg34gh6-n657-n6jk5-b5jg-d678s56w78e///NDL-C-DEEP-STATION//8965r579-ji75-gy75-99y9-789656d674e5",
          "corpro": "Horus",
          "frame": "Balor",
          "mech": "E.T.N.A"
        },
	{
          "callsign": "Monkey",
          "alias": "Sophia Ogawa",
          "code": "",
          "corpro": "SSC",
          "frame": "Orchis",
          "mech": "Arcturus"
        },
      ],
      "header": {
        "planet": "Astran IV",
        "year": "5014u",
        "system": "Kasdaen",
        "gate": "Hermes 329",
        "ring": "Long Rim",
        "headerTitle": "Mirrorsmoke",
        "headerSubtitle": "Mercenary Company",
        "subheaderTitle": "World's End",
        "subheaderSubtitle": "Delta-Echo-Echo-Zulu",
      },
      "options":{
        "eventsMarkdownPerMission": true
      }
    }
  },

  created() {
    this.loadMissionMarkdown()
    this.loadEventsMarkdown()
  },

  computed: {

  },

  methods: {
    selectMission(mission) {
      this.mission_slug = mission.slug;
      this.loadMissionMarkdown()
      if(this.options.eventsMarkdownPerMission){
        this.loadEventsMarkdown();
      }
    },
    loadMissionMarkdown() {
      let self = this;
      let md = `/missions/${self.mission_slug}.md`
      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.current_md = client.responseText;
      }
      client.send();
    },
    loadEventsMarkdown() {
      let self = this;
      let md = "";

      if(self.options.eventsMarkdownPerMission){
        md = `/events/${self.mission_slug}.md`
      }
      else {
        md = "/events.md"
      }

      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.events = client.responseText;
      }
      client.send();
    }
  }

}
</script>


<style lang="scss">
#app {
  width: 100vw;
  height: 100vh;
  min-width: 1300px;
  min-height: 910px;
  overflow: hidden;
}
</style>
