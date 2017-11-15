# Why the results are bad when I use opencv c++ function resize() to downsacle the image and use the VDSR to upscale the image ?
  It's usually caused by the difference of opencv c++ function resize() and matlab imrsize(). In matlab, the Anti-aliasing is default enabled. But the Anti-aliasing is unenabled by default in opencv c++ function resize(). You use matlab imrsize() to process the trainning data and get the model by trainning. but use opencv c++ function resize() to process the test image(down scale the image), so the results are bad. The same resize function should be used when trainning data and test data are processed.

# Anti-Aliasing
introduce the difference of Matlab imresize and the opencv resize

# Matlab imresize() && Python cv2.resize() && c++/c cv::resize()
 Maybe you are familiar with theses three functions, they can enlarge or shrunk images according to their parameters. But there are some default parameters should be noted. In Matlab imresize() and cv2.resize(), the Anti-Aliasing is default on, and you can use like this:
 
 imresize(im_label,scale,'bicubic','Anti-Aliasing','true') or imresize(im_label,scale,'bicubic') in Matlab
 cv2.resize(img, None, fx=scale_ratio, fy=scale_ratio, interpolation=cv2.INTER_CUBIC) in OpenCV
 
 But in c++ opencv, there are no Anti-aliasing by default. So the resaults are different from Matlab imresize() && Python cv2.resize(), when you downscale an image.
 
 If you do not use Anti-Aliasing, you can use like this:
 
 imresize(im_label,scale,'bicubic','Anti-Aliasing','false') in Matlab
 cv2.resize(img, None, fx=scale_ratio, fy=scale_ratio, interpolation=cv2.INTER_NEAREST) in OpenCV
