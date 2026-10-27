# QuadratFindR

![QuadratDetectR title image](QuadratDetectR_title_pic.jpg)

`QuadratFindR` identifies 1 m² quadrats in ground-based LiDAR point clouds. The workflow uses reflective tape placed around each quadrat as a visual and geometric marker.

This workflow was developed using data from piñon-juniper woodland plots sampled as part of [Nate Beine's master's thesis](https://www.proquest.com/docview/3344191296?pq-origsite=gscholar&fromopenview=true).

## How quadrats are identified

`QuadratDetectR` locates 1 m² quadrats in ground-based LiDAR point clouds by using the reflective tape placed around each quadrat as a visual and geometric marker. The general workflow is:

1. **Load the LiDAR point cloud**

   The script reads a TLS or MLS point cloud containing the surveyed ground surface and any reflective quadrat markers.

2. **Identify reflective tape returns**

   Reflective tape produces distinctive, high-intensity returns in the LiDAR data. The point cloud is filtered to retain points that are likely to belong to the tape rather than vegetation, soil, or other objects.

3. **Group nearby candidate points**

   The remaining points are grouped spatially so that returns belonging to the same physical quadrat are treated as a single candidate. Small, isolated groups can be removed as noise.

   ![Candidate reflective-tape point clusters before fitting](Quadrat_findR_blue_quads.jpg)

4. **Fit a square to each candidate**

   For each candidate group, the script estimates the quadrat's position, orientation, and dimensions. A fitted square is then drawn around the detected tape points.

   ![Blue fitted squares around identified quadrats](Quadrat_findR_blue_quads.jpg)

5. **Check the fitted quadrats**

   The fitted squares can be inspected to confirm that they align with the reflective tape and represent the intended 1 m² quadrats. This step is useful for identifying false detections, overlapping quadrats, or poor-quality fits.

6. **Extract points within each quadrat**

   Once the quadrat boundaries have been identified, the script selects the LiDAR points inside each 1 m² square. These extracted points can then be saved or used for downstream analyses of vegetation structure and composition.

   ### Point-cloud clipping workflow

   <table>
     <tr>
       <td align="center">
         <strong>Original point cloud</strong><br>
         <img src="QuadratDetectR_point_cloud.jpg" alt="Original LiDAR point cloud containing quadrats" width="420">
       </td>
       <td align="center" style="font-size: 32px; vertical-align: middle;">
         &nbsp;→&nbsp;
       </td>
       <td align="center">
         <strong>Extracted quadrats</strong><br>
         <img src="QuadratDetectR_extracted_quads.jpg" alt="Extracted LiDAR quadrats" width="420">
       </td>
     </tr>
   </table>

### Suggested workflow

The complete process is:

> Raw point cloud → reflective tape filtering → candidate clusters → fitted squares → extracted quadrat point clouds

The point-cloud clipping step is illustrated below:

![Point-cloud clipping workflow](QuadratDetectR_point_cloud.jpg)

→

![Extracted quadrats](QuadratDetectR_extracted_quads.jpg)
