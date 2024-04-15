
# Title: A Learning Framework for Deformable Medical Image Registration  
##  Data set
 Fundus Image Registration dataset (FIRE) : The dataset consists of 129 retinal images forming 134 image pairs. These image pairs are split into 3 different categories depending on their characteristics. The images were acquired with a Nidek AFC-210 fundus camera, which acquires images with a resolution of 2912x2912 pixels and a FOV of 45° both in the x and y dimensions. Images were acquired at the Papageorgiou Hospital, Aristotle University of Thessaloniki, Thessaloniki from 39 patients.
 FIRE is used as data set in my project . It consists of Fixed Image and Moving Image . We have taken  89 pairs as my train dataset and 45 image pairs as my validation dataset. 
 you download the data set from following link :
 https://projects.ics.forth.gr/cvrl/fire/FIRE.7z
## Voxel Morph
The VoxelMorph class defines a neural network model for image registration tasks. It consists of a U-Net architecture followed by a spatial transformation module. The U-Net takes concatenated input images (moving and fixed) and predicts a deformation matrix representing the spatial transformation required to align them. The deformation matrix is then used by the spatial transformation module to register the moving image to the fixed image. Finally, the registered image and deformation matrix are returned as outputs. This architecture enables end-to-end learning of image registration, allowing the model to automatically align images without the need for explicit feature extraction or predefined transformation models.
## Unet architecture
Contracting Blocks: These blocks perform feature extraction and downsampling, gradually reducing spatial dimensions while increasing the depth of feature maps.

Bottleneck: The bottleneck module captures high-level features and serves as a bridge between the contracting and expansive stages, enabling the model to learn spatial transformations effectively.

Expansive Blocks: These blocks perform feature upsampling and decoding, allowing the model to recover spatial information lost during contraction. They incorporate skip connections to preserve fine-grained details.

Final Layer: The final block performs convolutional operations to generate the deformation matrix, which represents the spatial transformation required to align the moving image with the fixed reference image.

The U-Net architecture facilitates end-to-end learning of image registration, enabling the model to automatically learn complex spatial transformations from input image pairs. By leveraging skip connections and transposed convolutions, the model can effectively capture both local and global features, enhancing registration accuracy.

This implementation follows best practices in deep learning, including batch normalization and ReLU activation functions, promoting stable training and improved convergence. Additionally, the modular design allows for easy customization and adaptation to different registration tasks and datasets.
## Spatial Transformer Function
The SpatialTransformation class implements spatial transformation operations necessary for image registration tasks, including meshgrid generation, repeat operations, and interpolation.

Meshgrid Generation: The meshgrid method generates a meshgrid of coordinates for the given height and width.

Repeat Operation: The repeat method repeats tensor elements along specified dimensions.

Interpolation: The interpolate method performs bilinear interpolation to warp the input moving image according to the provided deformation matrix, adjusting pixel intensities based on transformed coordinates.

Forward Pass: In the forward method, the deformation matrix is extracted into displacement components (dx and dy), and the meshgrid is generated. The displacement components are added to the meshgrid to obtain new coordinates. The moving image is then interpolated using these transformed coordinates, producing the registered image.

This class enables the spatial transformation of images based on learned deformation matrices, facilitating image registration by aligning moving images with fixed reference images. The interpolation technique preserves image details during transformation, ensuring accurate registration results.
## Loss Function
Cross-correlation Loss: This function measures the similarity between two images, I and J, based on their cross-correlation. It computes the mean squared error between local image patches and is commonly used as a similarity metric during optimization. This loss is essential for aligning images accurately during the registration process.

Smoothing Loss: This loss promotes smoothness in the predicted deformation field (y_pred). It calculates the gradient of the deformation field along the x and y directions and computes the mean squared difference between neighboring pixel values. This encourages the deformation field to be smooth and continuous, preventing unrealistic deformations in the registered images.

These loss functions play a crucial role in training image registration models. The cross-correlation loss guides the model to minimize the discrepancy between the moving and fixed images, ensuring accurate alignment. Meanwhile, the smoothing loss encourages spatially consistent deformation fields, leading to visually appealing and physically plausible registrations
## Hyper parameters
Learning rate: 1e-4
Batch size: 1
Optimizer: Adam
Loss function: Unsupervised Loss Function
𝜆:regularization parameter - 0.01
## YOU TUBE LINk :
https://youtu.be/_aTDC-uqXLk
