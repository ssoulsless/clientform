<template>
	<form @submit.prevent="handleSubmit">
		<p class="form-header">Форма клиента:</p>
		<div>
			<label>Поля с * обязательны для заполнения</label>
		</div>
		<label for="secondName">Фамилия* :</label>
		<input
			:class="$v.form.secondName.$error ? 'is-invalid' : ''"
			type="text"
			id="secondName"
			v-model.trim.trim="form.secondName"
		/>
		<p
			v-if="$v.form.secondName.$dirty && !$v.form.secondName.required"
			class="invalid-feedback"
		>
			Это обязательное поле!
		</p>

		<label for="name">Имя* :</label>
		<input
			:class="$v.form.secondName.$error ? 'is-invalid' : ''"
			type="text"
			id="name"
			v-model.trim="form.name"
		/>
		<p
			v-if="$v.form.name.$dirty && !$v.form.name.required"
			class="invalid-feedback"
		>
			Это обязательное поле!
		</p>

		<label for="patronymic">Отчество :</label>
		<input type="text" id="patronymic" v-model.trim="form.patronymic" />

		<label for="dateOfBirth">Дата рождения* :</label>
		<input
			:class="$v.form.dateOfBirth.$error ? 'is-invalid' : ''"
			type="date"
			id="dateOfBirth"
			v-model.trim="form.dateOfBirth"
		/>
		<p
			v-if="$v.form.dateOfBirth.$dirty && !$v.form.dateOfBirth.required"
			class="invalid-feedback"
		>
			Это обязательное поле!
		</p>

		<label for="phoneNumber">Номер телефона* :</label>
		<input
			placeholder="7 xxx xxx xx xx"
			:class="$v.form.phoneNumber.$error ? 'is-invalid' : ''"
			type="tel"
			id="phoneNumber"
			v-model.trim="form.phoneNumber"
		/>
		<p
			v-if="$v.form.phoneNumber.$dirty && !$v.form.phoneNumber.required"
			class="invalid-feedback"
		>
			Это обязательное поле!
		</p>
		<p
			v-if="
				($v.form.phoneNumber.$dirty &&
					!$v.form.phoneNumber.mustBeWithLengthOfEleven) ||
					($v.form.phoneNumber.$dirty &&
						!$v.form.phoneNumber.mustStartsWithSeven)
			"
			class="invalid-feedback"
		>
			Введите номер формата: 7хххххххххх
		</p>

		<label>Пол :</label>
		<div class="gender-options">
			<div class="gender-options--item">
				<input
					type="radio"
					name="genderRadio"
					id="male"
					value="male"
					v-model="form.gender"
				/>
				<label for="male">Мужской</label>
			</div>

			<div class="gender-options--item">
				<input
					type="radio"
					name="genderRadio"
					id="female"
					value="female"
					v-model="form.gender"
				/>
				<label for="female">Женский</label>
			</div>
		</div>

		<label>Группа клиентов* : </label>
		<select
			class="clients-groups"
			v-model="form.selectedClientsGroups"
			multiple
			:class="$v.form.selectedClientsGroups.$error ? 'is-invalid' : ''"
		>
			<option
				v-for="(clientsGroup, index) in clientsGroups"
				:key="index"
				:value="clientsGroup.value"
				>{{ clientsGroup.label }}</option
			>
		</select>
		<p
			v-if="
				$v.form.selectedClientsGroups.$dirty &&
					!$v.form.selectedClientsGroups.required
			"
			class="invalid-feedback"
		>
			Это обязательное поле!
		</p>

		<label>Лечащий врач :</label>
		<select v-model="form.doctor">
			<option
				v-for="(doctor, index) in doctors"
				:key="index"
				:value="doctor.value"
				>{{ doctor.label }}</option
			>
		</select>

		<div class="sms-acception">
			<input
				id="smsAcception"
				type="checkbox"
				v-model.trim="form.smsAcception"
			/>
			<label for="smsAcception">Не отправлять смс</label>
		</div>

		<label for="zipCode">Индекс :</label>
		<input
			type="text"
			id="zipCode"
			name="zipCode"
			v-model.trim="form.zipCode"
		/>

		<label for="country">Страна :</label>
		<input
			type="text"
			id="country"
			name="country"
			v-model.trim="form.country"
		/>

		<label for="region">Область :</label>
		<input type="text" id="region" name="region" v-model.trim="form.region" />

		<label for="city">Город* :</label>
		<input
			:class="$v.form.city.$error ? 'is-invalid' : ''"
			type="text"
			id="city"
			name="city"
			v-model.trim="form.city"
		/>
		<p
			v-if="$v.form.city.$dirty && !$v.form.city.required"
			city
			class="invalid-feedback"
		>
			Это обязательное поле!
		</p>

		<label for="street">Улица :</label>
		<input type="text" id="street" name="street" v-model.trim="form.street" />

		<label for="house">Дом :</label>
		<input type="text" id="house" name="house" v-model.trim="form.house" />

		<label>Тип документа* :</label>
		<select
			:class="$v.form.documentType.$error ? 'is-invalid' : ''"
			v-model.trim="form.documentType"
		>
			<option value="passport">Паспорт</option>
			<option value="birthCertificate">Свидетельство о рождении</option>
			<option value="driversLicense">Водительское удостоверение</option>
		</select>
		<p
			v-if="$v.form.documentType.$dirty && !$v.form.documentType.required"
			city
			class="invalid-feedback"
		>
			Это обязательное поле!
		</p>

		<label for="series">Серия документа :</label>
		<input type="number" id="series" name="series" v-model.trim="form.series" />

		<label for="numberofDocument">Номер документа :</label>
		<input
			type="number"
			id="numberofDocument"
			name="numberofDocument"
			v-model.trim="form.numberofDocument"
		/>

		<label for="issuedByWhom">Кем выдан :</label>
		<input
			type="text"
			id="issuedByWhom"
			name="issuedByWhom"
			v-model.trim="form.issuedByWhom"
		/>

		<label for="dateOfIssue">Дата выдачи* :</label>
		<input
			:class="$v.form.dateOfIssue.$error ? 'is-invalid' : ''"
			type="date"
			id="dateOfIssue"
			name="dateOfIssue"
			v-model.trim="form.dateOfIssue"
		/>
		<p
			v-if="$v.form.dateOfIssue.$dirty && !$v.form.dateOfIssue.required"
			city
			class="invalid-feedback"
		>
			Это обязательное поле!
		</p>

		<button type="submit">Создать клиента</button>
		<p v-if="$v.form.$dirty && $v.form.$error" city class="invalid-feedback">
			Пожалуйста, введите корректные данные
		</p>
	</form>
