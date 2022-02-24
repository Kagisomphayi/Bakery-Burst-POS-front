<template>
  <section class="contact-background" id="contact">
                <h2 class="text-center display-6 fw-bold mb-3 subtitlee">
            <u>Contact Us</u>
          </h2>
          <div id="emailHelp" class="pb-2 form-text text-center">
            <p>
              Let's get in touch. <br />We will never share your information
              with anyone.
            </p>
          </div>
    <div class="cont container">
      <div class=" justify-content-center formm">
        <form @submit.prevent="handleSubmit" class="contactMe">
          <label class="text-black">Name:</label>
          <input type="text" class="text-white" v-model="name" required />

          <label class="text-black">Email:</label>
          <input type="email" class="text-white" v-model="email" required />

          <label class="text-black">Subject:</label>
          <input type="text" class="text-white" v-model="subject" />

          <label class="text-black">Message:</label>

          <input type="text" class="text-white" v-model="message" />

          <div class="submit mb-3">
            <button class="mb-3 btn button-body">
              <h5 id="sub" class="text-black mb-0">Submit</h5>
            </button>
          </div>
        </form>
      </div>
      <div class="iframe">
        <p>
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d13233.339803357552!2d18.462627286917076!3d-33.98392934734347!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x1dcc42c52081a7cb%3A0x79fbdc90a0e82eac!2sClaremont%2C%20Cape%20Town%2C%207708!5e0!3m2!1sen!2sza!4v1645728763435!5m2!1sen!2sza"
            width="400"
            height="300"
            style="border: 0"
            allowfullscreen=""
            loading="lazy"
          ></iframe>
        </p>
      </div>
    </div>
    <div class="container text-white">
      <div class="row text-center">
        <div class="col col-lg-4 col-sm-4 coL-md-6">
          <i class="bi bi-geo-alt contact-icons"></i>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      subject: "",
      message: "",
    };
  },
  methods: {
    handleSubmit() {
      fetch("https://kagisomphayiportfolio.herokuapp.com/contact", {
        method: "POST",
        body: JSON.stringify({
          name: this.name,
          email: this.email,
          subject: this.subject,
          message: this.message,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => console.log(json));
    },
  },
};
</script>

<style scoped>
form {
  max-width: 100%;
  margin: 30px auto;
  text-align: left;
  border-radius: 10px;
}
label {
  color: rgb(0, 0, 0);
  display: inline-block;
  margin: 25px 0 15px;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
  background-color: rgba(0, 0, 0, 0.25);
}
.button-body {
  background: #fdfdfd;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: rgb(0, 0, 0);
  border-radius: 10px;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
  background: #000000;
}
.submit {
  text-align: center;
}
#sub:hover {
  color: rgb(255, 255, 255) !important;
}
#sub {
  color: white;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
.contactMe {
  width: 100%;
  margin: 0px;
}
.contact-icons {
  font-size: 20px !important;
}
.formm{
    width: 100%;
}
.cont{
    display: flex;
    flex-wrap: wrap;
    justify-content: center !important;
}
/* .iframe{
margin-top: 25px;
} */
@media all and (max-width: 415px) {
.iframe{
width: 80% !important;
}
}
</style>
