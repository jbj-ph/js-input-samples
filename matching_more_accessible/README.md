### Matching, More Accessible ###

#### Notes ####
This was originally built at the Open edX Technical Conference Hackathon, November 2014. It's almost ready for deployment, but I would wait a month or two first.

The main difference between this one and the one marked "accessible" is that this has a single interface for mouse and keyboard/screen reader access, rather than two different interfaces.


#### Overview ####
This implements a standard matching exercise of the "draw the lines to match things on the left with things on the right" sort (though without actually drawing lines). It handles both text and images, and does one-to-one and many-to-many matching. The correct answer is hidden from students via python in the problem XML.

In addition, this problem is well-accessible via screen reader. A button on each of the right-hand objects will open a contextual menu with checkboxes that perform the matching functions.

Student state is recorded via Logger.log() when a grade is calculated, but not at other times.

#### Creating Your Own Matching Problems ####

Here's how to adapt this example to create your own matching problems.

1. Come up with the items. 
2. Find images or write text (full HTML ok) for the matching items. Consider front-loading the text of your items so that students hear the most important or identifiable parts of them first when using a screen reader.
3. Download the files used in this problem.
4. Update the MatchingA\_Elements.js file. Fill in the 'type' property with either 'text' or 'image', and fill in the according property with the image's filename or with your text. The text field is used as alt text for images.
5. Upload all your images and files to the "Files and Uploads" section of Studio, or just dump them in the proper directory if you're using the XML approach.
6. Create a new Custom Javascript Display and Input problem (under the "Advanced" problem tab). Copy and paste the contents of MatchingA.xml into that problem, fix up the `right\_answer` variable so that it contains the answer you want, and add your own instructions for the students.
7. Use your browser's javascript console for debugging - for instance, if your items' text or images aren't showing up, it may point you to the line in your MatchingMA\_Elements.js file that is causing the problem.

##### Using Multiple Matching Problems #####

If you have multiple matching problems in your course, you need to have different MatchingA_Element files for each one. You will need to number or name them differently, and update the link in the HTML page.

Never put two matching problems on the same page. The universe will explode. Or maybe they just won't work. Probably the second one. No guarantees.

#### Files: ####

Inside you will find many pieces used to create this problem:

- `jschannel.js`: the javascript file that allows javascript-type problems to work at all. You should not need to change this. I didn't make this one.
- `underscore.js`: This does some nice array equality checking for us, and some minor other stuff. You should not need to change this. I didn't make this one.
- `jquery.ui.touch-punch.min.js`: [Touch Punch](https://github.com/furf/jquery-ui-touch-punch), an awesome JQuery extension that maps touch events into mouse events. Used for mobile compatibility. Should not need to alter.
- `MatchingMA.js`: the javascript file that does the majority of the work and allows you to drag items around and stuff. You should not need to change this.
- `MatchingMA.css`: the css file that makes things look pretty (or as close as I could get them). You should not need to change this.
- `MatchingMA.html`: the HTML file that will be iframed into the page. You should not need to change this unless you have more than one matching problem in your course.
- `MatchingMA.xml`: the XML used to create the problem within Studio. You will need to make changes to this: updating `right\_answer` to be the actual right answer you want, and filling it with your own instruction text.
- `MatchingMA\_Elements.js`: holds the pregenerated group names. You will need to update this to have the items you want.
- And several image files that you will need to replace with your own. 

When creating your own matching problem, you will upload almost every file in this directory to the Files and Uploads section. There are two exceptions: the XML file (which you cut-and-paste into Studio) and the image files (which you replace with your own).
