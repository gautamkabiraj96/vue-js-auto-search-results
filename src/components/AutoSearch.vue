<template>
  <div>
    <div style="width: 400px; display: inline-block !important">
      <div class="np-title">The Big Bang Theory Characters</div>
      <div style="width: 100%">
        <div class="auto-search-container">
          <input
            type="text"
            class="np-input-search"
            v-model="inputSearchText"
            placeholder="Search names"
            autocomplete="off"
            v-on:keyup="searchNames"
          />
        </div>
      </div>
      <div class="np-result-container">
        <div v-if="filteredResult.length > 0">
          <div
            v-for="(result, resultIndex) in filteredResult"
            :key="resultIndex"
          >
            <div class="np-result-item" @click="showCharacterDetails(result)">
              <div class="np-ib" style="width: 50px">
                <img :src="result.url" class="np-avatar" />
              </div>
              <div class="np-ib np-text-container">
                <div>
                  {{ result.name }}
                </div>
                <div class="np-result-description">
                  {{ result.description }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div
      class="np-details"
      style="width: 500px; display: inline-block !important"
      v-if="characterDetails != null"
    >
      <div v-if="characterDetails != null">
        <div>
          <img :src="characterDetails.url" class="np-result-details-img" />
        </div>
        <div class="np-result-details-title">
          {{ characterDetails.name }}
        </div>
        <div class="np-result-details-description">
          {{ characterDetails.description }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AutoSearchMenu",
  data() {
    return {
      inputSearchText: "",
      filteredResult: [],
      characterDetails: null,
      characterNames: [
        {
          id: 1,
          name: "Penny",
          description: "Blonde, Cheese cake factory, Cow boy family background",
          url: "https://i.imgur.com/GX6QGer.jpg",
        },
        {
          id: 2,
          name: "Leonard",
          description:
            "Single child, geek, experimental physicist, short height",
          url: "https://i.imgur.com/FraeGOM.jpg",
        },
        {
          id: 3,
          name: "Howard Wolowitz",
          description: "Mamas boy, pervert, MIT engineer",
          url: "https://i.imgur.com/59Dpc9Y.jpg",
        },
        {
          id: 4,
          name: "Sheldon Cooper",
          description: "Theoretical physicist, robot, prodigy",
          url: "https://i.imgur.com/Zl4xMhM.jpg",
        },
        {
          id: 5,
          name: "Rajesh Koothrapali",
          description:
            "Forever single, astrophysicist, selective mutism, indian",
          url: "https://i.imgur.com/Vqmoy0O.jpg",
        },
      ],
    };
  },
  methods: {
    searchNames() {
      this.filteredResult = [];
      this.characterDetails = null;
      if (
        this.inputSearchText == null ||
        (this.inputSearchText != null && this.inputSearchText.length === 0)
      ) {
        this.filteredResult = [];
        this.characterDetails = null;
      } else {
        if (
          this.characterNames &&
          this.characterNames.length > 0 &&
          this.inputSearchText.length >= 2
        ) {
          this.characterNames.forEach((character) => {
            const searchHasCharacterName =
              character.name &&
              character.name
                .toLowerCase()
                .includes(this.inputSearchText.toLowerCase());
            const searchHasCharacterDescription =
              character.description &&
              character.description
                .toLowerCase()
                .includes(this.inputSearchText.toLowerCase());
            if (searchHasCharacterName || searchHasCharacterDescription) {
              this.filteredResult.push(character);
            }
          });
        }
      }
    },
    showCharacterDetails(result) {
      this.characterDetails = result;
    },
  },
};
</script>

<style scoped>
.np-title {
  margin-left: 20px;
  margin-top: 30px;
  font-size: 18px;
  color: rgb(0, 64, 255);
}
.auto-search-container {
  background: #ffffff;
  width: 300px;
  margin-top: 30px;
  z-index: 9999;
  font-size: 24px;
  height: 44px;
  padding: 0px 14px;
}
.np-input-search {
  width: 300px;
  height: 22px;
  padding: 12px 28px;
  background: #eee;
  font-size: 18px;
  border: 1px solid #eee;
  border-radius: 32px;
  transition: all 0.3s;
  outline: none;
}
.np-input-search:hover {
  background: rgb(225, 225, 225);
  transition: all 0.4s;
}
.np-result-container {
  margin-top: 30px;
  margin-left: 18px;
  text-align: left;
}
.np-result-item {
  width: 320px;
  border: 1px solid #eee;
  border-radius: 12px;
  margin-bottom: 12px;
  padding: 12px 14px;
  cursor: pointer;
  transition: all 0.3s;
}
.np-result-item:hover {
  background: #eee;
  transition: all 0.3s;
}
.np-result-description {
  font-size: 11px;
}
.np-ib {
  display: inline-block;
}
.np-avatar {
  height: 50px;
  border-radius: 12px;
}
.np-text-container {
  width: 180px;
  vertical-align: top;
  padding-left: 20px;
}
.np-details {
  vertical-align: top;
  border: 1px solid #eee;
  border-radius: 12px;
  margin-bottom: 12px;
  margin-left: 20px;
  margin-top: 30px;
  padding: 12px 14px;
  height: 400px;
}
.np-result-details-img {
  border-radius: 12px;
  height: 250px;
}
.np-result-details-title {
  font-size: 20px;
  padding: 8px 0px;
  font-weight: 500;
}
.np-result-details-description {
  font-size: 16px;
}
</style>