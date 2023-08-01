---
title: "Chat AI Prompt Engineering - Part 1 (Intro and Spark Example)"
date: 2023-07-25T05:40:49-07:00
draft: false
Author: "Guy Cutting"
tags: ["ChatGPT", "Google Bard", "Chat bots", "AI", "GPT models", "Prompt Engineering", "OpenAI"]
---

![Apache Spark logo](/apache_spark.webp)

This post is hopefully the first in a series on the topic of prompt engineering, which has become of topic of heavy discussion with the explosion of [ChatGPT](https://chat.openai.com), [Bard](https://bard.google.com), and other (generally GPT-based) chat bots onto the AI scene. 

## GPT Models Available

ChatGPT has received most of the attention in the GPT space, but it's certainly not the only competitor.

I'd like to take a moment to discuss [Google Bard](https://bard.google.com), which has not received nearly the kind of press attention that ChatGPT has, but which should certainly be considered a worthy competitor. Bard is a great LLM, but my (mostly subjective) experience is that it's just not quite as quite as advanced as ChatGPT in almost any area. ChatGPT gives better code, more interesting poetry/rhymes, more varied language, and in general responses that seem to have been written at a higher level (by someone with a graduate degree as opposed to an undergraduate). As we go through some example prompts, I'll provide some side-by-side examples to back up my assertion about this generalized comparison.

One key difference, as of the writing of this article (July 25, 2023) is that ChatGPT has commercial availability (you can sign up for a paid version of the service with extra features, and ChatGPT is being integrated into commercial products like Bing search), whereas [Bard](https://bard.google.com) is still only available via pre-release waitlist signup. So for business purposes that's a pretty important consideration and probably a dealbreaker for Bard for most folks.

So for now, Bard is still an experiment (although a very exciting one) rather than a commercially available product. But it's definitely something to keep an eye on. Google is still perhaps *the* AI leader, having created and developed much of the current AI/ML infrastucture currently in use, and it would be foolish to count them out of the game in any sense.

There's a [great GPT model comparison available from bito.ai](https://bito.ai/epic-battle-of-ai-models-google-bard-chatgpt-3-5-gpt-4-bison-palm-2-and-anthropic-claude-unveiling-the-best/). I don't want to spend too much time comparing models generally, and I don't have access to Claude, so I'll let them take this one.

## My Personal Excitement about Prompt Engineering

GPT models obviously have a lot of people excited about their capabilities and I'm no exception.

As a writer of fiction and poetry, I'm also interested in prompt engineering as a communication exercise. A story from my childhood might help illustrate this interest. My father had a PhD in statistics and his dissertation, published in the early 1970s (in the era of mainframes programmed on punch cards) was a piece of software that managed information for a large urban school district. Later in life, he disavowed a lot of technology (for reasons that I only began to understand as I became an adult), but when I was young he understood the value of digital technology and was eager that I should have access to computers and know how to use them. 

When I was 6 or 7 (~1989) he bought a used Commodore-64 for me from a friend. I'm not sure if it didn't include the original manuals or if I just didn't bother with them. But I sat down to use the machine without much in the way of references, so I interacted with it in the way that made the most intuitive sense to my young brain. I understood that the computer could hold information, and the first thing that I did when I looked at the blinking prompt on the screen was to type, 'What is geography?' to see what answer I would get. When I (of course) got some sort of error, I thought about it for a minute and realized that maybe the computer had not yet been told what geography was, so I typed in, 'Geography is the study of the world,' thinking that if I explicitly told it that fact then the machine would be able to answer my original question. The Commodore still didn't understand this, because it was obviously looking for much more structured commands, as I would soon learn. 

But the way I tried to interact with that computer was the way that we now interact with chatbots, in a natural language way, by telling them things and asking them questions. As a writer, I'm fascinated by prompt engineering because it is much different from writing code (although the two can be closely related since GPT models have a remarkable ability to produce coherent code as well as natural language). The art of prompt engineering is a very specific kind of communication, but one which makes use of the same communication skills that all human beings learn at some point. It's important to provide clear context (but not too much), ask for a clearly defined response, and give the model some specific parameters to guide its response.

But while it makes use of those general skills, prompt engineering (in the tech realm) is a much more specialized task. Good prompt engineers are not just good communicators generally, but are also technically knowledgeable enough to know what they're looking for from a chatbot interaction, and have a good sense of how to guide the AI to a particular useful output.

In this article and hopefully later ones, I'm going to provide some examples of my own prompts and the responses I got, and also provide some great resources I've been finding elsewhere (blog posts and articles, videos, etc.). Prompt engineering is a fascinating area and it's developing by the minute, so there's a quickly-growing wealth of resources to explore.

## An Engineering Example with PySpark

I'm working on some Spark project material to put up here on the site and on GitHub for potential clients to see. I have worked with Spark for years and consider myself proficient with it, though not an expert. I've seen different file structures for PySpark files, and I thought it would be interesting to see what ChatGPT and Bard considered canonical PySpark file structure and to see if they could fill in some basic computational task.

I tried out a couple of different versions of this prompt; I'm giving the finalized one first because it's most interesting and the heart of the article. After we review this finalized version, I'll also show a preliminary version that I tried out before arriving at the final version, and which gave a strikingly different set of responses.

### My Prompt For A PySpark Job File

 Here's the prompt:


>**I'm starting a PySpark project on Google Cloud Platform. Can you please provide me with a sample .py file that contains the necessary imports and program structure for a basic PySpark program, along with some sort of basic computation (like reading a text file and counting the number of words using a lambda function)?**


### ChatGPT Response

Here's the response:

>Sure, I can provide you with a basic PySpark program that reads a text file and counts the number of words using a lambda function. Make sure you have
>PySpark installed and set up in your Google Cloud Platform environment before running the code.
>
>First, let's install PySpark using pip:
>
>```pip install pyspark```
>
>Next, create a Python file (e.g., word_count.py) and paste the following code:
>
>```python
>from pyspark.sql import SparkSession
>
>def word_count(file_path):
>    # Create a SparkSession
>    spark = SparkSession.builder.appName("WordCount").getOrCreate()
>
>    # Read the text file and split it into words using a lambda function
>    text_rdd = spark.sparkContext.textFile(file_path)
>    words_rdd = text_rdd.flatMap(lambda line: line.split(" "))
>
>    # Count the occurrences of each word
>    word_counts_rdd = words_rdd.map(lambda word: (word, 1)).reduceByKey(lambda a, b: a + b)
>
>    # Collect the results and print them
>    word_counts = word_counts_rdd.collect()
>    for word, count in word_counts:
>        print(f"{word}: {count}")
>
>    # Stop the SparkSession
>    spark.stop()
>
>if __name__ == "__main__":
>    # Replace 'path/to/your/text/file.txt' with the actual path of your text file
>    file_path = 'path/to/your/text/file.txt'
>    word_count(file_path)
>```
>
>Replace 'path/to/your/text/file.txt' in the code with the actual path of your text file in Google Cloud Storage or any accessible location in your GCP environment.
>
>The above code sets up a SparkSession, reads the text file, splits it into words using a lambda function, and then counts the occurrences of each word using another lambda function. The results are printed on the console.
>
>To run the program on Google Cloud Dataproc, you can submit it using the following command:
>
>```gcloud dataproc jobs submit pyspark --cluster <cluster-name> word_count.py```
>
>Replace `'<cluster-name>'` with the name of your Dataproc cluster.
>
>Please note that this is just a basic example to get you started. Depending on your specific requirements and the size of your data, you may need to >adjust the code and configuration accordingly.

### Analysis (ChatGPT)

I would score this response an **A+** (details below). It not only works and does what I need and expect, but conforms to a high standard of coding practice.

Before even getting to the main code, ChatGPT includes the detail on how to install PySpark in our cloud environment so the code will work when we run it. And it includes a precise instruction for execution of the code file using `gcloud`.

The answer itself worked perfectly as provided. The only change I made was (following the instructions in the response) to modify the file path in `main()` to point to a real text file. Even though I've been working with the GPT models for a few months now, it's still pretty astounding when you get an answer that's so useful and correct (especially when you know that the model isn't making use of any sort of top-down knowledge of the world, but building the answer statistically based on language patterns). The code works perfectly just as written, and I also got the correct details on installing pyspark and on how to submit the pyspark job to my DataProc cluster, even though I hadn't directly asked for those (although I had mentioned that I was starting a GCP project.)

Now, I'm not a Spark newbie, but I wanted to generate a canonical (best-practice-following) program file instead of just copying one of the ones I had used before. I was looking for something as close as possible to what the Spark project or Google Cloud would include in their documentation for such a reference file. And I'm not that familiar with using lambda functions. I'm guessing that for me to write and debug the file that ChatGPT gave me would have taken maybe a half hour - I would have consulted several example files and distilled them down into a single canonical file structure, then written and debugged the wordcount lambda function. ChatGPT provided this response in **two or three seconds**. That's pretty impressive. We're going to be talking about prompt engineering, so if I stop to wax impressed every time I get a good response, we won't get very far. But with this initial example I just wanted to take a moment to admit that I'm frankly astonished on a regular basis at how well these models can work. 

And of course think about the productivity implications, which is one of the big points of excitement surrounding GPT models. Someone that knows nothing about Python or Spark could have gotten ChatGPT to generate this working code. Well, that's not entirely true, because it would have been hard for someone who knew *nothing* about Python or Spark to write the prompt. I already knew that I was looking for piece of python code, that it needed to include library imports and follow a certain accepted program structure, and had an idea that a lambda function would be a good quick example of a basic computation that didn't get into Spark's heavy lifting yet.

I think this is a pretty good prompt (concise but still detailed), and a very good answer. This is a great example of how much GPT models can help improve productivity, because this kind of situation arises all the time. Even very knowledgeable coders spend a lot of time looking up things they don't know and debugging unanticipated problems. Someone who's already technically sound, and who has a good understanding of how to write prompts, can make significant improvements in their own productivity.

Besides the fact that it worked properly without any necessary modifications, there are several things that ChatGPT did well in this response. In order to illustrate those, let's go ahead and look at Bard's response to the same prompt.

### Bard Version

Obviously I was pretty happy with ChatGPT's response to my prompt about a PySpark job template file. Now let's look at what Bard had to say to the same prompt as given above:

>Sure, here is a sample .py file that contains the necessary imports and program structure for a basic PySpark program, along with some sort of basic computation (like reading a text file and counting the number of words using a lambda function):
>
>```python
>import sys
>import pyspark
>
># Create a SparkContext
>sc = pyspark.SparkContext()
>
># Read the text file into a Spark RDD
>text_file = sc.textFile("my_text_file.txt")
>
># Count the number of words in the text file using a lambda function
>word_counts = text_file.flatMap(lambda line: line.split(" ")).map(lambda word: (word, 1)).reduceByKey(lambda a, b: a + b)
>
># Print the word counts
>for word, count in word_counts.collect():
>    print(f"{word}: {count}")
>
># Stop the SparkContext
>sc.stop()
>```
>
>This code will first import the necessary libraries, then create a SparkContext. Next, it will read the text file into a Spark RDD. Then, it will use a lambda function to count the number of words in the text file. Finally, it will print the word counts.
>
>To run this code, you can save it as a .py file and then run it using the following command:
>
>`pyspark my_pyspark_program.py`
>
>This will start a PySpark shell and execute the code in the .py file. The output of the code will be printed to the console.
>
>I hope this helps! Let me know if you have any other questions.

### Analysis (Bard)

I give this answer an **A-**.

Bard also gave a concise code snippet that worked as-is and produced the desired output. But there are some obvious differences in structure and approach, even though the output produced by the code from these separate responses is essentially identical - a couple of notifications and a word/count list. But even to someone who isn't very knowledgable about coding, it should be apparent that, among other things, Bard's response is simplore. Now that's not necessarily a bad thing, and can sometimes be a recommendation. But in this case, the simplicity of Bard's response is a sign of a lower-quality response. Here's the list of key differences I notice, with more detailed comments to follow:

1. ChatGPT's imports were more concise and specific
2. ChatGPT followed typical modularization best practice, packaging the word count into a separate function
3. ChatGPT used Spark's session context to create an app name
4. ChatGPT followed the idiom known as the 'main guard' or 'main check', which is proper practice for programming packages and gives the program more overall structure

Let's look at point #1, the imports, first. ChatGPT only used one import statement: 
```python
from pyspark.sql import SparkSession
```

whereas Bard also used `import sys`, which (as far as I can tell) is unnecessary. The more specific import format which ChatGPT used (`from pyspark.sql import SparkSession`, which imports only the exactly functionality needed from the PySpark package instead of using `import pyspark` to import the whole library, like Bard did) is also, from my many years of Python experience, definitely the better practice in this case. You should import only what specific functionality you need instead of importing whole packages. ChatGPT wins hands down on #1 above (imports).

On point 2, modularization, this is a pretty clear win for ChatGPT as well. Even most novice programmers are familiar with the idea that it's good practice to define a block of related code as a function, which ChatGPT does explicitly with the block beginning with `def word_count(file_path):`. This keeps code more modular, reusable, and easy to maintain.

Point 3, app name declaration, is another seemingly small point that does not directly affect the ability of the code to execute, but which incorporates best practices for programming in PySpark. The app name is useful for monitoring and other purposes, and the [Apache docs](https://spark.apache.org/docs/3.1.1/api/python/reference/api/pyspark.sql.SparkSession.builder.appName.html) explain that if no application name is set, a randomly generated one will be used. So as we can see, this is not a make-or-break point, but it's another bonus detail that ChatGPT very helpfully includes (and which makes me feel comfortable referring to this prompt answer as an ideal canonical one).

Finally, on point 4, the 'main guard', ChatGPT scores more best-practice points. I further prompted ChatGPT (because I couldn't remember the exact name for this idiom), and got this answer:

>The programming idiom in Python that refers explicitly to a main function using the if __name__ == "__main__": block is commonly known as the "main guard" or "main check" idiom.
>
>In Python, the __name__ variable is a built-in variable that is automatically set for every script. When the script is the main program being executed, __name__ is set to "__main__". On the other hand, if the script is being imported as a module into another script, __name__ is set to the name of the module.
>
>By using the if __name__ == "__main__": block, you can ensure that certain code (often the main function of the script) is only executed when the script is run directly as the main program, and not when it is imported as a module in another script. This allows you to have reusable code in your Python modules that can be imported and used in other scripts without unwanted side effects.
>
>So, it is a common Python idiom to place the main functionality of your script inside a main() function and then use the if __name__ == "__main__": block to call that main() function when the script is run as the main program.


That's another great answer and explains why the 'main guard' is best practice without me having to further elaborate.

So on all four points, ChatGPT provides what most experienced programmers would, I believe, consider to be objectively better code, according to accepted Python best practices.

It's important to keep in mind, somewhat in defense of Bard, that this is a pretty short code snippet, and in this sort of context Python programmers often write code in a script-type style (as opposed to a more formal object-oriented type style). That's one of the advantages of the language: you don't have to use a bunch of class declarations and other unwieldy structure just to accomplish one small task. Honestly what Bard produced is much closer to what I would have written in this context if I was just trying to get the code working and wasn't too concerned about following every last best practice. But even though I didn't specifically ask for a 'canonical' or 'best-practice' form of the code, that's what ChatGPT gave me, and its answer is definitely better. I would score ChatGPT's answer an A+ and Bard's an A-. They're both concise and functional and well-commented, but ChatGPT's follows numerous best practices that Bard's doesn't.

Looking at this code side by side is fascinating to me, since the answers are so similar and yet so different. Bard's code worked, but I didn't learn much from it, whereas with ChatGPT's snippet I came away feeling like it had improved my abilities as a programmer.

## A Previous (Less Specific) Version of the Spark Job Prompt

There was another previous round of prompting that I did before the one detailed above that is also quite illuminating. Before deciding to include this specific Spark starter file prompt in this article, I prompted Bard for such a file, but in a less specific and clear way than I did in the version given above. The idea of using a lambda function in this context in fact came from an answer that Bard gave to that similar, but less specific, prompt. That earlier prompt was:

>**I'm creating a Spark job on a Dataproc cluster on Google Cloud for the first time. Can you give me a sample .py file so I can see the necessary imports for the job file?**

It's clear that this previous version gave less detail and was less specific about what I was looking for. When I threw it out at Bard, I was working quickly and not considering including it in a detailed write-up. But now I'm glad I worked through it, because the contrast with the more detailed version of the prompt is insightful.

Here is **Bard's response to that simpler version:**

>Sure, here is a sample .py file that you can use to create a Spark job on a Dataproc cluster on Google Cloud:
>
>```python
>import sys
>import os
>from pyspark import SparkContext
>from pyspark.sql import SparkSession
>
>def main():
>    # Create a SparkContext
>    sc = SparkContext(appName="My Spark Job")
>
>    # Create a SparkSession
>    spark = SparkSession(sc)
>
>    # Read some data from a file
>    data = spark.read.text("data.txt")
>
>    # Count the number of words in the data
>    wordCounts = data.flatMap(lambda line: line.split(" ")).map(lambda word: (word, 1)).reduceByKey(lambda a, b: a + b)
>
>    # Print the word counts
>    print(wordCounts.collect())
>
>if __name__ == "__main__":
>    main()
>```
>
>This code imports the following libraries:
>
>- sys
>- os
>- pyspark.SparkContext
>- pyspark.sql.SparkSession
>- The sys and os libraries are used for system-level operations, such as getting the current working directory. The pyspark.SparkContext library is used to create a SparkContext, which is a handle to the Spark cluster. The pyspark.sql.SparkSession library is used to create a SparkSession, which is a high-level API for working with Spark data.
>
>The main() function in the code creates a SparkContext and a SparkSession. It then reads some data from a file and counts the number of words in the data. Finally, it prints the word counts.
>
>To run this code, you can save it as a .py file and then submit it to a Dataproc cluster using the gcloud dataproc jobs submit pyspark command. For example, to submit the code to a cluster named my-cluster, you would run the following command:
>
>`gcloud dataproc jobs submit pyspark my-script.py`
>
>This will submit the job to the cluster and start it running. You can then monitor the progress of the job using the gcloud dataproc jobs list command.
>
>I hope this helps! Let me know if you have any other questions.

The code from this response, though similar to the code given to the above, more detailed prompt, did not in fact execute sucessfully. I got `AttributeError: 'DataFrame' object has no attribute 'flatMap'` at line 17, meaning that there was a problem with the implicit conversion of the DataFrame to RDD (different forms of data representation that Spark uses). Upon getting that error, I didn't give up, and followed up with Bard to see if I could gently guide it into giving me a working version. I explained the error, and Bard followed up with:

>The error message `AttributeError: 'DataFrame' object has no attribute 'flatMap'` indicates that you are trying to use the flatMap() method on a DataFrame, but the flatMap() method is only available for RDDs.
>
>To fix this error, you need to convert the DataFrame to an RDD before you call the flatMap() method. You can do this using the rdd() method on the DataFrame. For example, the following code will convert the DataFrame to an RDD and then call the flatMap() method on the RDD:

suggesting that I add the line:
```python
rdd = data.rdd()
```

and assured me that 

>This code will now run without any errors.

I decided to run the error down and see if Bard could fix its own error if I took a little bit of time to work through the situation. That was because I had run into this problem with GPT models before and have sometimes been able to find a working solution without too much trouble by being persistent with the bot. I tried the suggested change (adding the explicit conversion to RDD), but got another error. Over the next twenty minutes or so, I continued this cycle, following suggested changes, and each time getting a new error in response (along with a confident assurance that the most recent suggested code change would fix the problem). After a little while I felt like I was wasting time, since I already had a working version of the code from a different prompt, and was more concerned with the rest of the details of my Spark project and this article. 

This less specific prompt, then, revealed a more significant difference in response between ChatGPT and Bard. With a detailed and specific prompt (first version given above), both ChatGPT and Bard were able to give working answers that more or less gave me what I needed, though ChatGPT scored numerous extra points for consistently following programming best practices. But when I was somewhat vague and did not provide as much prompt detail, Bard was not able to provide a working answer, while ChatGPT still gave a very solid answer (though with a somewhat different approach due to the lack of more detailed instruction).

### ChatGPT Version

Here's the ChatGPT response to the simpler version of the prompt for a PySpark job file:

>Certainly! Below is a sample Python file for a Spark job that you can run on a Dataproc cluster on Google Cloud:
>
>
>```python
>from pyspark.sql import SparkSession
>from pyspark.sql.functions import col
>
>def main():
>    # Create a SparkSession
>    spark = SparkSession.builder \
>        .appName("Sample Spark Job") \
>        .getOrCreate()
>
>    try:
>        # Read input data from Google Cloud Storage (GCS)
>        input_path = "gs://your-bucket-name/input_data.csv"
>        df = spark.read.csv(input_path, header=True, inferSchema=True)
>
>        # Your data processing logic here
>        df_filtered = df.filter(col("some_column") > 100)
>
>        # Write the processed data back to GCS
>        output_path = "gs://your-bucket-name/output_data/"
>        df_filtered.write.csv(output_path, mode="overwrite")
>
>    finally:
>        # Stop the SparkSession
>        spark.stop()
>
>if __name__ == "__main__":
>    main()
>```
>
>Note:
>
>Replace "gs://your-bucket-name/input_data.csv" with the path to your input data file on Google Cloud Storage (GCS).
>Replace "gs://your-bucket-name/output_data/" with the desired path where you want to store the processed data on GCS.
>To run this script on your Dataproc cluster, you need to package it into a .py file and submit it using the gcloud command or Dataproc UI. Make sure you have a Dataproc cluster up and running before you submit the job.
>
>If you haven't installed the necessary packages for interacting with Google Cloud and running Spark, you can do so by running the following commands:
>
>```python
>pip install google-cloud-storage
>pip install pyspark
>```
>
>After that, you can run the Spark job by executing the following command:
>
>`spark-submit --master yarn --deploy-mode cluster your_job_file.py`
>
>Replace your_job_file.py with the name of your Python file containing the Spark job.
>
>Remember to replace the required configurations and paths according to your specific use case. This example assumes that you have a CSV file as input data, but you can adapt it to other data formats or sources as needed.

This ChatGPT response, it must be noted, will not run locally (as the other sample responses did). I knew this would be the case before I even tried it when I saw the use of the `gs://...` filename syntax (which obviously refers to locations on Google Cloud Storage). But I don't penalize ChatGPT for that in this case since I was specific that I was looking for code that would run on GCP. And, much to ChatGPT's credit, it gives a very informative answer filled with context, making it clear that the code is intended to be run on DataProc (as I asked), and recommending `pip` commands for installing pyspark and google-cloud-storage, and for executing the job file on the remote cluster.

One major observation from this less specific version of the prompt is to look at how much these two suggested code samples from ChatGPT and Bard differ. In the first version of the prompt posted in the article, which gave more context and more specific direction, the two suggested code samples (ChatGPT and Bard) were overall pretty close, though ChatGPT employed some best Python practices that Bard didn't. But if you look at the code suggestions from the less specific prompt (second version in this article), it's clear that ChatGPT and Bard are taking significantly different approaches. Bard's version is pretty locally oriented (despite the specific mention of DataProc), whereas ChatGPT very explicitly takes into account the DataProc context and provides a cloud-native answer that is much more suitable for running on a DataProc cluster.

The difference in response when the level of detail in the prompt is low is quite striking in this example. ChatGPT clearly was able to infer more about what I wanted from limited context, and provide an answer that was still quite strong. Bard obviously suffered a bit, since in fact it was unable to come up with a code snippet that would execute without errors, despite a few rounds of requestioning and informing Bard about its mistakes.

## Takeaways 

There's a lot of information to be gleaned just from comparing ChatGPT and Bard on one set of mostly similar prompts. We've gone over a lot in this post, and I'm going to wrap up the detailed analysis here. But let's take a few moments to review what we discovered in this set of comparisons:

- ChatGPT and Bard are both amazing tools, but ChatGPT is able to achieve a level of performance that's simply astonishing in a lot of cases. For writing code, ChatGPT is still your best friend. I have spent a lot of time with Bard, and it feels friendlier in some ways, and it has given me some pretty good code solutions. But the results of the direct and detailed comparison from this article show that ChatGPT gives noticably more and better detail, and is more likely to generate a proper working solution.
- Proper specificity and context are essential to effective AI prompt engineering. Without giving the bot sufficient clear information to answer your request, you simply can't expect to get a very helpful answer. A little bit of information in the prompt makes a lot of difference. The difference of about a sentence's worth of information (between the more and less detailed versions of the PySpark job file prompt) made a significant difference in the character and quality of the answers. Taking a little bit of extra time obviously pays off in spades in this sort of situation. I only spent an extra minute or so adding details to the better version of the Spark prompt question, but the results were much better for that better-developed version.
- The difference in model quality between ChatGPT and Bard shows up especially when considering the difference in prompt quality and level of detail. Bard could hang pretty close with ChatGPT when working with a detailed and specific prompt, but when working with a lower quality prompt, Bard simply wasn't able to infer enough information to give a useful (or even runnable answer). 

None of these takeaways is terribly surprising, but we fleshed them out in a lot of detail in this post. Next I think I'll do a post on mathematical reasoning based on a prompt I worked with the other day to get the bots to prove and explain why the sum of angles in a triangle is always 180 degrees. Stay tuned, because that one is quite a fascinating exercise as well, though the context is different and not as technical (at least in regards to programming languages). Thanks for reading.