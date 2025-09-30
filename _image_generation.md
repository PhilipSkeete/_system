# Venice Image Generation Assistant Guide

This document outlines how to use the Venice Image module to generate and edit images by embedding a detail block in your responses.

## Image Operation Workflow
1.  **Act:** Emit the image operation after your conversational response.
2.  **Format:** Emit one HTML `<details>` block for the image operation. The `<summary>` MUST start with "Image:" and specify the operation.

## Generating New Images
<details>
   <summary>Image: New</summary>
   action: generate
   prompt: A futuristic cityscape at sunset, with flying cars and neon signs.
   style_preset: Cinematic
   variants: 2
   image_size: 1280x720
</details>

### Parameters:
-   `action` (str, required): Must be `generate`.
-   `prompt` (str, required): A description of the image to generate. (1-1500 characters).
-   `model` (str, optional): Image generation model, web_fetch list here https://api.venice.ai/api/v1/models?type=image
-   `style_preset` (str, optional): Image style preset, web_fetch list here https://api.venice.ai/api/v1/image/styles
-   `negative_prompt` (str, optional): A description of what to avoid in the image. (Max 1500 characters).
-   `variants` (int, optional): The number of images to generate. (Range: 1-4). Defaults to 1.
-   `image_size` (str, optional): The dimensions of the image (e.g., `1024x1024`). Max width/height is 1280. Defaults to `auto`.
-   `cfg_scale` (float, optional): Prompt adherence. (Range: 0-20). Defaults to 7.5.
-   `steps` (int, optional): Number of generation steps. (Range: 1-50, model dependent). Defaults to 30.
-   `seed` (int, optional): A seed for deterministic generation. (Range: -999999999 to 999999999).

**Reminder:** At the start of each new image generation session, web_fetch the current models and styles lists from the URLs provided above.

## Editing Existing Images
<details>
   <summary>Image: Edit</summary>
   action: edit
   prompt: Make the sky look like a vibrant sunset.
   source_image_url: https://im.di.st/123xyz.webp
</details>

### Parameters:
-   `action` (str, required): Must be `edit`.
-   `prompt` (str, required): Instructions for how to edit the image (e.g., "Change the background to a forest"). (Max 1500 characters).
-   `source_image_url` (str, required): The URL of the image to edit.

## Upscaling Images
<details>
   <summary>Image: Edit</summary>
   action: upscale
   prompt: Upscale this image 4x and enhance the details.
   replication: 0.5
   source_image_url: https://im.di.st/456abc.webp
</details>

### Parameters:
-   `action` (str, required): Must be `upscale`.
-   `source_image_url` (str, required): The URL of the image to upscale.
-   `prompt` (str, optional): A prompt to guide the upscaling process. Can include `2x` or `4x` to specify the factor.
-   `enhance` (bool, optional): Whether to enhance the image during upscaling. Defaults to `false`.
-   `enhance_prompt` (str, optional): A prompt for the enhancement process. (Max 1500 characters).
-   `replication` (float, optional): How strongly lines and noise are preserved. (Range: 0-1). Defaults to 0.35.
-   `scale` (int, optional): The upscale factor. (Range: 1-4). Defaults to 2.

### Notes - Model-Specific Tips:
wai-Illustrious: This model is already optimized for anime generation. Skip the style_preset parameter to avoid over-stylization - the model's inherent training produces cleaner, more natural anime results without additional style layering.