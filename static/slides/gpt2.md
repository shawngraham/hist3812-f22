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

Here's the output, by the way, from the prompt above.

```
Something dreadful happened. As the
whole party was loaded with hunger, much wind, and a keen
arth
rush, the morning of the 31st was very cold. The following
chronological record is sufficient to give the course of events
around the point
====================
Something dreadful happened. We were all frozen
in-place for the greater part of a winter in which the gale
has subsided, and snow was falling more brightly than before. Yet
each of us was reduced to much colder prevails in the day,
====================
Something dreadful happened. I
saw Mr. Back and his party being pushed about with a
strong pull of the wind from the tents, being covered with snow.
Accurate charts and drawings, were absolutely
not possible, and we were in some degree in error
====================
Something dreadful happened. I felt a kind of swell around my knee, and was
in a state of shock throughout the whole enterprise. The Doctor having
ain't leisure to drop by our quarters during the night,
asked if I was still lame. I told
====================
Something dreadful happened. The dogs became very ill, and one of them was
affected with an ulcer, which was now our palliation
evasion. I was now so much exhausted, that my legs were raw, and
some other articles too, raw,
====================
```