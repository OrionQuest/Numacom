.. _sec-matrices:

Matrices
--------

Suppose we have :math:`n` vectors :math:`v^1,v^2,\ldots,v^n\in\mathbb R^m`.
There are several options available to us for denoting this set, either by writing each
one individually as a separate column vector:

.. math::

    v^1=\left(
        \begin{array}{c}
        v^1_1 \\
        v^1_2 \\
        \vdots \\
        v^1_m
        \end{array}
    \right), v^2=\left(
        \begin{array}{c}
        v^2_1 \\
        v^2_2 \\
        \vdots \\
        v^2_m
        \end{array}
    \right),\ldots,v^n=\left(
        \begin{array}{c}
        v^n_1 \\
        v^n_2 \\
        \vdots \\
        v^n_m
        \end{array}
    \right)

or by adopting the more efficient notation of combining all of them into a single :math:`m\times n` matrix:

.. math::
    
    \left(
    \begin{array}{cccc}
    \vert & \vert & & \vert \\
    v^1 & v^2 & \ldots & v^n \\
    \vert & \vert & & \vert
    \end{array}
    \right) = \left(
    \begin{array}{cccc}
    v^1_1 & v^2_1 & \ldots & v^n_1 \\
    v^1_2 & v^2_2 & \ldots & v^n_2 \\
    \vdots & \vdots & \ddots & \vdots \\
    v^1_m & v^2_m & \ldots & v^n_m
    \end{array}
    \right)

In general, an :math:`m\times n` matrix :math:`A\in\mathbb R^{m\times n}` is written as:

.. math::

    A = \left(
    \begin{array}{cccc}
    A_{11} & A_{12} & \ldots & A_{1n} \\
    A_{21} & A_{22} & \ldots & A_{2n} \\
    \vdots & \vdots & \ddots & \vdots \\
    A_{m1} & A_{m2} & \ldots & A_{mn}
    \end{array}
    \right)

In the example above, :math:`A_{ij}=v^j_i`. `NumPy <http://www.numpy.org/>`_ has a ``matrix`` class to conveniently define
:math:`m\times n` matrices, as shown below: ::

    >>> a=np.matrix([[1,2,3],[4,5,6],[7,8,9]])
    >>> a
    >>> matrix([[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]])

Note that `NumPy <http://www.numpy.org/>`_ defines the individual elements of
the matrix by specifying the rows, *not* the columns. Such an ordering of the
matrix elements is called a *row-major* ordering. On the other hand, if the data was specified
column-by-column, it would be called a *column-major* ordering. You are probably familiar
with the :math:`n\times n` *identity matrix* defined as:

.. math::

    I_{n\times n} = \left(\begin{array}{cccc}
    \vert & \vert & & \vert \\
    e^1 & e^2 & \ldots & e^n \\
    \vert & \vert & & \vert
    \end{array}
    \right) = \left(\begin{array}{ccccc}
    1 & 0 & \ldots & 0 & 0 \\
    0 & 1 & \ldots & 0 & 0 \\
    \vdots & \vdots & \ddots & \vdots & \vdots \\
    0 & 0 & \ldots & 1 & 0 \\
    0 & 0 & \ldots & 0 & 1
    \end{array}
    \right)

Matrix-Vector Product
~~~~~~~~~~~~~~~~~~~~~

Let :math:`x\in\mathbb R^{n\times 1}` be an :math:`n`-dimensional column vector
and :math:`A\in\mathbb R^{m\times n}` be an :math:`m\times n` matrix. The
matrix-vector product :math:`b=Ax` is the :math:`m`-dimensional vector defined
as:

.. math::

    b = \left(\begin{array}{c}
    b_1 \\
    b_2 \\
    \vdots \\
    b_m
    \end{array}
    \right),\mbox{ where }b_i = \sum_{j=1}^n A_{ij}x_j\mbox{ for all }1\leq i\leq m

Note that *all* matrices are *linear* operators, i.e., if :math:`x,y\in\mathbb R^{n\times 1}`
are two arbitrary :math:`n`-dimensional vectors, and :math:`\alpha\in\mathbb R`
is an arbitrary scalar, then it follows that:

.. math::

    A(x+y) &=& \enspace Ax + Ay \\
    A(\alpha x) &=& \enspace \alpha Ax

Matrix-vector products can be computed in `NumPy <http://www.numpy.org/>`_ using
the ``dot`` operator, as shown below: ::

    >>> a=np.matrix([[1,2,3],[4,5,6],[7,8,9]])
    >>> b=np.array([4,5,9])
    >>> a.dot(b)
    array([ 41,  95, 149])

