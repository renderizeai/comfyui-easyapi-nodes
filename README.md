# comfyui-easyapi-nodes
Custom nodes and features to extend API interface development.

Nodes that convert to base64 are output nodes. WebSocket messages will include `base64Images` and `base64Type`.
(See the `ImageToBase64Advanced` class in `ImageNode.py`, or inspect with browser DevTools → Network.)

Tips:
Base64 strings are long, which may cause UI lag and bandwidth issues.
If possible, upload the image to an OSS (Object Storage Service), then use `LoadImageFromURL`.
This project doesn’t provide an OSS upload node—you'll need to implement it yourself.

# Installation

Method 1: Install via ComfyUI-Manager  
Method 2: In the root directory of your ComfyUI install, run:

```
cd custom_nodes
git clone https://github.com/renderizeai/comfyui-easyapi-nodes.git
cd comfyui-easyapi-nodes
pip install -r requirements.txt
```

# Upgrade

```
cd custom_nodes/comfyui-easyapi-nodes
git pull
```

# Node List (Partial)

| Output? | Node Name                  | Description |
|---------|----------------------------|-------------|
| ✗       | LoadImageFromURL           | Load image from a network URL, one per line |
| ✗       | LoadMaskFromURL            | Load mask from a network URL, one per line |
| ✗       | Base64ToImage              | Convert base64 string to image |
| ✗       | Base64ToMask               | Convert base64 string to mask |
| ✗       | ImageToBase64Advanced      | Convert image to base64 (choose type: image or mask) |
| ✗       | ImageToBase64              | Convert image to base64 (imageType=["image"]) |
| ✔       | MaskToBase64Image          | Convert mask to base64 (imageType=["mask"]) |
| ✔       | MaskImageToBase64          | Convert mask image to base64 (imageType=["mask"]) |
| ✗       | LoadImageToBase64          | Load local image and convert to base64 |
| ✔       | SamAutoMaskSEGS            | Get semantic segmentations in coco_rle/uncompressed_rle |
| ✗       | SamAutoMaskSEGSAdvanced    | Same as above, with adjustable SAM params |
| ✗       | MaskToRle                  | Convert mask to RLE format |
| ✗       | RleToMask                  | Convert RLE back to mask |
| ✗       | InsightFaceBBOXDetect      | Detect faces and draw indexed bounding boxes |
| ✗       | ColorPicker                | Color selection tool |
| ✗       | IntToNumber                | Convert integer to number |
| ✗       | StringToList               | Convert string to list |
| ✗       | IntToList                  | Convert integer to list |
| ✗       | ListMerge                  | Merge two lists |
| ✗       | JoinList                   | Join list elements into string with separator |
| ✔       | ShowString                 | Display string value (from message key) |
| ✔       | ShowInt                    | Display integer value (from message key) |
| ✔       | ShowFloat                  | Display float value (from message key) |
| ✔       | ShowNumber                 | Display number value (from message key) |
| ✔       | ShowBoolean                | Display boolean value (from message key) |
| ✗       | ImageEqual                 | Check if two images are equal |
| ✗       | SDBaseVerNumber            | Detect if SD version is 1.5 or XL |
| ✗       | ListWrapper                | Wrap into a list |
| ✗       | ListUnWrapper              | Unwrap list and iterate over elements |
| ✗       | BboxToCropData             | Convert BBox to cropData for WAS nodes |
| ✗       | BboxToBbox                 | Convert between (x,y,w,h) and (x1,y1,x2,y2) |
| ✗       | BboxesToBboxes             | Same as above, but for lists |
| ✗       | SelectBbox                 | Select one BBox from list |
| ✗       | SelectBboxes               | Select multiple BBoxes from list |
| ✗       | CropImageByBbox            | Crop image using BBox |
| ✗       | MaskByBboxes               | Draw mask from BBoxes |
| ✗       | SplitStringToList          | Split string into list of str/int/float/bool |
| ✗       | IndexOfList                | Get item by index from list |
| ✗       | IndexesOfList              | Get multiple items by index |
| ✗       | StringArea                 | Multiline text input |
| ✗       | ForEachOpen                | Loop start |
| ✗       | ForEachClose               | Loop end |
| ✗       | LoadJsonStrToList          | Convert JSON string to object list |
| ✗       | ConvertTypeToAny           | Convert to generic type for bridging |
| ✗       | GetValueFromJsonObj        | Get value by key from JSON object |
| ✗       | FilterValueForList         | Filter list by value |
| ✗       | SliceList                  | Slice list |
| ✗       | LoadLocalFilePath          | List files in given path |
| ✗       | LoadImageFromLocalPath     | Load image by full path |
| ✗       | LoadMaskFromLocalPath      | Load mask by full path |
| ✗       | IsNoneOrEmpty              | Check if value is None/empty/empty list or dict |
| ✗       | IsNoneOrEmptyOptional      | Return fallback if value is None/empty |
| ✔       | EmptyOutputNode            | Empty output node |
| ✗       | SaveTextToFileByImagePath  | Save text alongside image using image name |
| ✗       | CopyAndRenameFiles         | Copy & rename files to another folder |
| ✗       | SaveImagesWithoutOutput    | Save image without being output node (used in loops) |
| ✗       | SaveSingleImageWithoutOutput | Same as above but for a single image |
| ✗       | CropTargetSizeImageByBbox  | Crop fixed size centered on BBox |
| ✗       | ConvertToJsonStr           | Serialize to JSON string |
| ✗       | SaveTextToLocalFile        | Save text to file |
| ✗       | ReadTextFromLocalFile      | Read text from file |
| ✗       | TryFreeMemory              | Free RAM/GPU memory |
| ✗       | IfElseForEmptyObject       | If/Else logic for lists |
| ✗       | ImageSizeGetter            | Get image dimensions (width, height, min/max, batch size) |
| ✗       | FilterSortDependSubGraphs  | Run only specified dependent subgraphs in order |
| ✗       | SortDependSubGraphs        | Run all subgraphs, prioritizing selected ones |
| ✗       | NoneNode                   | Return None |
| ✗       | NodeListToList             | Convert node list input to normal list |


