
CharPyLS
========

JPEG-LS for Python via CharLS C++ Library
-----------------------------------------

I wrote this interface to enable easy access to the awesome [JPEG-LS](http://en.wikipedia.org/wiki/Lossless_JPEG) lossless image compression algorithm from within my Python application.  I had no need to read/write anyone else's JPEG-LS image files, but rather I needed to compress some data structures internal to my application.  This data was similar in nature to greyscale imagery such that it was an easy choice to leverage the existing CharLS C++ library I found on [codeplex.com](http://www.codeplex.com).  I did eventually incorporate some basic file I/O functionality for my unit tests, and that's why I list Pillow below as a dependency.

I have tested this code on Windows 7 x64, Windows 8 x64, and Ubuntu x64.  Note, even though this package has the odd name "CharPyLS", you will import it into your module as "jpeg_ls".  Here is a quick example of using this tool to compress an image to a buffer in memory.  For more details, check out the examples included within the source code.

    # Read in an image from an existing PNG file.
    fname_img = 'test/image.png'
    data_image = data_io.read_PIL(fname_img)

    # Compress image data to a sequence of bytes.
    data_buffer = jpeg_ls.encode(data_image)

    # Sizes.
    size_png = os.path.getsize(fname_img)
    print('Size of RGB 8-bit image data:  {:n}'.format(len(data_image.tostring())))
    print('Size of PNG encoded data file: {:n}'.format(size_png))
    print('Size of JPEG-LS encoded data:  {:n}'.format(len(data_buffer)))

    # Decompress.
    data_image_b = jpeg_ls.decode(data_buffer)

    # Compare.
    is_same = (data_image == data_image_b).all()
    print('Restored data is identical to original: {:s}'.format(str(is_same)))

The output generated by the above example should look like the following:

    Size of RGB 8-bit image data:  5038848
    Size of PNG encoded data file: 2409950
    Size of JPEG-LS encoded data:  2088357
    Restored data is identical to original: True


About JPEG-LS
=============
  - From [Wikipedia article](http://en.wikipedia.org/wiki/Lossless_JPEG): JPEG-LS (ISO-14495-1/ITU-T.87) is an accepted lossless image compression standard derived from the [Hewlett Packard LOCO algorithm](http://www.hpl.hp.com/loco).
  - From [CharLS codeplex site](http://charls.codeplex.com): CharLS is an optimized implementation of the JPEG-LS standard for lossless and near-lossless image compression. JPEG-LS is a low-complexity standard that matches JPEG 2000 compression ratios. In terms of speed, CharLS outperforms open source and commercial JPEG LS implementations.

Dependencies
============
 - Numpy
 - Cython (only for building and installing, not for everyday use)
 - Pillow (friendly fork of PIL, used here for file I/O during unit tests)
 - CharLS (source included as subfolder)
