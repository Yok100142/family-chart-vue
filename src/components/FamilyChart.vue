<template>
  <div
    id="chart"
    style="
      height: 700px;
      max-height: calc(100vh - 80px);
      width: 900px;
      max-width: 100%;
      margin: auto;
      position: relative;
    "
  ></div>
</template>

<script>
import f3 from "family-chart";
import data from "../assets/data.json";

console.log(data);

export default {
  name: "FamilyChart",
  mounted() {
    const store = f3.createStore({
        data: data,
        cont: document.querySelector("#chart"),
        card_display: [(d) => d.data.label || "", (d) => d.data.desc || ""],
        mini_tree: true,
        hide_rels: true,
        edit: true,
        node_separation: 250,
        level_separation: 150,
        card_dim: {
          w: 220,
          h: 70,
          text_x: 75,
          text_y: 15,
          img_w: 60,
          img_h: 60,
          img_x: 5,
          img_y: 5,
        },
      }),
      view = f3.d3AnimationView(store);

    store.setOnUpdate((props) =>
      view.update({ tree: store.state.tree, ...(props || {}) })
    );
    store.update.tree();
  },
};
</script>

<style>
.cursor-pointer {
  cursor: pointer;
}

svg.main_svg {
  width: 100%;
  height: 100%;
  background-color: rgb(59, 85, 96);
  color: rgb(59, 85, 96);
}

svg.main_svg text {
  fill: currentColor;
}

.input-field input {
  height: 2.5rem !important;
}
.input-field > label:not(.label-icon).active {
  -webkit-transform: translateY(-8px) scale(0.8);
  transform: translateY(-8px) scale(0.8);
}

.card-female {
  fill: lightpink;
}

.card-male {
  fill: lightblue;
}

.card-genderless {
  fill: #fff;
}

.card-main {
  stroke: #000;
}

.card_family_tree {
  cursor: pointer;
}

.card_family_tree rect {
  transition: 0.3s;
}

.card_family_tree:hover rect {
  transform: scale(1.15);
}

.card_add_relative {
  cursor: pointer;
  color: lightgray;
  transition: 0.3s;
}

.card_add_relative circle {
  fill: #fff;
}

.card_add_relative:hover {
  color: black;
}

.card_edit.pencil_icon {
  transition: 0.3s;
}

.card_edit.pencil_icon:hover {
  color: white;
}

.card_break_link,
.link_upper,
.link_lower,
.link_particles {
  transform-origin: 50% 50%;
  transition: 1s;
}
.card_break_link {
  color: #fff;
}
.card_break_link.closed .link_upper {
  transform: translate(-140.5px, 655.6px);
}
.card_break_link.closed .link_upper g {
  transform: rotate(-58deg);
}
.card_break_link.closed .link_lower {
}
.card_break_link.closed .link_particles {
  transform: scale(0);
}
</style>