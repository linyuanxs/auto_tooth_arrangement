# Auto_tooth_arrangement
Automatically arrange teeth using neural networks. Applied to automatic orthodontic treatment of oral teeth.
# Reference:
1.TANet: Towards Fully Automatic Tooth Arrangement.
2.Tooth_Alignment_Network_Based_on_Landmark_Constraints_and_Hierarchical_Graph_Structure.
3.ViT：An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale.
# model structure
![auto teeth_model](https://github.com/huang229/auto_tooth_arrangement/assets/29627190/c57cab48-185c-4edf-a75c-a4f674e07504)
1. The reason for this design：
   a. Tooth arrangement includes two operations: translation and rotation.
   b. The model should have modules that care about rotation and translation separately.
   c.If you only care about rotation, then you should not be affected by position. So we should decentralize every tooth.
   d.If we only care about translation, then we should not be affected by tooth posture. The center point of the tooth is undoubtedly the characteristic that best reflects the position of the tooth.
   e.Embed tooth position information to better reflect the relative position relationship of each tooth. When you only train the tooth translation, the value of the embedded position information Loss function decreases less.
   f.Residual module, you don't know the global information required for each tooth, so set a learnable parameter weight for each tooth.
   g. Pay attention to the direction of the teeth, so the input should not be a feature unrelated to the tooth posture. Therefore, a transformer model is used here, which can extract the global features of each tooth.
   h.The first transformer module calculates the relationship between teeth in feature extraction of tooth center points, as the continuity of teeth on the dental arch is essentially the relative pose relationship between teeth. You can also use a fully connected layer instead, as the third transformer module also calculates the correlation between teeth.

