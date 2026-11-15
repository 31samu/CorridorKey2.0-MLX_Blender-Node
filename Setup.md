# Setup

Install the extension ZIP via **Preferences → Get Extensions → Install from Disk**.
In **Preferences → Add-ons**, expand **CorridorKey MLX Node** and click **Set Up CorridorKey**. To install both profiles in one pass, check **Also download the 1536 × 1024 model** before clicking **Download and Install**. Automatic setup requires Apple Silicon, macOS 26 or later, and Blender's **Allow Online Access** setting. A fresh install downloads about 2.8 GB for the runtime and 720p model, or about 4.1 GB with both models. Setup stores the runtime and models in Blender's per-extension user folder. Subsequent analysis runs locally.

If you already have a working backend, use the executable and model folder fields under **Advanced**. Clear both fields to use automatic setup. The **Cache folder** override is also under **Advanced**. Unsaved projects use the extension's local analysis cache.

## Use the node

1. In the scene compositor or a Sequencer strip's Compositor modifier, choose **Add → Keying → CorridorKey2.0 (MLX)** and connect its **Image** input. The editable **Start Frame** and **End Frame** fields fill from the strip's visible range or the linked Image node's media. For other graphs, they use the scene range. The bake fits the source into the selected model's frame without stretching it.
2. Before analysis, the **Image** output previews the source. The **Alpha Hint** under **More** adds a translucent white overlay. The **Garbage Mask** darkens excluded areas, including where the two masks overlap.
3. Click **Analyze**. The node shows frame counts as it bakes, analyzes, and keys. Connect its **Image** output to the **Foreground** input of an **Alpha Over** node, or to **Group Output → Image** to replace a Sequencer strip's image.
4. Click **Clear Bake** to return to the source preview before analyzing again. The cached files stay on disk by default. Enable **Delete Cache Files on Clear Bake** under **Advanced** in the add-on preferences to remove them as well. Undo can't recover deleted files, and other saved blend files may still need them. If a job fails, look for `analysis.log` in the job folder within the cache directory. The default cache is `corridorkey-cache` next to the saved blend file.

## Model resolutions

The installed 720p FP16 profile has a padded height × width of 768 × 1280. Model graphs use fixed tensor shapes. Image input can bake larger or smaller sources at the selected working resolution.

For the extension's **1536 × 1024** setting, click **Download 1536 × 1024 Model** in the add-on preferences. It adds the profile to your active model folder and reuses weights that match files in the installed 720p profile. A complete 720p install reduces the additional download to about 1.33 GB. 

Native 1920 × 1080 needs a 1152 × 1920 graph. Native 3840 × 2160 needs a 2176 × 3840 graph. Those profiles would need to be converted and validated for the MLX runtime, or supplied by the model maintainer. Then the extension would need to expose them.

The node reads the analysis cache during playback and render. Keep the cache with the project. The cache uses a new folder for each analysis, so you can remove earlier folders once any blend files that reference them have been retired.

![extension settings pane](images/settings.webp)
![dowload dialog](images/download.webp)
