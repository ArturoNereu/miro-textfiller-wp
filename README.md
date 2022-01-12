## Text Filler Web-plugin

A simple web plugin that adds [Lorem Ipsum-like](https://hipsum.co/?paras=1&type=hipster-latin&start-with-lorem=1) text to any shape in your Board.

### Try the [Text Filler Web-plugin](https://miro.com/oauth/authorize/?response_type=code&client_id=3458764516005409215&redirect_uri=%2Fconfirm-app-install%2F) in Miro.

The Web-plugin is pretty simple and is meant to help you understand the basics of how to extend Miro's functionality. I encourage you to learn more about [Miro](https://miro.com/), their [Developer Platform](https://developers.miro.com/docs) and the [app-samples repository](https://github.com/miroapp/app-examples) which I used as a base for this plugin.

Once installed, you'll find a new option in the bottomBar. This button was added as a Web-plugin, and once pressed, it will add dummy text to a selected shape.

![Text Filler in action](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/media/textfiller-wp.gif)

### Now, let's talk about how this works:

I will assume that you are not a web developer (such as myself) and will start talking about the two files included in this Web-plugin. Also note that there are other ways to interact with Miro boards.

We only have two files; an [`HTML`](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/index.html) and a [`JavaScript`](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/main.js) file. Both files need to be served via HTTP*s*. I'm using GitHub pages but also found [Tiiny Host](https://tiiny.host/) as an easy way to host and serve the plugin without spending too much time setting up a web server.

Without going into too much details on how Miro fetches your Web-plugin (which I don't know), it basically requests your HTML and JS and "injects" it into a Miro board that has been previously authorized to install the Web-plugin.

![](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/media/diagram-wp.png)

The [`index.html`](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/index.html) file is pretty short, think of it as a web page that doesn't render anything directly but loads Miro's SDK and our `JavaScript` file.

```
...
    <script src="https://miro.com/app/static/sdk.1.1.js"></script>
    <script src="main.js"></script>
...
```

The [`main.js`](https://github.com/ArturoNereu/miro-textfiller-wp/blob/main/main.js) has more code, but in reality is pretty straighforward.

Let's split it in three main parts:

#### Part 1
```
const icon = '<path ... />'
const dummyText = "..."
```
We define two constants, `icon` which contains the SVG code for our custom icon to render and `dummyText`, a simple string generated using [Hipster Ipsum](https://hipsum.co/?paras=1&type=hipster-latin&start-with-lorem=1)

#### Part 2
```
miro.onReady(() => {
  miro.initialize({
    extensionPoints: {
      bottomBar: {
        title: 'Text Filler',
        svgIcon: icon,
        positionPriority: 1,
        
        ...
        
      },
    },
  })
})
```
This code, configures our extension after the board is ready and initialized. See that our tool is added to the bottomBar and the icon will be the icon we defined avobe.

#### Part 3
```
onClick: async () => {

          let shape = (await miro.board.widgets.get({type:'shape'}))[0]
          await miro.board.viewport.zoomToObject(shape)
          miro.board.widgets.update({id: shape.id, text: dummyText, style:{shapeBackgroundColor:'#7ac673'}})
          miro.showNotification('Dummy Text Added to your Shape!')
},
```
This last piece is actually the piece that gives our plugin its functionality. I feel that the Miro reference is self explanatory but in a nutshell we are:

- getting the reference to the shapes in our board. For our example, we simply select the first registered one `[0]```
- for a better UX, we zoom into the shape we selected
- we update the text in the shape with our dummyText
- we show a notification telling the user the function was executed

### Why?
Miro has a [Marketplace](https://miro.com/marketplace/)(I recently learned about it!) and you can publish your apps there. But also, if your company needs more functionality than the one built into Miro, you can add it.

### Known issues and features to add
* if no shape is found, an exception will be thrown
* we could allow the user to select all the shapes she wanted to add text to in batch
* we could allow the user to configure the length of the text
