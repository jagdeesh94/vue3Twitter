<template>
  <div class="twoot-item">
    <div class="twoot-item__user">
      {{ twoot.content }}
    </div>
  </div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style>
.twoot-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #Dfe3eb;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s case;
}

.twoot-item:hover {
  transform: scale(1.1, 1.1);
}

.twoot-item__user {
  font-weight: bold;
}
</style>