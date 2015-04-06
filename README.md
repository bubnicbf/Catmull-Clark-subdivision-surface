# Catmull-Clark-subdivision-surface
The Catmull–Clark algorithm is a technique used in computer graphics to create smooth surfaces by subdivision surface modeling.

Catmull–Clark surfaces are defined recursively, using the following refinement scheme:

Start with a mesh of an arbitrary polyhedron. All the vertices in this mesh shall be called original points.

  - For each face, add a face point
    - Set each face point to be the average of all original points for the respective face.
  - For each edge, add an edge point.
    - Set each edge point to be the average of the two neighbouring face points and its two original endpoints.
  - For each face point, add an edge for every edge of the face, connecting the face point to each edge point for the face.
  - For each original point P, take the average F of all n (recently created) face points for faces touching P, and take the average R of all n edge midpoints for edges touching P, where each edge midpoint is the average of its two endpoint vertices. Move each original point to the point

$$
\frac{F + 2R + (n-3)P}{n}.
$$

This is the barycenter of P, R and F with respective weights (n − 3), 2 and 1.

  - Connect each new vertex point to the new edge points of all original edges incident on the original vertex.
  - Define new faces as enclosed by edges.

The new mesh will consist only of quadrilaterals, which in general will not be planar. The new mesh will generally look smoother than the old mesh.

Repeated subdivision results in smoother meshes. It can be shown that the limit surface obtained by this refinement process is at least $\mathcal{C}^1$ at extraordinary vertices and $\mathcal{C}^2$ everywhere else (when n indicates how many derivatives are continuous, we speak of $\mathcal{C}^n$ continuity). After one iteration, the number of extraordinary points on the surface remains constant.

The arbitrary-looking barycenter formula was chosen by Catmull and Clark based on the aesthetic appearance of the resulting surfaces rather than on a mathematical derivation, although Catmull and Clark do go to great lengths to rigorously show that the method yields bicubic B-spline surfaces.

####Example
Implements the Catmull-Clark surface subdivision, which is an algorithm that maps from a surface (described as a set of points and a set of polygons with vertices at those points) to another more refined surface. The resulting surface will always consist of a mesh of quadrilaterals.

Then each face is replaced by new faces made with the new points,

for a triangle face (a,b,c):

     - (a, edge_pointab, face_pointabc, edge_pointca)
     - (b, edge_pointbc, face_pointabc, edge_pointab)
     - (c, edge_pointca, face_pointabc, edge_pointbc)

for a quad face (a,b,c,d):

     - (a, edge_pointab, face_pointabcd, edge_pointda)
     - (b, edge_pointbc, face_pointabcd, edge_pointab)
     - (c, edge_pointcd, face_pointabcd, edge_pointbc)
     - (d, edge_pointda, face_pointabcd, edge_pointcd)
   
   
