<template>
  <modal name="single-modal" :width="700" :height="`auto`" :minHeight="600" :adaptive="true" :scrollable="true" @before-open="beforeOpen">
      <div class="single-modal">
          <div class="modal-close" @click="$modal.hide('single-modal')">X</div>
          <h3 class="single-modal--title">{{title}}</h3>
          <p class="single-modal--description">{{description}}</p>
          <p class="single-modal--category"><strong>Task category :</strong> {{category}}</p>
          <div class="row">
              <div class="col-md-6 single-modal--start"><strong>Task start:</strong> {{start}}</div>
              <div class="col-md-6 single-modal--stop"><strong>Task end:</strong> {{stop}}</div>
          </div>
          <div class="row">
              <div class="col-md-6 col-12"><a href="#" class="delete-task-btn" @click.prevent="sendIdTask">Delete task</a></div>
          </div>
      </div>
  </modal>
</template>

<script>
import {EventBus} from "../../helpers/event-bus.js"
export default {
    data(){
        return {
            id : null,
            title : null,
            description : null,
            category : null,
            start : null,
            stop : null,
            status : null
        }
    },
    methods: {
        beforeOpen (event) {
            if(event.params.id)  this.id = event.params.id;
            if(event.params.title)  this.title = event.params.title;
            if(event.params.description)  this.description = event.params.description;
            if(event.params.category)  this.category = event.params.category;
            if(event.params.start)  this.start = event.params.start;
            if(event.params.stop)  this.stop = event.params.stop;
        },
        sendIdTask(){
            EventBus.$emit('get-del-id-task', this.id);
            this.$modal.hide('single-modal');
        }
    }
}
</script>
