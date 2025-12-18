

# Part 2 — Reasoning-Based Answers

## **Q1: Choosing the Right Approach**

For detecting whether a product is missing a label, I would start with **object detection** instead of classification or segmentation. Detection allows the model to localize the label on the product and verify whether it is present in the correct region, whereas classification would only tell us if a label exists somewhere without spatial context. Segmentation could work, but it is more computationally expensive and requires pixel-level annotation, which may not provide significant extra value for this task. If object detection fails due to subtle label differences or low contrast, my fallback would be a two-stage system: first detect the product, then run fine-grained classification or OCR on the detected label area to confirm presence and correctness.

---

## **Q2: Debugging a Poorly Performing Model**

If my model performs poorly on new factory images, I would first check for **domain shift** by comparing sample training and test images visually. Then, I would examine label quality — ensuring annotation consistency, bounding box correctness, and checking for missing labels. I would perform a small ablation: train with and without augmentations to see if augmentation is causing harm. Finally, I would test generalization by running inference step-by-step on new images, inspecting confidence scores, feature maps, and evaluating whether failures are due to lighting, angle, or unseen product variations.

---

## **Q3: Accuracy vs Real Risk**

Accuracy is not the right metric here, because it hides class imbalance and safety risk. Missing 1 out of 10 defective products is unacceptable in a manufacturing environment, even if accuracy looks high. Instead, I would prioritize **recall**, **precision**, and particularly **false-negative rate**, because missing a defective item is more costly than flagging a false alarm. For decision-making, I would also evaluate metrics like F1-score and confusion matrix to better understand model trade-offs, and potentially adjust confidence thresholds to minimize critical misses.

---

## **Q4: Annotation Edge Cases**

Blurry or partially visible objects should be included selectively, depending on deployment conditions. If real-world factory cameras frequently produce blurry or occluded frames, including these examples improves robustness and prevents the model from failing in production. However, if the edge cases are unrealistic or severely degraded, they may add noise and confuse the model. The trade-off is between dataset cleanliness (better convergence) and real-world generalization (better resilience), so a balanced approach is labeling realistic edge cases while excluding unusable ones.

---

# End of Part 2

---