.. topic:: Example: Image Blurring

    To illustrate the power of the abstraction that matrix-vector products
    provide, we will show an example from image processing where we will
    blur an image by casting the problem as a matrix-vector multiplication.
    However, first we must outline how to read an image in `Python <https://www.python.org/>`_
    using the ``matplotlib`` package. Consider reading this `image <_images/chill.jpg>`_: ::

        >>> import matplotlib.pyplot as plt
        >>> I=plt.imread('chill.jpg')
        >>> plt.imshow(I)
        <matplotlib.image.AxesImage object at 0x7f22b353d390>
        >>> plt.show()

    The above sequence of commands should display the following image:

    .. image:: images/color_plot.png
        :height: 612px
        :width: 812px
        :scale: 75%
        :align: center

    In our case, it is more convenient to operate on grayscale images. We
    will use the `PIL <http://www.pythonware.com/products/pil/>`_ package in `Python <https://www.python.org/>`_
    for this purpose. ::

        >>> import numpy as np
        >>> import matplotlib.pyplot as plt
        >>> from PIL import Image
        >>> fname='chill.jpg'
        >>> image = Image.open(fname).convert("L")
        >>> arr = np.asarray(image)
        >>> plt.imshow(arr, cmap='gray')
        <matplotlib.image.AxesImage object at 0x7fa3da005390>
        >>> plt.show()

    The above commands should display the following image:

    .. image:: images/grayscale_plot.png
        :height: 612px
        :width: 812px
        :scale: 75%
        :align: center

    To blur the image, we will perform the following simple operation, which
    replaces the grayscale value at every pixel by the weighted average of
    its neighbors:

    .. math::
        \textsf{pixel} \leftarrow \frac{1}{8}(4\cdot\textsf{pixel} + \textsf{pixel}_\textsf{north} + \textsf{pixel}_\textsf{south} + \textsf{pixel}_\textsf{east} + \textsf{pixel}_\textsf{west})

    Since our blurring code is substantially more complex than anything else we
    have encountered so far, for convenience of execution, we will copy all the
    code into a file named ``blur.py``, as shown below: ::

        # blur.py
        import numpy as np
        import matplotlib.pyplot as plt
        from PIL import Image
        from scipy.sparse import lil_matrix
        
        # read image file
        fname = 'chill.jpg'
        image = Image.open(fname).convert("L")
        arr = np.asarray(image)
        arr.setflags(write = 1)
        
        # initialize blurring matrix
        m = arr.shape[0]
        n = arr.shape[1]
        dofs = m*n
        A = lil_matrix((dofs,dofs))
        A.setdiag(np.ones(dofs))
        for i in range(1,m-1):
            for j in range(1,n-1):
                A[n*i+j,n*i+j] = 4./8.
                A[n*i+j,n*(i-1)+j] = 1./8.
                A[n*i+j,n*(i+1)+j] = 1./8.
                A[n*i+j,n*i+j-1] = 1./8.
                A[n*i+j,n*i+j+1] = 1./8.
        A = A.tocsr()
        
        # Blurring function - converts image to a vector, multiplies by
        # the blurring matrix, and copies the result back into the image
        def blur():
            x = np.zeros(shape=(dofs,1))
            for i in range(0,m):
                for j in range(0,n):
                    x[n*i+j] = arr[i,j]
        
            y = A.dot(x)
            for i in range(0,m):
                for j in range(0,n):
                    arr[i,j] = y[n*i+j]
        
        # Execute the blurring function 20 times
        for i in range(0,20):
            blur()
        
        # Display the blurred image
        plt.imshow(arr,cmap='gray')
        plt.show()

    Several new concepts have been introduced in the code above. The image array
    ``arr`` can be thought of as a column vector ``x`` so that it can be
    multiplied by a matrix. Here, we see the generality of the concept of a
    vector -- an :math:`m\times n` image corresponds to a :math:`mn`-dimensional
    vector. We first construct a :math:`mn\times mn` matrix :math:`A` to encode
    the blurring action. Since densely allocating this matrix would incur a
    substantial memory overhead, we allocate a *sparse* matrix instead using the
    ``scipy.sparse`` package. A sparse matrix only stores non-zero entries in a
    matrix, resulting in significant memory savings. The ``lil_matrix`` format
    allows us to set individual elements in the matrix, and the ``tocsr``
    function converts it to the *compressed sparse row* format. Several other
    formats are available, as explained `here <https://docs.scipy.org/doc/scipy/reference/sparse.html>`_.
    The ``blur`` function first converts the :math:`m\times n` image array into a
    :math:`mn\times 1` vector, multiplies it by the blurring matrix,
    and stores the result back into the image. We run this function :math:`20`
    times to exaggerate the overall effect. To run the above code, simply
    execute the following command: ::

        >>> python blur.py

    This may take some time depending upon the speed of your computer, because
    the size of the matrices and vectors is somewhat large.
    Finally, the following blurred result should be displayed upon completion:

    .. image:: images/blurred_plot.png
        :height: 612px
        :width: 812px
        :scale: 75%
        :align: center

    Sparse matrices are extremely useful in practice, because the majority of
    matrices encountered in real world applications tend to be sparse. We will
    see many more examples of their usage in later sections.
        

