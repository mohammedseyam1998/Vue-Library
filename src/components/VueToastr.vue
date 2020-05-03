<template>
  <div id="app">
    <div class="c">
      <p>
        <button
          style="background: lightblue;
"
          type="button"
          name="button"
          @click="add"
        >
          SHOW TOSTER
        </button>
        <button v-if="showRemoveButton" type="button" @click="removeSticky">
          Remove Sticky Toast By Name
        </button>
      </p>
    </div>
    <vue-toastr ref="toastr"></vue-toastr>
  </div>
</template>

<script>
import VueToastr from "vue-toastr";

export default {
  data() {
    return {
      showRemoveButton: false
    };
  },
  // mounted() {
  //   this.$toastr.defaultTimeout = 10000; // default timeout : 5000
  //   this.$toastr.defaultClassNames = ["animated", "zoomInUp"];
  //   this.$toastr.s(
  //     "This Message From Toastr Plugin\n You can access this plugin : <font color='yellow'>this.$toastr</font>"
  //   );
  //   this.$toastr.defaultClassNames = ["animated", "bounceInRight"];
  //   this.$toastr.defaultPosition = "toast-top-left";
  //   this.$toastr.s(
  //     "This Message From Toastr Plugin\n You can access this plugin : <font color='yellow'>this.$toastr</font>"
  //   );
  // },
  components: {
    VueToastr
  },
  methods: {
    removeSticky() {
      this.$refs.toastr.removeByName("stickyToast");
    },
    add() {
      this.$refs.toastr.Add({
        name: "stickyToast",
        title: "Sticky",
        msg: "You can't close and my name is 'stickyToast'",
        clickClose: false, // Click Close Disable
        timeout: 0, // Remember defaultTimeout is 5 sec..
        position: "toast-bottom-center",
        type: "error",
        classNames: ["animated", "flipInX"],
        onCreated: () => {
          this.showRemoveButton = true;
        },
        onClosed: () => {
          this.showRemoveButton = false;
        }
      });
      this.$refs.toastr.Add({
        msg: "You cant click close, auto closed 8 sec.. with timeout options",
        title: "Sticky2",
        clickClose: false,
        timeout: 8000,
        position: "toast-top-center",
        type: "error"
      });
      // setTimeout(() => {
      //   //alert("onClosed by type warning");
      //   this.$refs.toastr.removeByType("warning");
      // }, 5000);
      // this.$refs.toastr.close(VooAaa);
      // You Can Change Default Toast Type
      this.$refs.toastr.defaultTimeout = 3000; // default timeout : 5000
      // You Can Change Default Toast Type
      this.$refs.toastr.defaultType = "error"; // default type : success
      // change global progress bar
      this.$refs.toastr.defaultProgressBar = false;
      // You Can Change Default Position
      this.$refs.toastr.defaultPosition = "toast-bottom-left"; // default position: toast-top-right
      // this.$refs.toastr.Add(
      //   "Default Type Position and timeout is Changed, closed 3 sec."
      // );
    }
  }
};
</script>

<style>
.c {
  margin-top: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.c p {
  margin: 0;
}
</style>
