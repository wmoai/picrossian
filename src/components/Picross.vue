<template>
  <div>
    <table id="picross-body">
      <thead>
        <tr>
          <th></th>
          <th v-for="(column, k) in columns" :key="k" class="column">
            <div v-for="(num, l) in column" :key="l">
              {{ num }}
            </div>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, y) in rows" :key="y">
          <th class="row">
            <span v-for="(num, n) in row" :key="n">
              {{ num }}
            </span>
          </th>
          <td
            :class="{dotted: inputs[x][y], crossed: inputs[x][y] === false}"
            v-for="(_, x) in columns"
            :key="x"
            @click="hitDot(x, y)"
          ></td>
        </tr>
      </tbody>
    </table>
    <div id="controller">
      <input id="input-dot" type="radio" v-model="inputType" value="dot" />
      <label for="input-dot">■</label>
      <input id="input-cross" type="radio" v-model="inputType" vlaue="closs" />
      <label for="input-cross">x</label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  props: {
    columns: Array,
    rows: Array,
  },
  data: function() {
    const columnSize = this.columns.length;
    const rowSize = this.rows.length;
    return {
      columnSize,
      rowSize,
      inputType: 'dot',
      inputs: new Array(columnSize).fill(new Array(rowSize).fill(null)),
    };
  },
  methods: {
    hitDot: function(x, y) {
      const currentInput = this.inputType === 'dot' ? true : false;
      const newValue = this.inputs[x][y] === null ? currentInput : null;
      const newColumn = Array.from(this.inputs[x]);
      newColumn[y] = newValue;
      this.inputs.splice(x, 1, newColumn);
    },
  },
  watch: {
    inputs: function() {
      console.log(123);
    },
  },
};
</script>

<style lang="scss">
#picross-body {
  border-collapse: collapse;
  border: 2px solid black;
  user-select: none;
  th {
    border: 1px solid black;
    line-height: 1em;
    background-color: #fcfcfc;
    &:nth-child(5n + 2) {
      border-left-width: 2px;
    }

    &.column {
      vertical-align: bottom;
      padding: 5px 0;
    }
    &.row {
      text-align: right;
      padding: 0 7px;
    }
  }
  tr {
    border-top: 1px solid black;
    &:nth-child(5n + 1) {
      border-top-width: 2px;
    }
  }
  $cellSize: 25px;
  td {
    position: relative;
    border: 1px solid black;
    box-sizing: border-box;
    width: $cellSize;
    height: $cellSize;
    cursor: pointer;
    &:nth-child(5n + 2) {
      border-left-width: 2px;
    }

    &.dotted {
      background-color: #555;
    }

    &.crossed {
      &:before,
      &:after {
        position: absolute;
        left: 0;
        content: '';
        display: block;
        width: 100%;
        border-top: 1px solid #555;
      }
      &:before {
        transform: skewY(-45deg);
      }
      &:after {
        transform: skewY(45deg);
      }
    }
  }
}
#controller {
  margin-top: 20px;
  input[type='radio'] {
    display: none;

    &:checked + label {
      background-color: palegreen;
    }
  }

  label {
    display: table-cell;
    width: 40px;
    height: 40px;
    text-align: center;
    font-size: 40px;
    line-height: 1em;
    vertical-align: middle;
    border: 1px solid gray;
    user-select: none;
  }
}
</style>
