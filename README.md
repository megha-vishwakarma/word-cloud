# word-cloud in pyhton  source code-

!pip install matplotlib
!pip install pandas
!pip install wordcloud
!pip install fileupload
!pip install ipywidgets
!jupyter nbextension install --py --user fileupload
!jupyter nbextension enable --py fileupload

import wordcloud
import numpy as np
from matplotlib import pyplot as plt
from IPython.display import display
import fileupload
import io
import sys





def _upload():

    _upload_widget = fileupload.FileUploadWidget()

    def _cb(change):
        global file_contents
        decoded = io.StringIO(change['owner'].data.decode('utf-8'))
        filename = change['owner'].filename
        print('Uploaded `{}` ({:.2f} kB)'.format(
            filename, len(decoded.read()) / 2 **10))
        file_contents = decoded.getvalue()

    _upload_widget.observe(_cb, names='data')
    display(_upload_widget)

_upload()

#upload a .txt  file contains any text/paragraph




def calculate_frequencies(file_contents):
    # Here is a list of punctuations and uninteresting words you can use to process your text
    punctuations = '''!()-[]{};:'"\,<>./?@#$%^&*_~'''
    uninteresting_words = ["the", "a", "to", "if", "is", "it", "of", "and", "or", "an", "as", "i", "me", "my", \
    "we", "our", "ours", "you", "your", "yours", "he", "she", "him", "his", "her", "hers", "its", "they", "them", \
    "their", "what", "which", "who", "whom", "this", "that", "am", "are", "was", "were", "be", "been", "being", \
    "have", "has", "had", "do", "does", "did", "but", "at", "by", "with", "from", "here", "when", "where", "how", \
    "all", "any", "both", "each", "few", "more", "some", "such", "no", "nor", "too", "very", "can", "will", "just"]
    
    # LEARNER CODE START HERE
    non_punctuation_text=""
    for char in file_contents:
        if char not in punctuations:
            non_punctuation_text=non_punctuation_text+char
    words=non_punctuation_text.split()
    clean_words=[]
    frequencies={}
    for word in words:
        if word.isalpha():
            if word not in uninteresting_words:
                clean_words.append(word)
    for alpha_word in clean_words:
        if alpha_word not in frequencies:
            frequencies[alpha_word]=1
        else:
            frequencies[alpha_word]+=1
    #wordcloud
    cloud = wordcloud.WordCloud()
    cloud.generate_from_frequencies(frequencies)
    return cloud.to_array()





# Display your wordcloud image

myimage = calculate_frequencies(file_contents)
plt.imshow(myimage, interpolation = 'nearest')
plt.axis('off')
plt.show()

To say Education is important is an understatement. Education is a weapon to improve one’s life. It is probably the most important tool to change one’s life. Education for a child begins at home. It is a lifelong process that ends with death. Education certainly determines the quality of an individual’s life. Education improves one’s knowledge, skills and develops the personality and attitude. Most noteworthy, Education affects the chances of employment for people. A highly educated individual is probably very likely to get a good job. In this essay on importance of education, we will tell you about the value of education in life and society.Education makes an individual a better user of technology. Education certainly provides the technical skills necessary for using technology. Hence, without Education, it would probably be difficult to handle modern machines.

People become more mature with the help of Education. Sophistication enters the life of educated people. Above all, Education teaches the value of discipline to individuals. Educated people also realize the value of time much more. To educated people, time is equal to money.

Finally, Educations enables individuals to express their views efficiently. Educated individuals can explain their opinions in a clear manner. Hence, educated people are quite likely to convince people to their point of view.
