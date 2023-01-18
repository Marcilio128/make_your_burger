<template>
        <div class="message-container">
            <p>{{msg}}</p>
        </div>
    
</template>

<script>
import MessageCSS from "../css/Message.css"
    export default {
        name: "Message",
        data() {
            return {

            }
        },
        props: {
            msg: String
        },
        components: {
            MessageCSS
        } 
    }

</script>