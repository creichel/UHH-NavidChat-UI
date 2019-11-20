<template>
  <q-page ref="page" class="q-pa-md full-width column wrap justify-end" >
    <div style="width: 100%; max-width: 900px; margin: 0 auto">
      <template v-for="message in messages">
        <template v-if="message.user == 'me'">
          <q-chat-message
            v-bind:key="message"
            :text="[message.text]"
            sent
            text-color="white"
            bg-color="blue"
          ></q-chat-message>
        </template>
        <template v-else>
          <q-chat-message
            v-bind:key="message"
            :name="message.user"
            :text="[message.text]"
            text-color="black"
            avatar="statics/avatar.jpg"
            bg-color="grey-3"
          ></q-chat-message>
        </template>
      </template>
    </div>
    <q-footer elevated class="bg-white text-black q-pa-md">
      <q-toolbar>
          <q-form @submit="sendMessage" class="full-width">
            <q-input
              rounded
              outlined
              v-model="messageToSend"
              ref="messageInput"
              autofocus
            >
              <template v-slot:append>
                <q-btn
                  type="submit"
                  round
                  dense
                  flat
                  icon="arrow_upward"
                  class="bg-blue text-white"
                  :loading="sending"
                  @click="sendMessage"
                >
                  <template v-slot:loading>
                    <q-spinner-ios />
                  </template>
                </q-btn>
              </template>
            </q-input>
          </q-form>
      </q-toolbar>
    </q-footer>
  </q-page>
</template>

<style lang="scss">
.q-message-text {
  border-radius: 18px !important;
  padding: 8px 17px 6px 13px !important;
  &:after {
    position: absolute;
    content: "";
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    z-index: -1;
  }

  &::before {
    border: none !important
  }
}

.text-blue {
  &:after {
    background: url("data:image/svg+xml;charset=utf-8,<svg xmlns='http://www.w3.org/2000/svg' x='0px' y='0px' width='15.515px' height='17.5px' viewBox='32.485 17.5 15.515 17.5' enable-background='new 32.485 17.5 15.515 17.5'><path fill='#1084FF' d='M48,35c-7-4-6-8.75-6-17.5C28,17.5,29,35,48,35z'/></svg>") right bottom no-repeat;
    right: -6px;
  }
}

.text-grey-3:after {
  background: url("data:image/svg+xml;charset=utf-8,<svg xmlns='http://www.w3.org/2000/svg' x='0px' y='0px' width='15.515px' height='17.5px' viewBox='32.484 17.5 15.515 17.5' enable-background='new 32.484 17.5 15.515 17.5'><path fill='#E5E5EA' d='M38.484,17.5c0,8.75,1,13.5-6,17.5C51.484,35,52.484,17.5,38.484,17.5z'/></svg>") left bottom no-repeat;
  left: -6px;
}

.q-message-text-content {
  font-size: 16px;
  line-height: 1.4;
}

.q-field--with-bottom {
  padding-bottom: 0
}

</style>

<script>
export default {
  name: 'Chat',
  data () {
    return {
      messageToSend: '',
      sending: false,
      messages: [
        {
          id: 0,
          user: `NavidChat`,
          text: `Hi! Danke, dass du beim Interview teilnimmst 😃`
        },
        {
          id: 1,
          user: `me`,
          text: `Kein Problem ☺️ ich helfe immer gerne`
        },
        {
          id: 2,
          user: `NavidChat`,
          text: `lalalalala ich kann ziemlich ziemlich viel schreiben. : Auch gibt es niemanden, der den Schmerz an sich liebt, sucht oder wünscht, nur, weil er Schmerz ist, es sei denn, es kommt zu zufälligen Umständen, in denen Mühen und Schmerz ihm große Freude bereiten können. Um ein triviales Beispiel zu nehmen, wer von uns unterzieht sich je anstrengender körperlicher Betätigung, außer um Vorteile daraus zu ziehen? Aber wer hat irgend ein Recht, einen Menschen zu tadeln, der die Entscheidung trifft, eine Freude zu genießen, die keine unangenehmen Folgen hat, oder einen, der Schmerz vermeidet, welcher keine daraus resultierende Freude nach sich zieht? Auch gibt es niemanden, der den Schmerz an sich liebt, sucht oder wünscht, nur, weil er Schmerz ist, es sei denn, es kommt zu zufälligen Umständen, in denen Mühen und Schmerz ihm große Freude bereiten können. Um ein triviales Beispiel zu nehmen, wer von uns unterzieht sich je anstrengender körperlicher Betätigung, außer um Vorteile daraus zu ziehen? Aber wer hat irgend ein Recht, einen Menschen zu tadeln, der die Entscheidung trifft, eine Freude zu genießen, die keine unangenehmen Folgen hat, oder einen, der Schmerz vermeidet, welcher keine daraus resultierende Freude nach sich zieht?`
        },
        {
          id: 3,
          user: `me`,
          text: `Wenn ich doch nur wirklich Nachrichten schreiben könnte...`
        }
      ]
    }
  },
  methods: {
    sendMessage () {
      console.log('Send called')
      this.sending = true

      this.messages = this.messages.concat({
        id: this.messages.length,
        user: `me`,
        text: this.messageToSend
      })
      this.messageToSend = ''
      this.sending = false
      window.scrollTo(0, document.body.scrollHeight)
      this.$refs.messageInput.$el.focus()
    }
  }
}
</script>
