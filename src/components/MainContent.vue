<template>
  <div class="main-content" id="main-content">
    <form class="form" @submit.prevent="submitHandler">
      <h1 class="form__title">Для регистрации укажите необходимые данные</h1>
      <p class="form__description">Обязательные поля помечены *</p>
      <div class="input-field">
        <label class="form__label">Фамилия*</label>
        <input
          type="text"
          placeholder="Фамилия"
          class="form__input"
          v-model.trim="surname"
          :class="{
            invalid:
              ($v.surname.$dirty && !$v.surname.required) ||
              ($v.surname.$dirty && !$v.surname.minLength),
            error_input:
              ($v.surname.$dirty && !$v.surname.required) ||
              ($v.surname.$dirty && !$v.surname.minLength),
          }"
        />
        <p class="error-text" v-if="$v.surname.$dirty && !$v.surname.required">
          Поле не должно быть пустым
        </p>
        <p class="error-text" v-if="$v.surname.$dirty && !$v.surname.minLength">
          Слишком короткая фамилия
        </p>
      </div>

      <div class="input-field">
        <label class="form__label">Имя*</label>
        <input
          type="text"
          placeholder="Имя"
          class="form__input"
          v-model.trim="name"
          :class="{
            invalid:
              ($v.name.$dirty && !$v.name.required) ||
              ($v.name.$dirty && !$v.name.minLength),
            error_input:
              ($v.name.$dirty && !$v.name.required) ||
              ($v.name.$dirty && !$v.name.minLength),
          }"
        />
        <p class="error-text" v-if="$v.name.$dirty && !$v.name.required">
          Поле не должно быть пустым
        </p>
        <p class="error-text" v-if="$v.name.$dirty && !$v.name.minLength">
          Слишком короткое имя
        </p>
      </div>

      <div class="input-field">
        <label class="form__label">Отчество</label>
        <input
          type="text"
          placeholder="Отчество"
          class="form__input"
          v-model.trim="patronymic"
          :class="{
            invalid: $v.patronymic.$dirty && !$v.patronymic.minLength,
            error_input: $v.patronymic.$dirty && !$v.patronymic.minLength,
          }"
        />
        <p
          class="error-text"
          v-if="$v.patronymic.$dirty && !$v.patronymic.minLength"
        >
          Слишком короткое отчество
        </p>
      </div>

      <div class="input-field">
        <label class="form__label">Дата рождения*</label>
        <input
          type="date"
          placeholder="Дата рождения"
          class="form__input"
          v-model.trim="date"
          :class="{
            invalid: $v.date.$dirty && !$v.date.required,
            error_input: $v.date.$dirty && !$v.date.required,
          }"
        />
        <p class="error-text" v-if="$v.date.$dirty && !$v.date.required">
          Поле не должно быть пустым
        </p>
      </div>

      <div class="input-field">
        <label class="form__label">Ваш номер телефона</label>
        <input
          type="number"
          class="form__input"
          v-model.trim="number"
          :class="{
            invalid:
              ($v.number.$dirty && !$v.number.minLength) ||
              ($v.number.$dirty && !$v.number.maxLength),
            error_input:
              ($v.number.$dirty && !$v.number.minLength) ||
              ($v.number.$dirty && !$v.number.maxLength),
          }"
        />
        <p
          class="error-text"
          v-if="
            ($v.number.$dirty && !$v.number.minLength) ||
            ($v.number.$dirty && !$v.number.maxLength)
          "
        >
          Номер телефона должен содержать 11 цифр
        </p>
      </div>

      <div class="input-field">
        <label class="form__label">Пол:</label>
        <br />
        <input name="sex" type="radio" id="sex-1" class="form__radio" />
        <label name="sex" class="form__label" for="sex-1">Мужской</label>
        <input name="sex" type="radio" id="sex-2" class="form__radio" />
        <label name="sex" class="form__label" for="sex-2">Женский</label>
      </div>

      <div class="input-field">
        <label class="form__label">Выберите группу*:</label>
        <select
          class="form__input form__select"
          multiple="multiple"
          size="3"
          v-model="group"
          :class="{
            invalid: $v.group.$dirty && !$v.group.required,
            error_input: $v.group.$dirty && !$v.group.required,
          }"
        >
          <option value="VIP">VIP</option>
          <option value="Проблемные">Проблемные</option>
          <option value="ОМС">ОМС</option>
        </select>
        <p class="error-text" v-if="$v.group.$dirty && !$v.group.required">
          Выберите группу
        </p>
      </div>

      <div class="input-field">
        <label class="form__label">Выберите врача:</label>
        <select class="form__input">
          <option value="Иванов">Иванов</option>
          <option value="Захаров">Захаров</option>
          <option value="Чернышева">Чернышева</option>
        </select>
      </div>

      <div class="input-field">
        <input id="sms" type="checkbox" class="form__checkbox" />
        <label name="sex" class="form__label" for="sms"
          >Не отправлять СМС</label
        >
      </div>

      <p class="form__description">Укажите адрес:</p>

      <div class="input-field">
        <label class="form__label">Индекс</label>
        <input type="text" class="form__input" placeholder="Индекс" />
      </div>

      <div class="input-field">
        <label class="form__label">Страна</label>
        <input type="text" class="form__input" placeholder="Страна" />
      </div>

      <div class="input-field">
        <label class="form__label">Область</label>
        <input type="text" class="form__input" placeholder="Область" />
      </div>

      <div class="input-field">
        <label class="form__label">Город*</label>
        <input
          type="text"
          class="form__input"
          placeholder="Город"
          v-model="sity"
          :class="{
            invalid: $v.sity.$dirty && !$v.sity.required,
            error_input: $v.sity.$dirty && !$v.sity.required,
          }"
        />
        <p class="error-text" v-if="$v.sity.$dirty && !$v.sity.required">
          Укажите город
        </p>
      </div>

      <div class="input-field">
        <label class="form__label">Улица</label>
        <input type="text" class="form__input" placeholder="Улица" />
      </div>

      <div class="input-field">
        <label class="form__label">Дом</label>
        <input type="text" class="form__input" placeholder="Дом" />
      </div>

      <div class="input-field">
        <label class="form__label">Выберите документ*:</label>
        <select
          class="form__input"
          v-model="document"
          :class="{
            invalid: $v.document.$dirty && !$v.document.required,
            error_input: $v.document.$dirty && !$v.document.required,
          }"
        >
          <option value="Паспорт">Паспорт</option>
          <option value="Свидетельство о рождении">
            Свидетельство о рождении
          </option>
          <option value="Водительское удостоверение">
            Водительское удостоверение
          </option>
        </select>
        <p
          class="error-text"
          v-if="$v.document.$dirty && !$v.document.required"
        >
          Документ не выбран
        </p>
      </div>

      <div class="input-field">
        <label class="form__label">Cерия</label>
        <input type="text" class="form__input" placeholder="Серия" />
      </div>

      <div class="input-field">
        <label class="form__label">Номер</label>
        <input type="text" class="form__input" placeholder="Номер" />
      </div>

      <div class="input-field">
        <label class="form__label">Кем выдан</label>
        <input type="text" class="form__input" placeholder="Кем выдан" />
      </div>

      <div class="input-field">
        <label class="form__label">Дата выдачи*</label>
        <input
          type="text"
          class="form__input"
          placeholder="Дата выдачи"
          v-model="dateOfIssue"
          :class="{
            invalid: $v.dateOfIssue.$dirty && !$v.dateOfIssue.required,
            error_input: $v.dateOfIssue.$dirty && !$v.dateOfIssue.required,
          }"
        />
        <p
          class="error-text"
          v-if="$v.dateOfIssue.$dirty && !$v.dateOfIssue.required"
        >
          Укажите дату выдачи
        </p>
      </div>

      <button type="submit" class="form__button" value="Отправить">
        Отправить
      </button>
      <div class="successfully" v-bind:class="{ active: isActive }">
        <p class="successfull__message">Новый клиент успешно создан</p>
      </div>
    </form>
  </div>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";

