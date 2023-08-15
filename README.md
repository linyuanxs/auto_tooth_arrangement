# Auto_tooth_arrangement(code: Model 1 application)
1.Automatically arrange teeth using neural networks. Applied to automatic orthodontic treatment of oral teeth.

2.This is only an automatic arrangement of single jaw teeth (considering certain factors). It is easy to expand to full mouth teeth.
3.This code is only for Model 1 and does not consider missing teeth.
# Reference:
1. TANet: Towards Fully Automatic Tooth Arrangement.
2. Tooth_Alignment_Network_Based_on_Landmark_Constraints_and_Hierarchical_Graph_Structure.
3. ViT：An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale.
4. https://github.com/ziyangyeh/TANet-Pytorch
# model .pth
链接：https://pan.baidu.com/s/1nsectXx46bpWMqeVSbYnTQ 
提取码：0chs    
The reason why the model file is so large is because I did not delete some useless parameters.
# model structure
![auto teeth_model](https://github.com/huang229/auto_tooth_arrangement/assets/29627190/7999d5ae-ceb8-43ff-a593-4f3e00023315)
![loss](https://github.com/huang229/auto_tooth_arrangement/assets/29627190/236e02c0-e7a6-4541-b6d1-c6dff3798b93)

# The reason for this design：
1. Tooth arrangement includes two operations: translation and rotation.
2. The model should have modules that care about rotation and translation separately.
3. If you only care about rotation, then you should not be affected by position. So we should decentralize every tooth.
4. If we only care about translation, then we should not be affected by tooth posture. The center point of the tooth is undoubtedly the characteristic that best reflects the position of the tooth.
5. Embed tooth position information to better reflect the relative position relationship of each tooth. When you only train the tooth translation, the value of the embedded position information Loss function decreases less.
6. Residual module, you don't know the global information required for each tooth, so set a learnable parameter weight for each tooth.
7. Pay attention to the direction of the teeth, so the input should not be a feature unrelated to the tooth posture. Therefore, a transformer model is used here, which can extract the global features of each tooth.
8. The first transformer module calculates the relationship between teeth in feature extraction of tooth center points, as the continuity of teeth on the dental arch is essentially the relative pose relationship between teeth. You can also use a fully connected layer instead, as the third transformer module also calculates the correlation between teeth.
9. The fusion of center point features and tooth features is because tooth arrangement is a relative pose relationship of teeth on the dental arch. For example, even if the position is correct but the posture is not good, serious collisions may still occur, and poor posture can also affect bite, and so on.
10. Finally, separate the prediction of tooth translation and rotation, and consider that translation and rotation are two different tasks.
# Environment
1.python 3.7.0

2.pytorch 11.3.1

3.pytorch3D 0.7.4
# Train
python main.py
# test
python test_rotate.py
# Difficult issues:
1.Orthodontics: The collision between teeth is undoubtedly a crucial point, and what constraints should be established to 100% avoid tooth collisions in the dental alignment results. The occlusion and coverage between teeth are all worth in-depth consideration.

2.I hope to have like-minded friends to discuss together. Leave QQ for easy communication.


# Appendix
1.When doctors perform dental correction on patients, not all teeth will change, but only a few teeth or some of their positions will change. For example, if the patient only has a deformed position of the incisors, they may only move and rotate the incisors, or move and rotate them together with the lateral incisors and canines near the incisors. The posterior premolars and molars may remain unchanged during orthodontic treatment, so the design of Model 1 is unreasonable. Doctors often refer to the position of dental arches and teeth without deformities when performing orthodontic treatment on patients. Therefore, it can be understood as only adjusting the relative posture of some deformed teeth based on referencing the correct tooth posture, or it may be a back and forth dynamic adjustment process (for deformed teeth and adjacent teeth).
医生对患者进行牙齿矫正，并不是所有的牙齿都会变化，只是少数的几颗牙齿或者部分牙齿的位姿发生变化。比如患者只有切牙的位姿畸形，那么可能只移动和旋转切牙，或者连同切牙附近的侧切牙和尖牙一起移动和旋转，后面的前磨牙和磨牙在正畸治疗过程中可能是毫无变化的，因此模型1设计不合理。医生对患者进行牙齿正畸治疗，往往参考了牙弓和没有畸形的牙齿的位姿等等。因此可以理解为在参考正确的牙齿位姿的基础上仅对部分畸形牙齿做相对位姿调整，也可能是来回动态调整过程（那畸形牙及邻牙）。

model structure:
![model 2](https://github.com/huang229/auto_tooth_arrangement/assets/29627190/e7ff546c-5a15-4dd7-8b68-8accd05d7d0b)
![model 3](https://github.com/huang229/auto_tooth_arrangement/assets/29627190/b9245f5b-984a-4ba0-a745-73fd09fbb5e3)


# License and Citation
1.Without permission, the design concept of this model shall not be used for commercial purposes, profit seeking, etc.

2.If you refer to the design concept of this model for theoretical research and publication of papers on automatic tooth arrangement, please also add a reference.
