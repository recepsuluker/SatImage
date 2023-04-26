import os
import cv2
import rasterio

def split_image_into_tiles(input_image, output_folder, tile_size):
    with rasterio.open(input_image) as src:
        width, height = src.width, src.height
        transform = src.transform

        for i in range(0, width, tile_size):
            for j in range(0, height, tile_size):
                tile_transform = rasterio.windows.transform(
                    rasterio.windows.Window(i, j, tile_size, tile_size),
                    transform
                )
                tile = src.read(window=rasterio.windows.Window(i, j, tile_size, tile_size), out_shape=(1, tile_size, tile_size), resampling=rasterio.enums.Resampling.bilinear)

                output_path = os.path.join(output_folder, f'tile_{i}_{j}.tif')
                cv2.imwrite(output_path, tile[0])

if __name__ == '__main__':
    input_image = 'path/to/sentinel_image.jp2'
    output_folder = 'path/to/output/folder'
    tile_size = 512

    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    split_image_into_tiles(input_image, output_folder, tile_size)