export default {
  name: "main-content",
  data() {
    return {
      isActive: false,
      surname: "",
      name: "",
      patronymic: "",
      date: "",
      number: "7",
      group: [],
      sity: "",
      document: [],
      dateOfIssue: "",
    };
  },
  validations: {
    surname: { required, minLength: minLength(2) },
    name: { required, minLength: minLength(2) },
    patronymic: { minLength: minLength(2) },
    date: { required },
    number: { minLength: minLength(11), maxLength: maxLength(11) },
    group: { required },
    sity: { required },
    document: { required },
    dateOfIssue: { required },
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      this.isActive = true;
      setTimeout(() => (this.isActive = false), 1000);
    },
  },
};
</script>

<style>
.main-content {
  width: 600px;
  margin: 60px auto;
  border-radius: 30px;
  background: white;
}

.form {
  width: 100%;
  padding: 80px;
  box-sizing: border-box;
}

.form__title {
  font-size: 28px;
  margin: 0 0 20px 0;
}

.form__description {
  font-size: 24px;
  margin: 0 0 30px 0;
}

.form__input {
  width: 100%;
  height: 38px;
  font-size: 16px;
  font-weight: normal;
  color: #555555;
  background: #e9eff6;
  border-width: 0;
  border-radius: 15px;
  padding: 5px 10px;
  box-sizing: border-box;
  margin: 20px 0 0 0;
}

