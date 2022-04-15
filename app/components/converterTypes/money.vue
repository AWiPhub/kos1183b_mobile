<template>
  <Page class="page">
    <ActionBar title="Валюта" class="action-bar">
      <NavigationButton
        text="Назад"
        android.systemIcon="ic_menu_back"
        @tap="goBack"
      />
    </ActionBar>
    <ScrollView>
      <FlexboxLayout flexDirection="column">
        <FlexboxLayout
          flexDirection="row"
          alignItems="center"
          justifyContent="space-around"
          style="margin-top: 25px; width: 1000px"
        >
          <FlexboxLayout flexDirection="row" justifyContent="space-between">
            <Label text="Курс Центробанка РФ" style="font-size: 12px" />
            <FlexboxLayout flexDirection="row" style="margin-left: 150px">
              <FlexboxLayout flexDirection="row" alignItems="center">
                <Image
                  class="iconWallet"
                  src="~/assets/icons/dollar.png"
                  stretch="aspectFill"
                  alignSelf="center"
                />
                <Label
                  :text="courseRUB_USD"
                  style="font-size: 12px; margin-left: 15px"
                />
              </FlexboxLayout>
              <FlexboxLayout
                flexDirection="row"
                alignItems="center"
                style="margin-left: 50px"
              >
                <Image
                  class="iconWallet"
                  src="~/assets/icons/euro.png"
                  stretch="aspectFill"
                  alignSelf="center"
                />
                <Label
                  :text="courseRUB_EUR"
                  style="font-size: 12px; margin-left: 15px"
                />
              </FlexboxLayout>
            </FlexboxLayout>
          </FlexboxLayout>
        </FlexboxLayout>

        <FlexboxLayout
          flexDirection="column"
          alignItems="center"
          justifyContent="center"
          style="margin-top: 25px"
        >
          <FlexboxLayout flexDirection="row" alignItems="center">
            <Label class="labelPicker" text="Из" />
            <ListPicker
              class="listPicker"
              v-model="selectedOut"
              :items="listOfItems"
              selectedIndex="0"
              style="width: 700px"
            />
          </FlexboxLayout>
          <FlexboxLayout flexDirection="row" alignItems="center">
            <Label class="labelPicker" text="В" />
            <ListPicker
              class="listPicker"
              v-model="selectedTo"
              :items="listOfItems"
              selectedIndex="0"
              style="width: 700px"
            />
          </FlexboxLayout>
        </FlexboxLayout>

        <FlexboxLayout
          flexDirection="row"
          justifyContent="center"
          alignItems="center"
          style="margin-top: 50px; font-size: 22px"
        >
          <Label :text="total" />
        </FlexboxLayout>

        <FlexboxLayout
          flexDirection="row"
          justifyContent="center"
          style="margin-top: 50px"
        >
          <GridLayout columns="70, 70, 70" rows="65, 65, 65, 65, 65, 65, 65">
            <label
              :text="displayField"
              row="0"
              col="0"
              colSpan="3"
              class="display"
            />

            <button
              class="kp"
              text="C"
              row="1"
              col="0"
              colSpan="2"
              @tap="clear"
            />
            <button class="kp" text="⌫" row="1" col="2" @tap="backspace" />

            <button class="kp" text="7" row="2" col="0" @tap="input('7')" />
            <button class="kp" text="8" row="2" col="1" @tap="input('8')" />
            <button class="kp" text="9" row="2" col="2" @tap="input('9')" />

            <button class="kp" text="4" row="3" col="0" @tap="input('4')" />
            <button class="kp" text="5" row="3" col="1" @tap="input('5')" />
            <button class="kp" text="6" row="3" col="2" @tap="input('6')" />

            <button class="kp" text="1" row="4" col="0" @tap="input('1')" />
            <button class="kp" text="2" row="4" col="1" @tap="input('2')" />
            <button class="kp" text="3" row="4" col="2" @tap="input('3')" />

            <button
              class="kp"
              text="0"
              row="5"
              col="0"
              colSpan="3"
              @tap="input('0')"
            />

            <button
              class="kp"
              style="font-size: 16px"
              text="Конвертировать"
              row="6"
              col="0"
              colSpan="3"
              @tap="doConvertig"
            />
          </GridLayout>
        </FlexboxLayout>
      </FlexboxLayout>
    </ScrollView>
  </Page>
