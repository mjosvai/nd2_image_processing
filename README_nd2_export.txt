README: ND2 MAX Projection Conversion Macros for Fiji/ImageJ
=====================================================================

Author: [Your Name]
Last updated: [Date]

These macros automate the export and visualization of multi-channel 
microscopy images saved as Nikon .nd2 files (after manual maximum 
intensity projection). Two versions are provided:

  1. ND2_4CH_Export.ijm   → for 4-channel images (R, G, B, W)
  2. ND2_3CH_Export.ijm   → for 3-channel images (R, G, B)

Both macros:
  • Save individual channel TIFF and JPEG files
  • Generate multi-channel composite images with scale bars
  • Automatically adjust scale bar size based on objective magnification
  • Save all outputs in the same directory as the source file

---------------------------------------------------------------------
REQUIREMENTS
---------------------------------------------------------------------

• Fiji (recommended version: 2.15.0 or later)
  - Use Fiji, not plain ImageJ, since Fiji includes Bio-Formats 
    which is required for .nd2 file support.

• Input files must be:
  - Maximum intensity projection ND2 files
  - Containing either 3 (RGB) or 4 (RGBW) fluorescence channels
  - Single image, not a full Z-stack or time series

• Filenames must include the magnification keyword:
  “20X”, “40X”, “60X”, or “100X”
  → The macro uses this to calculate the correct scale bar width.

Example:
    Sample1_40X_MAX.nd2
    CellLineA_60X_Control.nd2

---------------------------------------------------------------------
BEFORE RUNNING
---------------------------------------------------------------------

1. Open your .nd2 file in Fiji.
   (Fiji will automatically use Bio-Formats to import ND2 files.)

2. Create a maximum intensity projection manually:
   Image → Stacks → Z Project → [Projection Type: Max Intensity]

3. Confirm that the resulting image is a *single composite image*
   with either 3 or 4 channels.

---------------------------------------------------------------------
RUNNING THE MACRO
---------------------------------------------------------------------

1. Open the appropriate macro file:
   Plugins → Macros → Edit... → Select ND2_3CH_Export.ijm or ND2_4CH_Export.ijm

2. With your projected image open, run the macro:
   Plugins → Macros → Run...

3. When prompted, choose the directory where you want to save the output files.

4. The macro will automatically:
   - Duplicate and save a backup of the original image
   - Split channels into individual TIFF and JPEG images
   - Create merged composite images with labeled scale bars

---------------------------------------------------------------------
OUTPUT FILES
---------------------------------------------------------------------

All outputs are saved in the same folder as the source ND2 file.

**For 3-channel (RGB) version:**
  - Individual channels:
      _R.tif, _R.jpg
      _G.tif, _G.jpg
      _B.tif, _B.jpg
  - Composite images:
      _RB.tif, _RB.jpg
      _GB.tif, _GB.jpg
      _RGB.tif, _RGB.jpg
  - Raw duplicate backup:
      _MAXRAW.tif

**For 4-channel (RGBW) version:**
  - Individual channels:
      _R.tif, _R.jpg
      _G.tif, _G.jpg
      _B.tif, _B.jpg
      _W.tif, _W.jpg
  - Composite images:
      _RB, _GB, _BW, _RBW, _RGB, _GBW, _RGBW (each as TIFF + JPEG)
  - Raw duplicate backup:
      _MAXRAW.tif

Each composite includes a white scale bar automatically positioned 
in the lower-right corner.

---------------------------------------------------------------------
TROUBLESHOOTING
---------------------------------------------------------------------

• “Error: File not found” 
  → Ensure the image window name still includes “.nd2”.
    The macro uses this to generate filenames.

• “Scale bar too large or too small” 
  → Check that the filename contains one of the required magnification tags
    (20X, 40X, 60X, or 100X).

• “Channels are out of order or wrong colors” 
  → Confirm the channel order from your ND2 export matches:
      -0003 = R, -0002 = G, -0001 = B (for 3-channel)
      -0004 = W, -0003 = R, -0002 = G, -0001 = B (for 4-channel)
    If your microscope exports in a different order, edit the macro accordingly.

• If ND2 files fail to open
  → Make sure Fiji is up to date and that Bio-Formats is enabled:
      Plugins → Bio-Formats → Bio-Formats Plugins Configuration...

---------------------------------------------------------------------
NOTES AND RECOMMENDATIONS
---------------------------------------------------------------------

• Run macros one file at a time (they are not batch-compatible by default).
• For batch processing, use “Process → Batch → Macro…” and select 
  the appropriate macro file.
• Review generated images for channel alignment and brightness 
  before publication.
• The macros can be modified to include overlays, annotations, or 
  different composite combinations if needed.