.form__input:focus {
  outline: none;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

input[type="number"],
input[type="number"]:hover,
input[type="number"]:focus {
  appearance: none;
  -moz-appearance: textfield;
}

.form__label {
  font-size: 20px;
  color: #707981;
  margin: 0 0 20px 0;
  text-align: center;
}

#sex-2 {
  margin: 0 5px 0 15px;
}

.form__radio {
  margin: 20px 5px 20px 0;
}

.form__checkbox {
  margin: 0 5px 20px 0;
}

.form__select {
  height: unset;
}

.form__button {
  background: #f69a73;
  border-bottom: 4px solid #d87d56;
  color: white;
  font-size: 14px;
  border-width: 0;
  border-radius: 20px;
  height: 38px;
  width: 100%;
  margin-top: 30px;
}

.form__button:hover {
  cursor: pointer;
  outline: none;
}

.successfully {
  position: fixed;
  left: 39%;
  top: 50%;
  background-color: yellowgreen;
  border-radius: 20px;
  opacity: 0;
  visibility: hidden;
  transition: 0.55s opacity, 0.55s visibility;
}

.active {
  opacity: 1;
  visibility: visible;
}

.successfull__message {
  margin: 0;
  padding: 20px;
  font-size: 20px;
}

.input-field {
  margin-bottom: 20px;
}

.error-text {
  color: red;
  font-size: 16px;
  margin: 10px 0 0 0;
}

.error_input {
  border: 2px solid red;
}

@media screen and (max-width: 768px) {
  .main-content {
    width: 425px;
    margin: 20px auto;
    border-radius: 30px;
  }

  .form {
    padding: 40px;
  }

  .form__title {
    font-size: 24px;
  }

  .form__description {
    font-size: 20px;
  }

  .form__input {
    font-size: 14px;
  }

  .form__label {
    font-size: 18px;
  }

  .error-text {
    font-size: 14px;
  }
}

@media screen and (max-width: 426px) {
  .main-content {
    width: 100%;
    margin: 0;
    border-radius: 0;
  }

  .form {
    padding: 15px;
  }

  .form__title {
    font-size: 20px;
  }

  .form__description {
    font-size: 18px;
  }

  .form__label {
    font-size: 16px;
  }

  .error-text {
    font-size: 12px;
  }
}
</style>
