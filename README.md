# Content-Based-Image-Retrieval
Features are extracted from the images of the MedNIST data-set using Histogram of Oriented Gradients, which are further used to create a Vantage-Point Tree, in order to easily perform Approximate Nearest Neighbor search with query images.

The MedNist dataset consists of 58954 images of 6 medical image modalities, namely, 'AbdomenCT', 'BreastMRI', 'CXR', 'ChestCT', 'Hand', 'HeadCT'. Each image is 64*64 in resoultion. The data-set was created by combining scaled down images from various other publically available datasets (TCIA, NIH-Chest XRay, the RSNA Bone AGe Challenge). It is a good dataset for benchmarking and simple hypothesis testing. It is mainly used for classification task.

NOTE : Instead of a HOG feature extractor, a neural network could have been deployed for creating the embeddings, however, was deemed easily prone to overfitting due to the small number of features.

An accuracy of 99.83 % (top 1) and 100  % (top 5),while testing on an unseen subset of the dataset (comprsing 589 images) was achieved. The methodology of classification used was Nearest Neighbor.

The VP-tree implementation was inspired by https://github.com/RickardSjogren/vptree. A more efficient modified implemntation of the same, which uses min heap priority queue for maintaining neighbors and a linkedlist for nodes_to_visit, has been added as "VP-efficient.py".

This methodolgy has the advantage of being invariant to imbalences in the dataset, and is much faster to create and query than neural network, along with final results being impressive.

While the HOG embeddings were each comprising a vector of 441*1, another approach has been added, which uses difference-hashing, to generate just 1 binary representation per image. The accuracy for this method was 95.08% (top 1) and 99.32% (top 5) (there were 29 missclassified examples, but, for 25 of them, top 5 predictions yielded correct results).
