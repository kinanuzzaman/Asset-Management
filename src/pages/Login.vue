<template>
  <q-layout class="flex flex-center">
    <q-card>
      <q-card-section>
        <div class="flex flex-center">
          <img
            alt="Quasar logo"
            src="~assets/laptop.png"
            style="width: 80px; height: 80px"
          />
        </div>

        <q-form>
          <q-input
            clearable
            v-model="email"
            label="EMAIL"
            placeholder="email@example.com"
          />
          <q-input
            v-model="password"
            :type="isPwd ? 'password' : 'text'"
            label="PASSWORD"
            ><template v-slot:append>
              <q-icon
                :name="isPwd ? 'visibility_off' : 'visibility'"
                class="cursor-pointer"
                @click="isPwd = !isPwd"
              />
            </template>
          </q-input>
          <q-btn
            id="btn"
            class="q-mt-md"
            to="/main/users"
            color="black"
            text-color="white"
            label="Login"
          ></q-btn>
        </q-form>
        <q-list>
          <q-item>
            <q-item-section> Don't have account with us ? </q-item-section>
            <q-btn id="btn" to="/register" flat label="REGISTER"></q-btn>
          </q-item>
          <q-item>
            <q-item-section> Don't remember password ? </q-item-section>
            <q-btn id="btn" to="/reqpass" flat label="REQUEST PASSWORD"></q-btn>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
  </q-layout>
</template>
<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      isPwd: true,
      admin: null,
    };
  },
  created() {},
  methods: {
    login() {
      let fd = new FormData();
      fd.append("email", this.email);
      fd.append("password", this.password);

      const options = {
        method: "POST",
        url: "http://127.0.0.1:8000/api/login",
        data: fd,
        headers: {
          Authorization: "8|JdXmwaAd4Ff3V2srhBX8cBvVGNetHXfkcajvopzA",
        },
      };

      axios
        .request(options)
        .then((response) => {
          console.log(response.data);
          this.admin = response.data;
        })
        .catch(function (error) {
          console.error(error);
        });
    },
  },
};
</script>
<style></style>