</template>
<script>
import { required } from 'vuelidate/lib/validators';

const mustStartsWithSeven = (value) => value[0] == 7;
const mustBeWithLengthOfEleven = (value) => value.length === 11;

export default {
	name: 'Form',
	validations() {
		return {
			form: {
				secondName: { required },
				name: { required },
				patronymic: {},
				dateOfBirth: { required },
				phoneNumber: {
					required,
					mustBeWithLengthOfEleven,
					mustStartsWithSeven,
				},
				gender: {},
				selectedClientsGroups: { required },
				doctor: {},
				smsAcception: {},
				zipCode: {},
				country: {},
				region: {},
				city: { required },
				street: {},
				house: {},
				documentType: { required },
				series: {},
				numberofDocument: {},
				issuedByWhom: {},
				dateOfIssue: { required },
			},
		};
	},
	data() {
		return {
			form: {
				secondName: '',
				name: '',
				patronymic: '',
				dateOfBirth: '',
				phoneNumber: '',
				gender: '',
				selectedClientsGroups: [],
				doctor: '',
				smsAcception: '',
				zipCode: '',
				country: '',
				region: '',
				city: '',
				street: '',
				house: '',
				documentType: '',
				series: '',
				numberofDocument: '',
				issuedByWhom: '',
				dateOfIssue: '',
			},
			clientsGroups: [
				{ label: 'VIP', value: 'vip' },
				{ label: 'Проблемные', value: 'problematic' },
				{ label: 'ОМС', value: 'oms' },
			],
			doctors: [
				{ label: 'Захаров', value: 'zaharov' },
				{ label: 'Иванов', value: 'ivanov' },
				{ label: 'Чернышева', value: 'chernisheva' },
			],
		};
	},
	methods: {
		handleSubmit() {
			this.$v.form.$touch();
			if (!this.$v.form.$error) {
				alert('Новый клиент успешно создан!');
			}
		},
	},
};
</script>
<style scoped>
form {
	max-width: 420px;
	margin: 30px auto;
	background: #fff;
	text-align: left;
	padding: 40px;
	border-radius: 10px;
}
label {
	color: #aaa;
	display: inline-block;
	margin: 25px 0 15px;
	font-size: 0.6em;
	text-transform: uppercase;
	letter-spacing: 1px;
	font-weight: bold;
}
input,
select {
	display: block;
	padding: 10px 6px;
	width: 100%;
	box-sizing: border-box;
	border: none;
	border-bottom: 1px solid #ddd;
	color: #555;
}
input[type='checkbox'] {
	display: inline-block;
	width: 16px;
	margin: 0 10px 0 0;
	position: relative;
	top: 2px;
}
input[type='radio'] {
	display: inline-block;
}
button {
	display: block;
	padding: 10px 30px;
	width: 50%;
	box-sizing: border-box;
	border-radius: 10px;
	border: 1px solid #ddd;
	margin: 25px auto;
}
.gender-options {
	display: flex;
	justify-content: space-between;
	padding-bottom: 25px;
	border-bottom: 1px solid #ddd;
}
.gender-options--item {
	display: flex;
	width: 100%;
}
.gender-options--item label,
.gender-options--item input {
	margin: 0;
	flex-grow: 1;
	width: auto;
}
.clients-groups {
	padding: 0;
	overflow: hidden;
	outline: none;
}
.sms-acception {
	text-align: center;
	border-bottom: 1px solid #ddd;
	padding-bottom: 10px;
}
.invalid-feedback {
	color: red;
	font-size: 0.9rem;
	text-align: center;
}
.is-invalid {
	border: 1px solid red;
	border-radius: 5px;
}
.form-header {
	text-align: center;
	color: #aaa;
	margin: 25px 0 15px;
	text-transform: uppercase;
	letter-spacing: 1px;
	font-weight: bold;
}
</style>
