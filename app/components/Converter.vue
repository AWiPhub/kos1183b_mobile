<template>
  <Page class="page">
    <ActionBar title="Конвертер" class="action-bar">
      <NavigationButton
        text="Назад"
        android.systemIcon="ic_menu_back"
        @tap="goBack"
      />
    </ActionBar>
    <ScrollView>
      <GridLayout columns="180, 180" rows="180, 180, 180">
        <FlexboxLayout
          flexDirection="column"
          justifyContent="center"
          alignItems="center"
          class="converterType"
          row="0"
          col="0"
          @tap="goTo('measure')"
        >
          <Image
            class="iconConverter"
            src="~/assets/icons/measure.png"
            alignSelf="center"
            stretch="aspectFill"
          />
          <Label> Длина и расстояние </Label>
        </FlexboxLayout>
        <FlexboxLayout
          flexDirection="column"
          justifyContent="center"
          alignItems="center"
          class="converterType"
          row="0"
          col="1"
          @tap="goTo('temp')"
        >
          <Image
            class="iconConverter"
            src="~/assets/icons/temperature.png"
            stretch="aspectFill"
            alignSelf="center"
          />
          <Label> Температура </Label>
        </FlexboxLayout>
        <FlexboxLayout
          flexDirection="column"
          justifyContent="center"
          alignItems="center"
          class="converterType"
          row="1"
          col="0"
          @tap="goTo('binary')"
        >
          <Image
            class="iconConverter"
            src="~/assets/icons/binary.png"
            stretch="aspectFill"
            alignSelf="center"
          />
          <Label textWrap> Единицы хранения цифровой информации </Label>
        </FlexboxLayout>
        <FlexboxLayout
          flexDirection="column"
          justifyContent="center"
          alignItems="center"
          class="converterType"
          row="1"
          col="1"
          @tap="goTo('color')"
        >
          <Image
            class="iconConverter"
            src="~/assets/icons/color.png"
            stretch="aspectFill"
            alignSelf="center"
          />
          <Label> HEX, RGB </Label>
        </FlexboxLayout>
        <FlexboxLayout
          flexDirection="column"
          justifyContent="center"
          alignItems="center"
          class="converterType"
          colSpan="2"
          row="2"
          col="0"
          @tap="goTo('money')"
        >
          <Image
            class="iconConverter"
            src="~/assets/icons/money.png"
            stretch="aspectFill"
            alignSelf="center"
          />
          <Label> Валюта </Label>
        </FlexboxLayout>
      </GridLayout>
    </ScrollView>
  </Page>
</template>

<script>
import Home from "./Home.vue";

import Measure from "./converterTypes/measure.vue";
import Temp from "./converterTypes/temp.vue";
import Binary from "./converterTypes/binary.vue";
import Color from "./converterTypes/color.vue";
import Money from "./converterTypes/money.vue";

export default {
  name: "Converter",
  methods: {
    goTo(place) {
      switch (place) {
        case "measure":
          this.$navigateTo(Measure);
          break;
        case "temp":
          this.$navigateTo(Temp);
          break;
        case "binary":
          this.$navigateTo(Binary);
          break;
        case "color":
          this.$navigateTo(Color);
          break;
        case "money":
          this.$navigateTo(Money);
          break;
      }
    },
    goBack() {
      this.$navigateTo(Home);
    },
  },

  data() {
    return {};
  },
};
</script>

<style>
.converterType {
  margin: 50px;
  background-color: #3c3c3c;
  text-align: center;
  font-size: 12px;
}
.iconConverter {
  width: 190px;
  height: 190px;
  margin-bottom: 30px;
}
</style>
