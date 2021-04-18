<template>
    <form class="sign-up" @submit.prevent="checkForm">
        <modal v-if="isShow"
            v-bind:isShow="isShow"
               @isShow="isShow = false"
        />
        <h2>Атрибут формы адреса</h2>
        <div class="form-group">
            <label for="index">Индекс:</label>
            <div class="input">
                <input
                    id="index"
                    class="form-control"
                    v-model.trim="form.index"
                    autocomplete="off"
                    type="text"
                >
            </div>
        </div>
        <div class="form-group">
            <label for="country">Страна:</label>
            <div class="input">
                <input
                    id="country"
                    class="form-control"
                    v-model.trim="form.country"
                    v-on:keypress="isLetter($event)"
                    autocomplete="off"
                    type="text"
                >
            </div>
        </div>
        <div class="form-group">
            <label for="region">Область:</label>
            <div class="input">
                <input
                    id="region"
                    type="text"
                    class="form-control"
                    v-model.trim="form.region"
                    v-on:keypress="isLetter($event)"
                    autocomplete="off"
                >
            </div>
        </div>
        <div class="form-group">
            <label for="city">Город:</label>
            <p v-if="$v.form.city.$dirty && !$v.form.city.required" class="invalid-feedback">
                *Обязательное поле
            </p>
            <div class="input">
                <input
                    id="city"
                    class="form-control"
                    :class="$v.form.city.$error ? 'is-invalid' : ''"
                    type="text"
                    v-model.trim="form.city"
                    v-on:keypress="isLetter($event)"
                    autocomplete="off"
                >
            </div>
        </div>
        <div class="form-group">
            <label for="street">Улица:</label>
            <div class="input">
                <input
                    id="street"
                    class="form-control"
                    type="text"
                    v-model.trim="form.street"
                    v-on:keypress="isLetter($event)"
                    autocomplete="off"
                >
            </div>
        </div>
        <div class="form-group">
            <label for="home">Дом:</label>
            <div class="input">
                <input
                    id="home"
                    class="form-control"
                    type="text"
                    v-model.trim="form.home"
                    @keypress="isNumber($event)"
                    autocomplete="off"
                >
            </div>
        </div>
        <div class="btn">
            <button type="submit" class="btn btn-primary">Сохранить</button>
        </div>
    </form>
</template>

<script>
    import { validationMixin } from 'vuelidate'
    import { required } from 'vuelidate/lib/validators'
    import modal from './ModalWindows'

    export default {
        mixins: [validationMixin],
        components: {
            modal
        },
        data() {
            return {
                form: {
                    index: '',
                    country: '',
                    region: '',
                    city: '',
                    street: '',
                    home: '',
                },
                isShow: false
            }
        },
        validations: {
            form: {
                city: { required }
            }
        },
        methods: {
            checkForm() {
                this.$v.form.$touch()
                if (!this.$v.form.$error) {
                    this.isShow = true;

                    this.form.index = '';
                    this.form.country = '';
                    this.form.region = '';
                    this.form.city = '';
                    this.form.street = '';
                    this.form.home = '';
                }
            },
            isLetter(e) {
                let char = String.fromCharCode(e.keyCode);
                if(/^[A-Za-z]+$/.test(char)) return true;
                else e.preventDefault();
            },
            isNumber: function(evt) {
                evt = (evt) ? evt : window.event;
                var charCode = (evt.which) ? evt.which : evt.keyCode;
                if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
                    evt.preventDefault();
                } else {
                    return true;
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    form {
        height: calc(100% - 20px);
        padding: 10px 0;
        position: relative;

        h2 {
            font-style: normal;
            font-weight: bold;
            font-size: 16px;
            line-height: 19px;
            text-transform: uppercase;
            color: #B3B3B3;
            text-align: center;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            width: 500px;
            margin-bottom: 10px;
            position: relative;

            label {
                margin-bottom: 5px;
                color: #B3B3B3;
                font-weight: 600;
            }

            .input {
                width: 100%;
                display: flex;
                position: relative;
                align-items: center;
            }

            .invalid-feedback {
                color: rgba(255, 0, 0, .5)!important;
                position: absolute;
                right: 0;
                top: 0;
                margin: 0;
            }

            input[type="text"] {
                display: flex;
                align-items: center;
                border: 2px solid #4d4d4d;
                padding: 0 .5rem;
                height: 32px;
                background-color: #212121;
                color: #ccc;
                width: calc(100% - 18px);
                outline: 0;
            }

            .is-invalid {
                border-color: rgba(255, 0, 0, .5)!important;
            }
        }
    }
    .form-control {
        border: 1px solid transparent;
        width: 100%;
        transition: all ease-in-out 0.5s;
        background: #212121;
        color: #808080!important;
        outline: none;
        height: 34px;
        padding: 0 8px;
    }
    .form-check {
        margin-right: 10px;
    }

    .btn {
        display: flex;
        align-items: center;
        justify-content: flex-end;
        width: 100%;

        button {
            margin-top: 15px;
            background: rgba(0, 102, 51, 0.7);
            color: #E6E6E6;
            border: none !important;
            -moz-user-select: none;
            -ms-user-select: none;
            cursor: pointer;
            outline: 0;
            margin: 0;
            width: 100px;
            line-height: 36px;
            padding: 0 16px;
        }
    }

    .flex {
        display: flex;
        align-items: center;
    }
</style>
