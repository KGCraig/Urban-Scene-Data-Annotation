# Project: Urban Scene Annotation (Instance Segmentation)

**Goal:** Provide high-precision instance segmentation for training an object recognition model.

## 1) Class Definitions

|Class Name|Class Definition|Annotation Type|
|---|---|---|
|`CAR`|Any sedan, truck, van, or SUV.|Instance Segmentation (Mask)|
|`PEDESTRIAN`|Any human present (adults/teenagers/children).|Instance Segmentation (Mask)|
|`ROAD_SURFACE`|The drivable portion of the street, curb to curb.|Semantic Segmentation (Mask)|
|`TRAFFIC_SIGN`|Any permanent street sign.|Bounding Box|

## 2) Segmentation Rules (for Masks and Polygons)

### **Mask Tightness:**

Masks must be pixel-perfect, or as close to pixel-perfect as possible. No background pixels should be included inside the mask.

- The segmentation mask will encompass the entire physical body of any `PEDESTRIAN` instance, including all worn items (clothing, hats, glasses, backpacks). It will exclude items pushed, pulled (carriages, carts), or loosely held (large bags, umbrellas) that extend significantly from the body.

### **Occlusion:**

If an object is partially blocked or hidden (occluded), annotate the visible portions only.
  
- **EXCEPTION:** If a `PEDESTRIAN` is partially occluded by a `CAR`, use your best judgment to draw the boundary of the pedestrian's body *as if* the car wasn't there.

### **Reflections and Shadows:**

DO NOT annotate any reflections or shadows. Only annotate the physical object.

- **EXCEPTION:** Use your best judgment to annotate `CAR` wheels UNLESS they are occluded by another object; If a car wheel is hidden because of shadows or lighting, continue to annotate an approximate mask for the car's wheels.

### **Attributes:**

Every annotation must have a `Visibility` attribute:

- `Visibility` **Attribute Rules:**
  - `Full` (Object is completely clear)
  - `Partial_Occlusion` (Partially hidden by another object/edge of frame)

### **Ambiguity and Clarity:**

Use these ambiguity and clarity rules to avoid guessing in your annotations.

   1) If you cannot confidently define the boundary of an object, **DO NOT** annotate it.
   2) If an object is *less than 25% visible*, is too ambiguous (looks like a blob or indistinguishable shape) or is very blurry, **DO NOT** annotate it!
   3) If an object is less than `32 X 32 pixels` or 1,024 pixels, **DO NOT** annotate it.

## 3) Bounding Box Rules (Traffic Signs)

Bounding boxes for `TRAFFIC_SIGN` objects must be drawn around the sign face only, excluding the pole or any mounting hardware.

- Do not annotate the back of a `TRAFFIC_SIGN`. Only the sign face.
- Bounding boxes must be as tight as possible around the traffic sign.

## 4) Image-Level Classification Rules

Each image must be assigned with ONE of the following tags for the entire image: `Daytime_Clear`, `Daytime_Cloudy`, `Daytime_Rainy`, `Nighttime_Clear`, `Nighttime_Cloudy`, `Nighttime_Rainy`
