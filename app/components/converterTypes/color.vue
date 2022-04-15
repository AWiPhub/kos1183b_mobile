<template>
  <Page class="page">
    <ActionBar title="HEX в RGB" class="action-bar">
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
          justifyContent="center"
          alignItems="center"
          style="margin-top: 200px; font-size: 22px; text-align: center"
        >
          <Label :text="total" textWrap />
        </FlexboxLayout>

        <FlexboxLayout
          flexDirection="row"
          justifyContent="center"
          style="margin-top: 200px"
        >
          <GridLayout
            columns="70, 70, 70, 70, 70"
            rows="65, 65, 65, 65, 65, 65"
          >
            <label
              :text="displayField"
              row="0"
              col="0"
              colSpan="5"
              class="display"
            />

            <button
              class="kp"
              text="C"
              row="1"
              col="0"
              colSpan="4"
              @tap="clear"
            />
            <button class="kp" text="⌫" row="1" col="4" @tap="backspace" />

            <button class="kp" text="7" row="2" col="0" @tap="input('7')" />
            <button class="kp" text="8" row="2" col="1" @tap="input('8')" />
            <button class="kp" text="9" row="2" col="2" @tap="input('9')" />
            <button class="kp" text="A" row="2" col="3" @tap="input('A')" />
            <button class="kp" text="B" row="2" col="4" @tap="input('B')" />

            <button class="kp" text="4" row="3" col="0" @tap="input('4')" />
            <button class="kp" text="5" row="3" col="1" @tap="input('5')" />
            <button class="kp" text="6" row="3" col="2" @tap="input('6')" />
            <button class="kp" text="C" row="3" col="3" @tap="input('C')" />
            <button class="kp" text="D" row="3" col="4" @tap="input('D')" />

            <button class="kp" text="1" row="4" col="0" @tap="input('1')" />
            <button class="kp" text="2" row="4" col="1" @tap="input('2')" />
            <button class="kp" text="3" row="4" col="2" @tap="input('3')" />
            <button class="kp" text="E" row="4" col="3" @tap="input('E')" />
            <button class="kp" text="F" row="4" col="4" @tap="input('F')" />

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
              style="font-size: 12px"
              text="Конвертировать"
              row="5"
              col="3"
              colSpan="2"
              @tap="doConvertig"
            />
          </GridLayout>
        </FlexboxLayout>
      </FlexboxLayout>
    </ScrollView>
  </Page>
</template>

<script>
import Converter from "../Converter.vue";

export default {
  name: "Calc",
  data() {
    return {
      displayField: "#",
      selectedOut: 0,
      selectedTo: 0,
      total: "",
    };
  },
  methods: {
    input(key) {
      if (this.displayField.length < 7) {
        this.displayField += key;
      }
    },
    backspace() {
      if (this.displayField.length > 1) {
        this.displayField = this.displayField.substr(
          0,
          this.displayField.length - 1
        );
      }
    },
    clear() {
      this.displayField = "#";
    },
    goBack() {
      this.$navigateTo(Converter);
    },
    doConvertig() {
      const result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(
        this.displayField
      );
      // this.total = result ? {
      //   r: parseInt(result[1], 16),
      //   g: parseInt(result[2], 16),
      //   b: parseInt(result[3], 16)
      // } : null;
      this.total = result
        ? `${parseInt(result[1], 16)}, ${parseInt(result[2], 16)}, ${parseInt(
            result[3],
            16
          )}`
        : "Неправильно введено\nHEX значение";
    },
  },
  computed: {
    viewSelectedOut: function () {
      return this.listOfItems[this.selectedOut];
    },
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
</style>
