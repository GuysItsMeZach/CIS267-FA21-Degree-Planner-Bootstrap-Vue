<template>
  <div id="app" class="d-flex flex-column min-vh-100">
    <!-- Main Content -->
    <main class="flex-fill">
      <div class="container-fluid">
        <div class="navigationbar row mb-5">
          <h1>Degree Planner</h1>
        </div>
        <div class="row main-content">
          <!-- Classes -->
          <div class="col-lg-4 required-classes">
            <h3>Required Classes</h3>

            <b-tabs content-class="mt-3">
              <!-- LAC Requirements -->
              
              <b-tab title="LAC" active>
                <div id="lac">
                  <CourseInfoCard
                    :course="course"
                    v-for="course in lacCourses"
                    :key="course.id"
                    @add-course="add"
                    @remove-course="remove"
                  />
                </div>
              </b-tab>


              
              <b-tab title="CS">
                <div id="cis">
                  <CourseInfoCard
                    :course="course"
                    v-for="course in cisCourses"
                    :key="course.id"
                    @add-course="add"
                  />
                </div>
              </b-tab>
            </b-tabs>
          </div>

          <!-- Semester Schedules -->
          <div class="col-lg-6 semester-schedules">
            <h3>Semester Schedules</h3>

            <SemesterSchedule
              v-for="schedule in schedules"
              :key="schedule.id"
              class="accordion my-4"
              id="schedule.id"
              :schedule="schedule"
              @remove-course="remove"
            />
          </div>

          <!-- Table of Contents Sidebar -->
          <div class="col-lg-2 position-sticky top-0 h-100 ps-5 toc">
            <nav>
              <p class="text-muted">On this page</p>
              <ul>
                <li><a href="#fall2020">Fall 2020</a></li>
                <li><a href="#spring2021">Spring 2021</a></li>
                <li><a href="#fall2021">Fall 2021</a></li>
                <li><a href="#spring2022">Spring 2022</a></li>
                <li><a href="#fall2022">Fall 2022</a></li>
                <li><a href="#spring2023">Spring 2023</a></li>
                <li><a href="#fall2023">Fall 2023</a></li>
                <li><a href="#spring2024">Spring 2024</a></li>
              </ul>
            </nav>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <footer class="bg-dark text-light py-4">
      <div class="container-fluid">
        <div class="row">
          <div class="col">
            <p>Made with ❤️ by FHU students!</p>
          </div>

          <div class="col-md-3">
            <p>&copy; 2021 Freed-Hardeman University</p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import cisCoursesFromFile from "./cis.json";
import lacCoursesFromFile from "./lac.json";
import CourseInfoCard from "./components/CourseInfoCard.vue";
import SemesterSchedule from "./components/SemesterSchedule.vue";


export default {
  name: "App",
  components: {
    //HelloWorld
    CourseInfoCard,
    SemesterSchedule,
  },
  mounted(){

  },
  data() {
    return {
      schedules: [
        {
          name: "Fall 2020",
          id: "fall2020",
          collapseId: "fall2020schedule",
          classes: [],
          total: 0,
        },
        {
          name: "Spring 2021",
          id: "spring2021",
          collapseId: "spring2021schedule",
          classes: [],
          total: 0,
        },
        {
          name: "Fall 2021",
          id: "fall2021",
          collapseId: "fall2021schedule",
          classes: [],
          total: 0,
        },
        {
          name: "Spring 2022",
          id: "spring2022",
          collapseId: "spring2022schedule",
          classes: [],
          total: 0,
        },
        {
          name: "Fall 2022",
          id: "fall2022",
          collapseId: "fall2022schedule",
          classes: [],
          total: 0,
        },
        {
          name: "Spring 2023",
          id: "spring2023",
          collapseId: "spring2023schedule",
          classes: [],
          total: 0,
        },
        {
          name: "Fall 2024",
          id: "fall2024",
          collapseId: "fall2024schedule",
          classes: [],
          total: 0,
        },
        {
          name: "Spring 2024",
          id: "spring2024",
          collapseId: "spring2024schedule",
          classes: [],
          total: 0,
        },
      ],
      lacCourses: lacCoursesFromFile,
      cisCourses: cisCoursesFromFile,
    };
  },
  methods: {
    add(id, selected) {
      //find schedule with matching value
      //push course onto classes array
      this.lacCourses.forEach((course) => {
        if (course.id == id) {
          this.schedules.forEach((s) => {
            if (selected == s.id) {
              if (!s.classes.includes(course)) {
                s.total += Number(course.hours);
                s.classes.push(course);
              }
              return;
            }
          });
        }
      });
      this.cisCourses.forEach((course) => {
        if (course.id == id) {
          this.schedules.forEach((s) => {
            if (selected == s.id) {
              if (!s.classes.includes(course)) {
                s.total += Number(course.hours);
                s.classes.push(course);
              }
              return;
            }
          });
        }
      });
    },
    remove(id, schedule) {
      schedule.classes.forEach((course) => {
        if (course.id == id) {
          schedule.total -= Number(course.hours);
          schedule.classes.pop(course);
        }
      });
    },
  },
};
</script>

<style>
#app {
  font-family: "Nunito Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.toc nav {
  text-align: left;
}
.toc ul {
  padding: 0;
  list-style: none;
}
.toc li {
  margin: 0;
  margin-bottom: 0.5rem;
}
.toc li a {
  text-decoration: none;
}
.toc li a:hover {
  text-decoration: underline;
}
.required-classes .card {
  border-left: 8px solid gold;
}
.navigationbar{
  background: maroon;
  color: white
}
</style>