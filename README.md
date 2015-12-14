COMP50 Parallel Reverse Video Search Engine

Mitchell Katz, Alex King, Isabelle Sennett, Matthew Yaspan

Sunday, December 6, 2015

Summary:
The Parallel Reverse Video Search Engine takes a video and searches a database
to see whether the query video is a clip from one of the existing videos within
the database.

This product could be used as a reverse search engine in case someone wanted to
find what video a gif came from or as copywright protection, for example.

Algorithm:
The Video Search is based off of a frame-to-frame root mean squared error
function. The RMSE function calculates the difference in brightness between
every pixel in two images. Final results are based off of the mean RMSE score
for two images. We have parallelized the search so that multiple videos can be
searched at once, and multiple chunks of a video can be searched in parallel.

Currently, our program works reliably on identical clips from a video, however
it does have trouble accounting for things like letterboxing, resolution
differences, and transformations (such as flipping across an axis)

Files:
Reverse Search Engine Files:
* framediff.py - Frame difference module. Exports one function, frame_rmse, that returns the root-mean-square error between two NumPy RGB arrays.
* chunk_compare.py - Video chunk comparison module. Exports one function, chunk_compare, that returns a list of matching sequences between the queried video and the specified database video.
* generate_jobs.py - Parallel database search module. Exports one function, server_entry, that when given a multiprocessing Queue will return a number of results for the client to expect to be added to the results queue. In effect, this allows the GUI to call the program with a query video path, watch for live additions to the results queue, and know when no more jobs will be added on.
* timeConvert.py - Short module to convert between timestamps and second count
* videoSearch.py - Wrapper module to call producer from the command line

Web Application Files:
* server.py - Code to use the Flask framework to set up a GUI
* static - the directory containing all CSS, and JavaScript Files
	* video - a subdirectory in static containing the video database
* template - the directory containing all HTML files

How to Run:

There are two ways to run the application- through the GUI which is
created as a web application using Flask. To do this:

You can also run the program via the console, using the command:

python videoSearch.py inputfile.mp4 path/to/database/ threshold

Threshold should be a percent value beteween 0-100.

You can also run it via a web application implemented with Flask. To do this, run the command

python server.py

on your command line, then open up a web browser and view the page hosted on local host port 9090.

Video Search relies on the following modules (which can be installed via PIP):
* MoviePy
* Pillow
* NumPy
* Flask
* SciPy

Note that this application relies on the MoviePy module, created by GitHub user
Zulko https://github.com/Zulko, which in turn calls the FFMPEG file