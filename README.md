# Weiner_Filter
The most important technique for removal of blur in images due to linear motion or unfocussed optics is the Wiener filter. From a signal processing standpoint, blurring due to linear motion in a photograph is the result of poor sampling. Each pixel in a digital representation of the photograph should represent the intensity of a single stationary point in front of the camera. Unfortunately, if the shutter speed is too slow and the camera is in motion, a given pixel will be an amalgram of intensities from points along the line of the camera's motion. This is a two-dimensional analogy to

G(u,v)=F(u,v).H(u,v)
where F is the fourier transform of an "ideal" version of a given image, and H is the blurring function. In this case H is a sinc function: if three pixels in a line contain info from the same point on an image, the digital image will seem to have been convolved with a three-point boxcar in the time domain. Ideally one could reverse-engineer a Fest, or F estimate, if G and H are known. This technique is inverse fitering.


2-D Fourier Transform of Horizontal Blur
It should be noted that the image restoration tools described here work in a similar manner for cases with blur due to incorrect focus. In this case the only difference is in the selection of H. The 2-d Fourier transform of H for motion is a series of sinc functions in parallel on a line perpendicular to the direction of motion; and the 2-d Fourier transform of H for focus blurring is the sombrero function, described elsewhere.

In the real world, however, there are two problems with this method. First, H is not known precisely. Engineers can guess at the blurring function for a given circumstance, but determination of a good blurring function requires lots of trial and error. Second, inverse filtering fails in some circumstances because the sinc function goes to 0 at some values of x and y. Real pictures contain noise which becomes amplified to the point of destroying all attempts at reconstruction of an Fest.

The best method to solve the second problem is to use Wiener filtering. This tool solves an estimate for F according to the following equation:

Fest(u,v) = |H(u,v)|^2.G(u,v)/(|H(u,v)|^2.H(u,v) + K(u,v))
K is a constant chosen to optimize the estimate. This equation is derived from a least squares method. An example of Wiener filtering is given below.


An ideal version of the cover of the Joshua Tree album by U2. All examples used are 256x256 pixels, but the same principles apply if size is varied. Also, the examples are all grayscale but the principles are valid for color photos by applying filtering techniques seperately to rgb elements.

The same photograph, with some blurring due to motion and noise due to poor development.>

Random gaussian noise (multiplied here by a factor of 100) added into the blurred version of the photo.

Reconstructed photograph, e.g. f estimate, through Wiener filtering
In closing, it should be noted that Weiner filters are far and away the most common deblurring technique used because it mathematically returns the best results. Inverse filters are interesting as a textbook starting point because of their simplicity, but in practice Wiener filters are much more common. It should also be re-emphasized that Wiener filtering is in fact the underlying premise for restoration of other kinds of blur; and being a least-mean-squares technique, it has roots in a spectrum of other engineering applications.