### Examples
![save api extended](docs/example_note.png)

### [Workflows](example)
![workflow 1](example/example.png)
![workflow 2](example/example_1.png)
![workflow 3](example/example_2.png)
![workflow 4](example/example_3.png)
![workflow 5](example/example_4.png)
![SAM mask example](example/example_sam_mask.png)
![Batch crop tagging](example/example_image_crop_tag.png)

## Changelog

### 2025-06-30 (v1.1.7)
- New node: NodeListToList

### 2025-05-15 (v1.1.5)
- Fix: When `FilterSortDependSubGraphs` and `SortDependSubGraphs` fail, re-submitting the job would skip those dependencies — now fixed.

### 2025-05-12 (v1.1.4)
- New node: NoneNode

### 2025-03-28 (v1.1.3)
- New setting: `allow_create_dir_when_save` — controls whether to auto-create folders when saving text/images
- New nodes: ImageSizeGetter, FilterSortDependSubGraphs, SortDependSubGraphs
![subgraph execution order](docs/sort_subgraphs.gif)
![filtered subgraph execution](docs/filter_sort_subgraphs.gif)

### 2025-02-19 (v1.1.1)
- New node: IsNoneOrEmptyOptional

### 2024-12-01 (v1.1.0)
- New nodes: SaveTextToLocalFile, ReadTextFromLocalFile

### 2024-11-04 (v1.0.9)
- New nodes: SamAutoMaskSEGSAdvanced, MaskToRle, RleToMask, ConvertToJsonStr

### 2024-10-24 (v1.0.7)
- New nodes: SaveTextToFileByImagePath, CopyAndRenameFiles, SaveImagesWithoutOutput, SaveSingleImageWithoutOutput, CropTargetSizeImageByBbox

### 2024-10-18
- New nodes: SliceList, LoadLocalFilePath, LoadImageFromLocalPath, LoadMaskFromLocalPath, IsNoneOrEmpty, IsNoneOrEmptyOptional, EmptyOutputNode

### 2024-09-29
- New node: FilterValueForList

### 2024-09-26
- New nodes: GetValueFromJsonObj, LoadJsonStrToList, ConvertTypeToAny

### 2024-09-25 [example](example/example_4.png)
- New nodes: ForEachOpen, ForEachClose

### 2024-09-20 [example](example/example_4.png)
- New nodes: SplitStringToList, IndexOfList, IndexesOfList, StringArea

### 2024-09-19
- Added ListUnWrapper node

### 2024-09-04
- Added BBox-related nodes

### 2024-08-08
- Menu UI adapted to new ComfyUI frontend
![new menu](docs/menu_new_ui.gif)

## Features

- **Extended "Save (API Format)" menu:**
  - Copy workflow
  - Save/Copy in API format (enable via Settings → Enable Dev Mode Options)
    - `Save as / Copy API`: Save or copy workflow in API format
    - `Copy EasyAi as / Copy EasyAi`: Same as above, but replaces `LoadImage` with `Base64ToImage`, and `PreviewImage`/`SaveImage` with `ImageToBase64`

![menu api format](docs/menu.gif)

- **Settings Enhancements:**
![settings ui](docs/settings.png)

  - **Maximum History Size**
    - Path: Settings → [EasyApi] Maximum History Size
    - Tip: When using base64, images are stored in memory. Default max history = 10000. This setting helps prevent memory overflow.

  - **Auto Expand Submenus**
    - Path: Settings → [EasyApi] Auto Open Sub Menu
![auto submenu](docs/menu_autoopen.gif)

  - **Fuzzy Search**
    - Path: Settings → [EasyApi] Fuzzy Search
![fuzzy search](docs/fuzzy_search.png)

  - **Mirror URLs for auto-downloading models**
    - HuggingFace Mirror
    - RawGithub Mirror
    - Github Mirror
![mirror settings](docs/settings_1.png)

- **Context Menu Extensions**
  - Set custom ID for selected node  
![set id](docs/node_context_menu_set_id.png)

  - Reset all node IDs starting from 1  
![reset all ids](docs/context_menu_reset_all_id.png)

  - Jump to connected nodes  
![link node navigation](docs/node_context_menu_link_node.png)
