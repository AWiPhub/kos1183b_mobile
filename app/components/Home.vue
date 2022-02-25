<template>
  <Page class="page">
    <ActionBar title="kos1183b" class="action-bar" />
    <ScrollView>
      <FlexboxLayout flexDirection="column" justifyContent="center">
        <Image
          src="~/assets/myPhoto.png"
          stretch="myPhoto"
          alignSelf="center"
        />

        <Label
          alignSelf="center"
          text="Студент 4 курса"
          style="margin-top: 40px"
        />
        <Label alignSelf="center" text="Группа 1183б" />
        <Label alignSelf="center" text="Карбышев Олег Сергеевич" />
        <Label alignSelf="center" text="АО «ГСК «Югория»" />
        <Label alignSelf="center" text="Младший разработчик" />
        <Label alignSelf="center" text="Управление фронт-офисных систем" />
        <Label
          alignSelf="center"
          text="Отдел разработки WEB и мобильных приложений"
        />

        <ScrollView orientation="horizontal" style="margin-top: 40px">
          <FlexboxLayout>
            <Button
              class="kp"
              text="Калькулятор"
              @tap="goToDetailPage('calc')"
            />
            <Button class="kp" text="Погода" @tap="goToDetailPage('weather')" />
          </FlexboxLayout>
        </ScrollView>
      </FlexboxLayout>
    </ScrollView>
  </Page>
</template>

<script>
import Calc from "./Calc.vue";
import Weather from "./Weather.vue";

export default {
  data() {
    return {};
  },
  methods: {
    goToDetailPage(page) {
      switch (page) {
        case "calc":
          this.$navigateTo(Calc);
          break;
        case "weather":
          this.$navigateTo(Weather);
          break;
      }
    },
  },
};
</script>

<style scoped>
.kp {
  width: 400px;
  height: 300px;
}
</style>
