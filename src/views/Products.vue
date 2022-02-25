<template>
  <!-- projects section -->
  <section id="projects" class="products">
    <div class="container hr">
      <hr class="bg-white" />
    </div>
    <div class="container">
      <div class="pb-5 justify-content-center">
        <h1 class="text-center display-6 fw-bold subtitlee"><u>Projects</u></h1>
        <p class="text-center text-muted mb-5">
          Below are some of the projects I've done
        </p>
        <div class="row col-lg-12 proji" style="row-gap: 30px">
          <div
            v-for="project of projects"
            :key="project.title"
            class="col-lg-3 col-md-6"
            style="display: flex; justify-content: center"
          >
            <div class="card shadow ani-card" style="width: 18rem">
              <img :src="project.img" class="card-img-top" alt="..." />
              <div class="card-body">
                <h4 class="card-title text-white">{{ project.title }}</h4>
                <p class="card-text text-white">{{ project.description }}</p>

                <!-- <ul class="list-group px-0 list-group-flush">
                <li class="list-group-item">{{project.html}}</li>
                <li class="list-group-item">{{project.css}}</li>
                <li class="list-group-item">{{project.js}}</li>
              </ul> -->
              </div>

              <div class="card-body">
                <a target="_blank" :href="project.netlify" class="card-link"
                  ><button class="btn mt-0 rounded-pill">
                    Netlify
                  </button></a
                >
                <a target="_blank" :href="project.github" class="card-link"
                  ><button class="btn mt-0 rounded-pill">
                    Github
                  </button></a
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="container hr">
      <hr class="bg-white" />
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      projects: null,
    };
  },
  mounted() {
    fetch()
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        this.projects = data;
      });
  },
};
</script>

<style scoped>
.products{
  padding-top: 50px;
}
</style>