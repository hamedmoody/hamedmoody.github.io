<template>
  <div class="container" id="latest-courses">
    <h2>آخرین دوره های من</h2>
    <div v-if=" ! fetching" class="courses">
      <CourseCard v-for="(course, course_index) in courses" :key="course_index" :course="course"/>
    </div>
    <div v-else>
      در حال بارگذاری دوره ها...
    </div>
  </div>
</template>

<script>
import CourseCard from "@/views/components/CourseCard.vue";
export default {
  name: "HomeCourses",
  components: {CourseCard},
  data(){
    return{
      courses   : [],
      fetching  : true,
    }
  },
  mounted() {
    this.get_courses();
  },
  methods: {
    get_courses(){
      let _this = this;
      let url = 'https://daneshjooyar.com/wp-json/api/v2/courses/?include=3374703,3361086,3357000,3350404,3365320,3365313,3339339,458810';
      fetch(url)
          .then(response => response.json())
          .then( (data) => {
            //console.log(data);
            _this.courses = data;
            _this.fetching = false;
          })
          .catch( (error) => {
            console.error('Error:', error)
          } );
    }
  }
}
</script>

<style scoped lang="scss">

  #latest-courses {
    margin-top: 50px;
    margin-bottom: 50px;
    h2 {
      font-size: 32px;
      font-weight: bold;
      text-align: center;
    }
  }

  .courses{
    display: grid;
    gap: 20px;
  }

  @media screen and ( min-width: 768px ){
    .courses{
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media screen and ( min-width: 992px ){
    .courses{
      grid-template-columns: repeat(3, 1fr);
    }
  }

  @media screen and ( min-width: 1366px ){
    .courses{
      grid-template-columns: repeat(4, 1fr);
    }
  }

</style>