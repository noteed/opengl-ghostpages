# The OpenGL ghostpages

These are assorted notes about 'modern' OpenGL programming, lousily
following the [manpages][] located on [opengl.org][].

Because it is quite short, it is just a single README file in markdown format;
github will happily display it nicely.

[manpages]: http://www.opengl.org/sdk/docs/man/xhtml/
[opengl.org]: http://www.opengl.org/

----------------------------------------------------------------------

## VertexAttribPointer

describe the format of vertex attribute raw data

    void glVertexAttribPointer (
      GLuint       location, 
      GLint        size, 
      GLenum       type, 
      GLboolean    normalized, 
      GLsizei      stride, 
      const GLvoid * offset);

* location
  - The numeric name of the vertex attribute for which the array will supply
  values.

* offset
  - Byte offset into the data store of the (non-zero named) buffer object
  bound to the ARRAY_BUFFER target.

### Notes:

The specifications talk about 'generic' vertex attributes to differentiate from
the old Vertex, Color, Normal (and some others) kinds of attributes whose
meaning was fixed. In the non-fixed pipeline, the purpose of the data is
specific to the shaders; i.e. put at the discretion of the programer.

For instance, a vertex attribute (singular) can be used for the position or the
texture coordinates of the vertices.

In the specifications, the location (i.e. the numeric name of the vertex
attribute) is called the 'index' (of a generic vertex attribute slot).

Offset is really that, an offset. It is called 'pointer' in the specifications
because, say, VertexPointer was initially used to describe 'vertex arrays'.

From the description above, it is clear it is necessary to have

- a named, enabled vertex attribute
- a buffer object bound to ARRAY_BUFFER

Vertex attribute names are managed with BindAttribLocation or
GetAttribLocation.  They are enabled with EnableVertexAttribArray. A buffer
object is bound to some target (here, ARRAY_BUFFER) with BindBuffer.

A default (called 'current' in the specifications) vertex attribute value may
be defined with VertexAttrib and will be used when no corresponding vertex
attribute array is enabled.

----------------------------------------------------------------------