</template>

<script>
import { Http } from "@nativescript/core";

import Converter from "../Converter.vue";

export default {
  name: "Calc",
  data() {
    return {
      displayField: "",
      listOfItems: [
        "Австралийский доллар",
        "Азербайджанский манат",
        "Фунт стерлинга",
        "Армянский драм",
        "Белорусский рубль",
        "Болгарский лев",
        "Бразильский реал",
        "Венгерский форинт",
        "Гонконгский доллар",
        "Датская крона",
        "Доллар США",
        "Евро",
        "Индийская рупия",
        "Казахстанский тенге",
        "Канадский доллар",
        "Киргизский сом",
        "Жэньминьби",
        "Молдавский лей",
        "Норвежская крона",
        "Польский злотый",
        "Румынский лей",
        "Сингапурский доллар",
        "Таджикский сомони",
        "Турецкая лира",
        "Туркменский манат",
        "Узбекский сум",
        "Украинская гривна",
        "Чешская крона",
        "Шведская крона",
        "Швейцарский франк",
        "Южноафриканский рэнд",
        "Южнокорейская вона",
        "Японская иена",
        "Рубль",
      ],
      displayListOfItems: [
        "AUD",
        "AZN",
        "GBP",
        "AMD",
        "BYN",
        "BGN",
        "BRL",
        "HUF",
        "HKD",
        "DKK",
        "USD",
        "EUR",
        "INR",
        "KZT",
        "CAD",
        "KGS",
        "CNY",
        "MDL",
        "NOK",
        "PLN",
        "RON",
        "SGD",
        "TJS",
        "TRY",
        "TMT",
        "UZS",
        "UAH",
        "CZK",
        "SEK",
        "CHF",
        "ZAR",
        "KRW",
        "JPY",
        "RUB",
      ],
      selectedOut: 0,
      selectedTo: 0,
      total: "",

      courseBase: undefined,
      courseRUB_USD: undefined,
      courseRUB_EUR: undefined,

      courseList: {
        AUD: undefined,
        AZN: undefined,
        GBP: undefined,
        AMD: undefined,
        BYN: undefined,
        BGN: undefined,
        BRL: undefined,
        HUF: undefined,
        HKD: undefined,
        DKK: undefined,
        USD: undefined,
        EUR: undefined,
        INR: undefined,
        KZT: undefined,
        CAD: undefined,
        KGS: undefined,
        CNY: undefined,
        MDL: undefined,
        NOK: undefined,
        PLN: undefined,
        RON: undefined,
        SGD: undefined,
        TJS: undefined,
        TRY: undefined,
        TMT: undefined,
        UZS: undefined,
        UAH: undefined,
        CZK: undefined,
        SEK: undefined,
        CHF: undefined,
        ZAR: undefined,
        KRW: undefined,
        JPY: undefined,
        RUB: undefined,
      },
    };
  },
  methods: {
    input(key) {
      if (["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"].includes(key)) {
        this.displayField += key;
      }
    },
    backspace() {
      this.displayField = this.displayField.substr(
        0,
        this.displayField.length - 1
      );
    },
    clear() {
      this.displayField = "";
    },
    goBack() {
      this.$navigateTo(Converter);
    },
    doConvertig() {
      const price = Number(
        Number(this.courseList[this.selectedToText]) /
          Number(this.courseList[this.selectedOutText])
      ).toFixed(2);
      this.total = `${this.displayField} ${this.selectedOutText} = ${price} ${this.selectedToText}`;
    },
  },
  computed: {
    viewSelectedOut: function () {
      return this.listOfItems[this.selectedOut];
    },
    selectedOutText: function () {
      return this.displayListOfItems[this.selectedOut];
    },
    selectedToText: function () {
      return this.displayListOfItems[this.selectedTo];
    },
  },
  mounted() {
    Http.getJSON(`https://cdn.cur.su/api/cbr.json`).then((res) => {
      this.courseBase = JSON.parse(JSON.stringify(res.base));
      this.courseRUB_USD = (
        Number(JSON.parse(JSON.stringify(res.rates.RUB))) /
        Number(JSON.parse(JSON.stringify(res.rates.USD)))
      ).toFixed(2);
      this.courseRUB_EUR = (
        Number(JSON.parse(JSON.stringify(res.rates.RUB))) /
        Number(JSON.parse(JSON.stringify(res.rates.EUR)))
      ).toFixed(2);

      this.courseList.AUD = JSON.parse(JSON.stringify(res.rates.AUD));
      this.courseList.AZN = JSON.parse(JSON.stringify(res.rates.AZN));
      this.courseList.GBP = JSON.parse(JSON.stringify(res.rates.GBP));
      this.courseList.AMD = JSON.parse(JSON.stringify(res.rates.AMD));
      this.courseList.BYN = JSON.parse(JSON.stringify(res.rates.BYN));
      this.courseList.BGN = JSON.parse(JSON.stringify(res.rates.BGN));
      this.courseList.BRL = JSON.parse(JSON.stringify(res.rates.BRL));
      this.courseList.HUF = JSON.parse(JSON.stringify(res.rates.HUF));
      this.courseList.HKD = JSON.parse(JSON.stringify(res.rates.HKD));
      this.courseList.DKK = JSON.parse(JSON.stringify(res.rates.DKK));
      this.courseList.USD = JSON.parse(JSON.stringify(res.rates.USD));
      this.courseList.EUR = JSON.parse(JSON.stringify(res.rates.EUR));
      this.courseList.INR = JSON.parse(JSON.stringify(res.rates.INR));
      this.courseList.KZT = JSON.parse(JSON.stringify(res.rates.KZT));
      this.courseList.CAD = JSON.parse(JSON.stringify(res.rates.CAD));
      this.courseList.KGS = JSON.parse(JSON.stringify(res.rates.KGS));
      this.courseList.CNY = JSON.parse(JSON.stringify(res.rates.CNY));
      this.courseList.MDL = JSON.parse(JSON.stringify(res.rates.MDL));
      this.courseList.NOK = JSON.parse(JSON.stringify(res.rates.NOK));
      this.courseList.PLN = JSON.parse(JSON.stringify(res.rates.PLN));
      this.courseList.RON = JSON.parse(JSON.stringify(res.rates.RON));
      this.courseList.SGD = JSON.parse(JSON.stringify(res.rates.SGD));
      this.courseList.TJS = JSON.parse(JSON.stringify(res.rates.TJS));
      this.courseList.TRY = JSON.parse(JSON.stringify(res.rates.TRY));
      this.courseList.TMT = JSON.parse(JSON.stringify(res.rates.TMT));
      this.courseList.UZS = JSON.parse(JSON.stringify(res.rates.UZS));
      this.courseList.UAH = JSON.parse(JSON.stringify(res.rates.UAH));
      this.courseList.CZK = JSON.parse(JSON.stringify(res.rates.CZK));
      this.courseList.SEK = JSON.parse(JSON.stringify(res.rates.SEK));
      this.courseList.CHF = JSON.parse(JSON.stringify(res.rates.CHF));
      this.courseList.ZAR = JSON.parse(JSON.stringify(res.rates.ZAR));
      this.courseList.KRW = JSON.parse(JSON.stringify(res.rates.KRW));
      this.courseList.JPY = JSON.parse(JSON.stringify(res.rates.JPY));
      this.courseList.RUB = JSON.parse(JSON.stringify(res.rates.RUB));
    });
  },
};
</script>

<style>
.listPicker {
  height: 350px;
  margin-left: 50px;
}
.labelPicker {
  font-size: 24px;
}
.iconWallet {
  width: 40px;
  height: 40px;
}
</style>
