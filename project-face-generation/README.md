In this project I trained a DC-GAN to generate realistic celebrity faces based on the CelebA dataset.
It was implemented with a deep convolutional generator and discriminator network using batch normalization everywhere except in the layers connecting the two networks, discriminator dropout, one sided label smoothing, and latent vectors sampled from a Normal distribution.
