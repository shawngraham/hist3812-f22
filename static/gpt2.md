Instructions for loading my pre-trained model.

Make a new code block at the top of the notebook. Enter the following code:

```
!wget http://smg.dhcu.ca/checkpoint_run1.tar
```

This is a zipped folder with the results of my first pass at training a model on Franklin's writing (eg, from here: https://www.gutenberg.org/cache/epub/18985/pg18985.txt). Add another code block beneath, and unzip with this command:

```
!tar -xvf checkpoint_run1.tar
```

The folder will unzip; if you refresh the file tray at left, you'll see a new folder called 'checkpoint' and inside it a subfolder called 'franklinrun1'. All of our model is inside this subfolder.

Run the code block with the `!pip install -q gpt-2-simple` code. This loads up all the lego blocks we need.

To generate new texts based on this model, scroll down to the section, **Load a Trained Model Checkpoint**

Since we're not sideloading the model from Google drive, we will NOT run the line with `gpt2.copy_checkpoint_from_gdrive`. Instead, modify the next code block like so:

```
sess = gpt2.start_tf_sess()
gpt2.load_gpt2(sess, run_name='franklinrun1')
```

Our model is now good to go. In the next section, **Generate Text From The Trained Model** modify the line to specify our Franklin model:

```
gpt2.generate(sess, run_name='franklinrun1')
```

Pick out phrases, and search the original source text to see if the model is just plagiarizing ('overfitting'). If you can't find the source phrases, then we know our model is generating new texts in the style of Franklin.

Now, let's talk with Franklin. Modify the next code block like this:

```
gpt2.generate(sess, run_name='franklinrun1',
              length=50,
              temperature=0.9,
              prefix="Something dreadful happened.",
              nsamples=5,
              batch_size=5,
              top_p=0.9
              )
```

The **prefix** setting is where we steer the model onto the topics we're interested in. Given the nature of the source text, how might you craft prompts to 'get inside' Franklin's mind? Prompt engineering involves a great deal of close reading and an understanding of the source texts... 