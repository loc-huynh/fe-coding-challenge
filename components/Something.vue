<!-- Please remove this file from your project -->
<template>
  <div class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0">
    <link
      href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css"
      rel="stylesheet"
    />
    <b-container
      class="bv-example-row bg-primary fluid"
      :style="{ 'min-height': '100vh' }"
    >
      <b-row :style="{'display': 'flex', 'justify-content': 'center', 'padding': '10px'}">
        <button :style="{'padding': '10px', 'color': 'white', 'background-color': 'darkred', 'margin-right': '10px'}">Save</button>
        <button :style="{'padding': '10px', 'color': 'white', 'background-color': 'darkred', 'margin-right': '10px'}">Undo</button>
        <button :style="{'padding': '10px', 'color': 'white', 'background-color': 'darkred', 'margin-right': '10px'}">Redo</button>
        <button :style="{'padding': '10px', 'color': 'white', 'background-color': 'darkred', 'margin-right': '10px'}">Import</button>
        <button :style="{'padding': '10px', 'color': 'white', 'background-color': 'darkred', 'margin-right': '10px'}">Export</button>
        <button :style="{'padding': '10px', 'color': 'white', 'background-color': 'darkred', 'margin-right': '10px'}">View</button>

      </b-row>
      <b-row>
        <b-col
          cols="3"
          class="bg-success"
        >
          <div :style="{
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'flex-direction': 'column',
            }">
            <img
              src="https://via.placeholder.com/100"
              alt="paragraph"
              :draggable="true"
              @dragstart="drag"
            />
            <p>paragraph</p>
          </div>
          <div :style="{
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'flex-direction': 'column',
            }">
            <img
              src="https://via.placeholder.com/100"
              alt="button"
              :draggable="true"
              @dragstart="drag"
            />
            <p>button</p>
          </div>
          <div :style="{
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'flex-direction': 'column',
            }">
            <img
              src="https://via.placeholder.com/100"
              alt="imageUpload"
              :draggable="true"
              @dragstart="drag"
            />
            <p>imageUpload</p>
          </div>
          <div :style="{
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'flex-direction': 'column',
            }">
            <img
              src="https://via.placeholder.com/100"
              alt="textEditor"
              :draggable="true"
              @dragstart="drag"
            />
            <p>textEditor</p>
          </div>
        </b-col>
        <b-col
          cols="9"
          class="bg-info"
          @drop="drop"
          @dragover="allowDrop"
          :style="{'position': 'relative'}"
        >
          {{ JSON.stringify(info) }}
          <ul>
            <li
              v-for="(item, index) in info"
              :key="index"
            >
              <button
                v-if="item.type === 'button'"
                :style="{
                  border: '1px solid black',
                  'background-color': 'gray',
                  padding: '10px',
                }"
                @click="changeText(item)"
              >
                {{item.text}}
              </button>
              <p
                v-if="item.type === 'paragraph'"
                :style="{ 'font-size': '20px', 'font-weight': 'bold' }"
                @click="changeText(item)"
              >
                {{item.text}}
              </p>
              <p
                v-if="item.type === 'imageUpload'"
                :style="{
                  'font-size': '20px',
                  'font-style': 'italic',
                  color: 'darkred',
                }"
                @click="changeText(item)"
              >
                imageUpload
              </p>
              <p
                v-if="item.type === 'textEditor'"
                :style="{
                  'font-size': '20px',
                  'font-style': 'italic',
                  color: 'blue',
                }"
                @click="changeText(item)"
              >
                textEditor
              </p>
            </li>
          </ul>
          <div :style="{'position': 'absolute', 'bottom': 0, 'display': 'block' ,'min-height': '100px', 'width': '97%','border-top': '1px solid black'}">
            detail
            <form v-if="selectedItem">
              <div v-if="selectedItem.type === 'paragraph'">
                <label for="text">paragraph text</label>
                <input
                  type="text"
                  :value="selectedItem.text"
                  @keyup="updateContent"
                />
              </div>
              <div v-if="selectedItem.type === 'button'">
                <label for="text">button text</label>
                <input
                  type="text"
                  :value="selectedItem.text"
                  @keyup="updateContent"
                >
                <label for="text">alert message</label>
                <input
                  type="text"
                  :value="selectedItem.alertMessage"
                  @keyup="updateAlertMessage"
                >
              </div>
            </form>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'SomethingComponent',
  data () {
    return {
      info: [],
      id: 0,
      selectedItem: null
    }
  },
  methods: {
    drag (event) {
      console.log('DRAG', event)
      const controlType = event.srcElement.alt
      event.dataTransfer.setData('type', controlType)
    },
    drop (event) {
      const type = event.dataTransfer.getData('type')
      console.log('DROP', type)
      event.preventDefault()
      /* const textnode = document.createTextNode('Water') */
      /* event.target.appendChild(textnode) */
      const item = { type, id: ++this.id, text: type };
      this.info.push(item)
    },
    allowDrop (event) {
      /* console.log('DROP', event) */
      event.preventDefault()
    },
    changeText (item) {
      console.log('change text')
      this.selectedItem = item
    },
    updateContent (event) {
      this.selectedItem.text = event.target.value;
      this.info[this.info.findIndex(item => item.id === this.selectedItem.id)].text = event.target.value;
    },
    updateAlertMessage(event) {
      this.selectedItem.alertMessage = event.target.value;
      this.info[this.info.findIndex(item => item.id === this.selectedItem.id)].alertMessage = event.target.value;
    },
  },
}
</script>
