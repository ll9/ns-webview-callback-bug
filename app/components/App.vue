<template>
    <Page @loaded="pageLoaded">
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <StackLayout >
            <Label class="message" :text="msg" />
            <WebView id="webView" />
            <Button text="callJS" @tap="callJs"></Button>
            <Button text="nav" @tap="nav"></Button>
        </StackLayout>
    </Page>
</template>

<script>
import Vue from "vue";

var webViewInterfaceModule = require("nativescript-webview-interface");
var oWebViewInterface;
import SecondPage from "../components/SecondPage";

const WWW_ROOT = "~/wwwroot/index.html";

export default Vue.extend({
  data() {
    return {
      msg: "Hello World!",
      /** @type webViewInterfaceModule.WebViewInterface */
      oWebViewInterface: null
    };
  },
  computed: {
    any: () => {}
  },
  methods: {
    pageLoaded(args) {
      let page = args.object;
      let webView = page.getViewById("webView");
      this.oWebViewInterface = new webViewInterfaceModule.WebViewInterface(
        webView,
        WWW_ROOT
      );
    },
    callJs() {
      this.oWebViewInterface.callJSFunction(
        "jsFun",
        null,
        resp => {
          console.log(resp);
        },
        err => console.log(err)
      );
    },
    nav() {
      this.$navigateTo(SecondPage);
    }
  }
});
</script>

<style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
</style>
