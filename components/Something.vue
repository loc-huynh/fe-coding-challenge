<!-- Please remove this file from your project -->
<template>
  <div
    class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0"
  >
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
        <b-col cols="3" class="bg-success">
          <div
            :style="{
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'flex-direction': 'column',
            }"
          >
            <img
              src="https://via.placeholder.com/100"
              alt="paragraph"
              :draggable="true"
              @dragstart="drag"
            />
            <p>paragraph</p>
          </div>
          <div
            :style="{
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'flex-direction': 'column',
            }"
          >
            <img
              src="https://via.placeholder.com/100"
              alt="button"
              :draggable="true"
              @dragstart="drag"
            />
            <p>button</p>
          </div>
          <div
            :style="{
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'flex-direction': 'column',
            }"
          >
            <img
              src="https://via.placeholder.com/100"
              alt="imageUpload"
              :draggable="true"
              @dragstart="drag"
            />
            <p>imageUpload</p>
          </div>
          <div
            :style="{
              display: 'flex',
              'justify-content': 'center',
              'align-items': 'center',
              'flex-direction': 'column',
            }"
          >
            <img
              src="https://via.placeholder.com/100"
              alt="textEditor"
              :draggable="true"
              @dragstart="drag"
            />
            <p>textEditor</p>
          </div>
        </b-col>
        <b-col cols="9" class="bg-info" @drop="drop" @dragover="allowDrop" :style="{'position': 'relative'}">
          {{ JSON.stringify(info) }}
          <ul>
            <li v-for="({ type }, index) in info" :key="index">
              <button
                v-if="type === 'button'"
                :style="{
                  border: '1px solid black',
                  'background-color': 'gray',
                  padding: '10px',
                }"
              >
                button
              </button>
              <p
                v-if="type === 'paragraph'"
                :style="{ 'font-size': '20px', 'font-weight': 'bold' }"
              >
                paragraph
              </p>
              <p
                v-if="type === 'imageUpload'"
                :style="{
                  'font-size': '20px',
                  'font-style': 'italic',
                  color: 'darkred',
                }"
              >
                imageUpload
              </p>
              <p
                v-if="type === 'textEditor'"
                :style="{
                  'font-size': '20px',
                  'font-style': 'italic',
                  color: 'blue',
                }"
              >
                textEditor
              </p>
            </li>
          </ul>
          <div :style="{'position': 'absolute', 'bottom': 0, 'display': 'block' ,'min-height': '100px', 'width': '97%','border-top': '1px solid black'}">
            detail
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'SomethingComponent',
  data() {
    return {
      info: [],
    }
  },
  methods: {
    drag(event) {
      console.log('DRAG', event)
      const controlType = event.srcElement.alt
      event.dataTransfer.setData('type', controlType)
    },
    drop(event) {
      const type = event.dataTransfer.getData('type')
      console.log('DROP', type)
      event.preventDefault()
      /* const textnode = document.createTextNode('Water') */
      /* event.target.appendChild(textnode) */
      this.info.push({ type })
    },
    allowDrop(event) {
      /* console.log('DROP', event) */
      event.preventDefault()
    },
  },
}
</script>