Suppose we consider the individual columns :math:`v^1,v^2,\ldots,v^n` of
:math:`A`, as shown above. Then the matrix-vector product :math:`b` can be
re-written as a *linear combination* of the columns of :math:`A`, i.e., :math:`b=Ax=\sum_{i=1}^n x_iv^i`.
This relation can be schematically depicted as follows:

.. math::

    \left(\begin{array}{c}
    \vert \\
    b \\
    \vert
    \end{array}\right) = \left(\begin{array}{cccc}
    \vert & \vert & & \vert \\
    v^1 & v^2 & \ldots & v^n \\
    \vert & \vert & & \vert
    \end{array}\right)\left(\begin{array}{c}
    x_1 \\
    x_2 \\
    \vdots \\
    x_n
    \end{array}\right) = x_1\left(\begin{array}{c}
    \vert \\
    v^1 \\
    \vert
    \end{array}\right) + x_2\left(\begin{array}{c}
    \vert \\
    v^2 \\
    \vert
    \end{array}\right) + \ldots + x_n\left(\begin{array}{c}
    \vert \\
    v^n \\
    \vert
    \end{array}\right)

Traditionally, we are used to viewing the relation :math:`Ax=b` as the *action*
of :math:`A` on :math:`x` to produce :math:`b`. The equation above is a
different interpretation that suggests, in contrast, that :math:`x` acts on
:math:`A` to produce :math:`b`. The set of all :math:`m`-dimensional vectors
:math:`b` that can be written as :math:`Ax` for some :math:`n`-dimensional
vector :math:`x` constitute the *column space* of :math:`A`. The *rank* of
:math:`A` is the dimension of its column space, i.e., the number of linearly
independent columns of :math:`A`.
Also, note how the dimensions of the result
:math:`b` are dependent on the dimensions of :math:`A` and :math:`x`:

.. math::

    b_{m\times 1} = A_{m\times n}\cdot x_{n\times 1}

The "middle" dimension :math:`n` has to be the same for both :math:`A` and
:math:`x` and is consumed as a result of the multiplication. This same principle also applies to the case of multiplying two arbitrary matrices,
i.e., if :math:`A\in\mathbb R^{m\times n}` and :math:`B\in\mathbb R^{n\times
p}` are two matrices, then their product :math:`C=A\cdot B\in\mathbb R^{m\times p}`. The ``dot`` operator
in `NumPy <http://www.numpy.org/>`_ can also be used for multiplying two
matrices, as shown below: ::

    >>> a = np.matrix([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
    >>> a
    matrix([[ 1,  2,  3,  4],
            [ 5,  6,  7,  8],
            [ 9, 10, 11, 12]])
    >>> b = np.matrix([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])
    >>> b
    matrix([[ 1,  2,  3],
            [ 4,  5,  6],
            [ 7,  8,  9],
            [10, 11, 12]])
    >>> a.dot(b)
    matrix([[ 70,  80,  90],
            [158, 184, 210],
            [246, 288, 330]])

Matrix Transpose
~~~~~~~~~~~~~~~~

Another operator on matrices that is quite useful is the *transpose* operator.
The transpose of a matrix :math:`A\in\mathbb R^{m\times n}` is denoted as
:math:`A^T\in\mathbb R^{n\times m}`, and is defined as:

.. math::

    A^T = \left(\begin{array}{cccc}
    A_{11} & A_{21} & \ldots & A_{m1} \\
    A_{12} & A_{22} & \ldots & A_{m2} \\
    \vdots & \vdots & \ddots & \vdots \\
    A_{1n} & A_{2n} & \ldots & A_{mn}
    \end{array}\right)

Thus, :math:`(A^T)_{ij}=A_{ji}`, i.e., the transpose of a matrix is obtained by
*flipping* the original matrix over its diagonal. The ``transpose`` operator in `NumPy <http://www.numpy.org/>`_
can be used for computing the transpose of a given matrix, as shown below: ::

    >>> a = np.matrix([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
    >>> a
    matrix([[ 1,  2,  3,  4],
            [ 5,  6,  7,  8],
            [ 9, 10, 11, 12]])
    >>> a.transpose()
    matrix([[ 1,  5,  9],
            [ 2,  6, 10],
            [ 3,  7, 11],
            [ 4,  8, 12]])
