<template>
  <v-app>
    <v-card class="mx-auto">
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-text-field
          v-model="project"
          label="ชื่อโครงการ"
          required
        ></v-text-field>

        <v-text-field
          v-model="email"
          :rules="emailRules"
          label="E-mail"
          required
        ></v-text-field>

        <v-radio-group v-model="radios" inline label="ลักษณะโครงการ">
          <v-radio label="บริการวิชาการ" value="radio-1"></v-radio>
          <v-radio label="วิจัย" value="radio-2"></v-radio>
          <v-radio label="วิเคราะห์ทดสอบ" value="radio-3"></v-radio>
          <v-radio label="อบรมระยะสั้น" value="radio-4"></v-radio>
          <v-radio label="อบรมใบอนุญาติขับขี่รถ" value="radio-5"></v-radio>
          <v-radio
            label="จำหน่ายผลงานวิจัย นวัตกรรม และทรัพย์สินทางปัญญา"
            value="radio-6"
          ></v-radio>
        </v-radio-group>

        <v-text-field
          v-model="autor"
          label="ผู้รับผิดชอบโครงการ"
          required
        ></v-text-field>

        <v-textarea
          clearable
          clear-icon="mdi-close-circle"
          label="สังกัดคณะ/สำนัก/สถาบัน "
          model-value=""
        ></v-textarea>

        <v-text-field
          v-model="TimeLine"
          label="ระยะเวลาดำเนินการ"
          required
        ></v-text-field>

        <v-textarea
          clearable
          label="หลักการและเหตุผล"
          model-value=""
        ></v-textarea>
        <v-btn @click="add" class="mr-4">เพิ่มขั้นตอนการดำเนินงาน</v-btn>
        <div
          v-for="(textField, i) in textFields"
          :key="i"
          class="text-fields-row"
        >
          <v-text-field
            :label="textField.label1"
            v-model="textField.value1"
          ></v-text-field>

          <v-text-field
            :label="textField.label2"
            v-model="textField.value2"
          ></v-text-field>
          <v-text-field
            :label="textField.label3"
            v-model="textField.value3"
          ></v-text-field>

          <v-btn @click="remove(i)" color="error">ลบขั้นตอน</v-btn>
        </div>

        <v-btn color="success" class="mr-4" @click="validate"> summit </v-btn>
        <v-btn color="warning" class="mr-4" @click="reset"> Reset Form </v-btn>
      </v-form>
    </v-card>
  </v-app>
</template>
<script>
export default {
  data: () => ({
    textFields: [],
    radios: null,
    valid: true,
    project: "",
    autor: "",
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => (v && v.length <= 10) || "Name must be less than 10 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
  }),

  methods: {
    async validate() {
      const { valid } = await this.$refs.form.validate();

      if (valid) alert("Form is valid");
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
    add() {
      this.textFields.push({
        label1: "กิจกรรม/ขั้นตอน",
        value1: "",
        label2: "ระยะเวลา",
        value2: "",
        label3: "ผู้รับผิดชอบ",
        value3: "",
      });
    },

    remove(index) {
      this.textFields.splice(index, 1);
    },
  },
};
</script>
