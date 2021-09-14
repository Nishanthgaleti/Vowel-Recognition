Preface:
Some important notes. Kindly make sure that you go through these:


* All files should be present in the same directory.
* The same project holds the code for with and wihtout the recording module.
* As inputs, presently we have 5 utterances each of each of the 5 vowels a, e, i, o and u. As testing, we have 10 utterances of each vowel. 
The number of training and testing files taken are immutable (5 and 10 respectively are hardcoded and cannot be changed).
* This document has been created and coded to be compatible with MS Visual Studio 2010. Launch VS2010, go to Open project/solution -> (folder) assignment2 -> (VC++  project) assignment2. In case you don’t have VS2010, go to Open ->  (folder) assignment1a -> (C++ source file) assignment1a.cpp. 
* Some library functions used here are compatible with VS2010 only, so might not work elsewhere. In this case, in the code, use snprintf() in place of _snprintf().
  Moreover, “stdafx.h” is defined for VC++ project only. In case you don’t have VS2010, replace the line #include “stdafx.h” with #include <stdio.h>.
* For convenience, some important parameters have been pre-defined at the top. These can be fine-tuned to see changes in the results.


Steps to follow during code run:

===> TRAINING 
* As soon as the program starts running, the training process is started, which generates the reference files for each of the vowels.
A variable called force_stop_training is kept for choosing whether to allow training or not. If you already have the reference files after training once and want to 
skip training further, set it as 1; otherwise leave it as it is (set to 0).

* For each vowel and each utterance of it, the following steps are done during training:
	- dc_remover(): removes dc component from text file.
	- normalize_waveform(): normalizes data.
	- extract_frames(): 5 frames from the steady part of normalized data are extracted.
	- compute_r_i(): calculates Ri values.
	- compute_coefficients_Durbin(): calculates LP coefficients (Ai values) using Durbin's algorithm.
	- compute_cepstral_coefficients(): calculates Ci values and applies a raised sine window on it to get resultant Ci values.
	- The Ci values for each vowel gives us a matrix called c_vowel (dimensions are 25 X 12 - (5 utterances x 5 frames) x (12 Ci values))
	- calculate_avg_ci_for_vowel(): calculates a matrix that gives the reference ci values for a vowel. The computation procedure is given in the comment section in the code. It gives us a (5 x 12) matrix. It is stored in a file.
	
* Hence we get 5 such reference files after training is done. The progress is shown in the console using messages.

===>TESTING
* Once training is complete, the program enters a menu-driven section. It contains mainly two sections:
	1. Recognize on own vowel file: It starts testing on 10 utterances of each vowel file and prints respective accuracies.
	2. Recognize on live recording: It prompts you to enter the recording interval (like 2 (in secs.)) - speak up any vowel. When "stop recording" shows on screen, hit any key and it moves forward.

	- All the functions used and their usages are mentioned as comments inside the code.
	
* Accuracies for each vowel as well as overall accuracies are also printed.

NOTE: Training and testing filenames are created dynamically within a loop. No. of training and testing files are hardcoded as 5 and 10. So, for any vowel, file no. 1 to 5 are used as training, and 6 to 15 are used as testing.
