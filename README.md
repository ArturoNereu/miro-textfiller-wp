## Text Filler Web-plugin

A simple web plugin that adds [Lorem Ipsum-like](https://hipsum.co/?paras=1&type=hipster-latin&start-with-lorem=1) text to any selected shape in your Board.

### Try the [Text Filler Web-plugin](https://miro.com/oauth/authorize/?response_type=code&client_id=3458764516005409215&redirect_uri=%2Fconfirm-app-install%2F) in Miro.

The Web-plugin is pretty simple and is meant to help you understand the basics of how to extend Miro's functionality. I encourage you to learn more about [Miro](https://miro.com/), their [Developer Platform](https://developers.miro.com/docs) and the [app-samples repository](https://github.com/miroapp/app-examples) which I used as a base for this plugin.

Once installed, you'll find a new option in the bottomBar. This button was added as a Web-plugin, and once pressed, it will add dummy text to a selected shape.

![Text Filler in action](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/media/textfiller-wp.gif)

### Now, let's talk about how this works:

I will assume that you are not a web developer (such as myself) and will start talking about the two files included in this Web-plugin. Also note that there are other ways to interact with Miro boards.

We only have two files; an [`HTML`](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/index.html) and a [`JavaScript`](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/main.js) file. Both files need to be served via HTTP*s*. I'm using GitHub pages but also found [Tiiny Host](https://tiiny.host/) as an easy way to host and serve the plugin without spending too much time setting up a web server.
