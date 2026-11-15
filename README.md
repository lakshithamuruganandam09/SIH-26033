# Smart India Hackathon Workshop
# Date:15/10/2026
## Reference Number:26018363
## Name:Lakshitha M

## Problem Title
SIH 26033: Multiple intermediaries reduce farmers earnings and increase consumer prices.

## Problem Creater's Organization
Ministry of Consumer Affairs, Food & Public Distribution

## Theme
Agriculture, FoodTech & Rural Development

## Problem Description
Expected Solution: Create a digital marketplace that:

• Connects farmers/FPOs directly with consumers and bulk buyers.
• Provides logistics support.
• Uses AI for demand forecasting and route optimization.

Benefits:

• Better prices for farmers.
• Lower prices for consumers.
• Reduced supply chain inefficiencies.

## Proposed Solution
Buyers who purchase directly from farmers often cannot judge produce quality without seeing it, so they either pay a safety margin or go back to middlemen who take a cut. Farmers, in turn, cannot prove that their produce is good, so they accept lower prices.

Our solution lets a farmer photograph produce with a phone, and an AI model suggests a quality grade (A, B or C). The grade appears on the listing with a matching price range, so buyers can trust the quality without visiting the farm.

The system has four parts:
1. *Photo capture:* the farmer takes photos of a produce batch on a plain background, following on-screen guidance (good light, whole produce in frame, a coin or ruler for scale).
2. *AI grading:* a model classifies the photo into grade A, B or C, and flags visible defects such as bruises, spots, or cracks.
3. *Grade-based listing:* the listing shows the grade, a short defect note, and a price range linked to the current mandi rate for that grade.
4. *Farmer confirmation:* the farmer can accept or override the suggested grade, and the final grade is recorded with the photo. Buyers can report a mismatch after delivery, which lowers that farmer's trust score.

*How it addresses the problem:*
- Buyers can trust the quality without visiting the farm, so they stop paying a safety margin.
- Farmers get paid for the grade they actually produce, instead of the lowest-grade price.
- Grade-based pricing makes the market fairer for both sides.

*Innovation:* most direct-selling apps rely on seller descriptions. This solution adds an independent visual check on each batch, and links the grade to a price range, so the quality claim can be verified by the buyer and by the platform's records.

## Technical Approach
- *Backend:* Python, Django, Django REST Framework
- *Frontend:* HTML, CSS, Bootstrap, JavaScript (camera capture in the browser)
- *Image processing:* OpenCV (resizing, background removal, colour and spot detection)
- *AI model:* TensorFlow/Keras with a pre-trained MobileNetV2 model, fine-tuned on labelled produce photos
- *Database:* SQLite for the prototype, PostgreSQL for deployment
- *Hardware:* a smartphone camera (no extra hardware for the prototype)

### Methodology and process for implementation

mermaid
flowchart LR
    A[Farmer takes photo] --> B[Image preprocessing]
    B --> C[AI grading model]
    C --> D{Confidence high?}
    D -- Yes --> E[Suggested grade A / B / C]
    D -- No --> F[Ask for a clearer photo]
    F --> A
    E --> G[Farmer confirms or overrides]
    G --> H[Listing with grade and price range]
    H --> I[Buyer orders]
    I --> J[Delivery and feedback]


*Implementation steps:*
1. *Dataset:* collect photos of one or two produce types (for example, tomatoes and onions), each labelled by a trained grader using the AGMARK grade standard for that crop.
2. *Preprocessing:* resize images, normalize brightness, and crop to the produce using OpenCV.
3. *Model training:* fine-tune MobileNetV2 on the labelled photos, and check accuracy on a separate test set.
4. *Defect detection:* use simple colour and spot analysis in OpenCV to list visible defects.
5. *Platform integration:* add the photo upload and grade display to the farmer and buyer pages in Django.
6. *Testing:* test with unseen photos, check the confidence threshold, and run a pilot with one FPO.
## Feasibility and Viability
- The model is a standard image classifier, and the tools are free and open source.
- A prototype needs a labelled dataset, which can be built with a few hundred photos per grade and a grader's help.
- Phone cameras are good enough for grading, so no special hardware is needed.

*Potential challenges and risks:*
- Photos taken in poor light or on cluttered backgrounds may give wrong grades.
- Grades can differ between graders, so the model may learn the wrong standard.
- Farmers may photograph their best produce and sell the rest as the same grade.
- The dataset may be too small to cover every variety and season.

*Strategies for overcoming these challenges:*
- Guide the farmer during capture, and reject photos that are too dark or blurred.
- Check the model against a senior grader's labels before using it in listings.
- Require a random sample from each batch, and let buyers report mismatches, which affects the farmer's trust score.
- Start with two crops, then add more as the dataset grows.
- Let the farmer override the grade, but keep the override and the buyer feedback in the record.

## Impact and Benefits
*Potential impact on the target audience:*
- *Farmers and FPOs:* paid for the grade they grow, with less loss from low-grade pricing.
- *Consumers and bulk buyers:* clear quality information before buying, and fewer surprises on delivery.

*Benefits of the solution:*
- *Social:* fairer income for small farmers, and better-quality food for consumers.
- *Economic:* less money lost to safety margins and quality disputes, and clearer pricing for every grade.
- *Environmental:* fewer rejected deliveries and less food wasted on quality disputes.

## Research and References
- AGMARK grade standards, Directorate of Marketing & Inspection: https://dmi.gov.in
- Agmarknet, government mandi price data: https://agmarknet.gov.in
- MobileNetV2 model, TensorFlow/Keras documentation: https://www.tensorflow.org/api_docs/python/tf/keras/applications/MobileNetV2
- OpenCV, image processing library: https://opencv.org
