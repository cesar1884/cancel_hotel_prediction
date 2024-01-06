# Hotel Booking Cancelation Prediction

## Problem Statement

The hospitality industry has undergone a significant transformation in recent years, with a shift in booking methods predominantly towards Online Travel Agencies (OTAs) like Booking.com. These platforms have revolutionized the way cancellation policies are presented and marketed, making free cancellation options a major highlight. This shift has led to an increasing trend of booking cancellations, posing a substantial challenge for the hotel industry.

Beyond the direct monetary impact, cancellations also disrupt operational efficiency, leading to issues like overstaffing or understaffing. These operational hiccups can degrade customer satisfaction and spawn adverse online reviews. In today's digital age, where online reviews significantly influence customer decisions, maintaining a positive online reputation is crucial. Studies have shown that a boost in a hotel's online reputation correlates directly with increased occupancy and revenue.

To mitigate these challenges, it's essential for hotels to predict the likelihood of cancellations. This insight enables better operational planning and prioritization of bookings, ultimately enhancing customer satisfaction and financial outcomes.

Our approach to addressing this issue involves leveraging a real-life hotel booking dataset. We aim to develop a classification model to predict booking cancellations with high accuracy.

By accurately forecasting cancellations, hotels can optimize their operations, improve customer experiences, and bolster their revenue stream, turning a challenge into an opportunity for growth and improvement.


# Model Validation

## Task Overview
In this project, we address a binary classification problem, where the primary objective is to predict whether a hotel booking will be canceled. Accurate predictions are crucial in helping hotels manage their reservations more effectively and maintain high customer satisfaction.

## Key Metrics
Given the nature of our task, two metrics are particularly important in evaluating the performance of our model:

1. **Accuracy**: This metric measures the proportion of total correct predictions (both true positives and true negatives) over all predictions. A high accuracy indicates that the model is effective in identifying both cancellations and non-cancellations.

2. **Recall (Sensitivity)**: Recall is critical in this context because it measures the model's ability to correctly identify actual cancellations. We do not want our model to predict with a really high precision a booking that will be cancelled but neglecting the recall for the booking that will not be cancelled.

## Importance of Minimizing False Positives
While focusing on recall, it's also essential to consider the implications of false positives - cases where the model incorrectly predicts a cancellation when the customer does not intend to cancel. In the hotel industry, such false predictions could lead to over-cautious room allocations, potentially causing a decline in occupancy rates and, consequently, revenue. More importantly, it may result in a scenario where genuine bookings are declined due to anticipated cancellations, adversely affecting the hotel's reputation and customer relations.

# Data Explanation

| Feature Name                 | Type         | Description |
|------------------------------|--------------|-------------|
| ADR                          | Float        | Average Daily Rate. Calculated by dividing the sum of all lodging transactions by the total number of staying nights. |
| Adults                       | Integer      | Number of adults. |
| Agent                        | Categorical  | ID of the travel agency that made the booking. |
| ArrivalDateDayOfMonth        | Integer      | Day of the month of the arrival date. |
| ArrivalDateMonth             | Categorical  | Month of arrival date with 12 categories: “January” to “December”. |
| ArrivalDateWeekNumber        | Integer      | Week number of the arrival date. |
| ArrivalDateYear              | Integer      | Year of arrival date. |
| AssignedRoomType             | Categorical  | Code for the type of room assigned to the booking. Sometimes the assigned room type differs from the reserved room type due to hotel operation reasons (e.g., overbooking) or by customer request. Code is presented instead of designation for anonymity reasons. |
| Babies                       | Integer      | Number of babies. |
| BookingChanges               | Integer      | Number of changes/amendments made to the booking from the moment the booking was entered on the Property Management System until the moment of check-in or cancellation. |
| Children                     | Integer      | Number of children. Sum of both payable and non-payable children. |
| Company                      | Categorical  | ID of the company/entity that made the booking or responsible for paying the booking. ID is presented instead of designation for anonymity reasons. |
| Country                      | Categorical  | Country of origin. Categories are represented in the ISO 3155–3:2013 format. |
| CustomerType                 | Categorical  | Type of booking, assuming one of four categories: Contract, Group, Transient, and Transient-party. |
| DaysInWaitingList            | Integer      | Number of days the booking was in the waiting list before it was confirmed to the customer. |
| DepositType                  | Categorical  | Indication on if the customer made a deposit to guarantee the booking. This variable can assume three categories: No Deposit, Non Refund, and Refundable. |
| DistributionChannel          | Categorical  | Booking distribution channel. The term “TA” means “Travel Agents” and “TO” means “Tour Operators”. |
| IsCanceled                   | Integer      | Value indicating if the booking was canceled (1) or not (0). |
| IsRepeatedGuest              | Integer      | Value indicating if the booking name was from a repeated guest (1) or not (0). |
| LeadTime                     | Integer      | Number of days that elapsed between the entering date of the booking into the Property Management System and the arrival date. |
| MarketSegment                | Categorical  | Market segment designation. In categories, the term “TA” means “Travel Agents” and “TO” means “Tour Operators”. |
| Meals                        | Categorical  | Type of meal booked. Categories include: Undefined/SC (no meal package), BB (Bed & Breakfast), HB (Half board), and FB (Full board). |
| PreviousBookingsNotCanceled  | Integer      | Number of previous bookings not canceled by the customer prior to the current booking. |
| PreviousCancellations        | Integer      | Number of previous bookings that were canceled by the customer prior to the current booking. |
| RequiredCarParkingSpaces     | Integer      | Number of car parking spaces required by the customer. |
| ReservationStatus            | Categorical  | Reservation last status, assuming one of three categories: Canceled, Check-Out, No-Show. |
| ReservationStatusDate        | Date         | Date at which the last status was set. |
| ReservedRoomType             | Categorical  | Code of room type reserved. Code is presented instead of designation for anonymity reasons. |
| StaysInWeekendNights         | Integer      | Number of weekend nights (Saturday or Sunday) the guest stayed or booked to stay at the hotel. |
| StaysInWeekNights            | Integer      | Number of week nights (Monday to Friday) the guest stayed or booked to stay at the hotel. |
| TotalOfSpecialRequests       | Integer      | Number of special requests made by the customer (e.g., twin bed or high floor). |


# Journey through the Project

## 1. Exploratory Data Analysis (EDA)
## 2. Data Cleaning
## 3. Feature Engineering
## 4. Modeling



# Results and explanation

## 1. Exploratory Data Analysis (EDA)

The dataset does not contain the same number of labels for each class but the dataset is not clearly inbalanced. we have enough data from both classes to train our model correctly.

Some Feature are highly correalted with the target variable as the lead time and the deposit type

![image](https://github.com/cesar1884/cancel_hotel_prediction/assets/94693373/ed7df8b9-fc80-4a3b-b65a-b967a8d9f5f8)


Some feature as those relating to the date are not correlated and has not a lot of sense in our analysis. We removed them.

## 2. Data Cleaning
the dataset is already well cleaned. almost nothing to do on this part. we just noticed some outliers in the adr column. we removed them.

## 3. Feature Engineering

By looking at some we noticed some interesting comportments so we decided to create some new features.

- `IsPortugal`: 1 if the country is Portugal, 0 otherwise
- `IsSameRoomType`: 1 if the reserved room type is the same as the assigned room type, 0 otherwise
- `IsGroup`: 1 if the customer type is group, 0 otherwise
- `IsChangeMade`: 1 if the booking was changed, 0 otherwise

These feature are interestingly correlated with the target variable.

![image](https://github.com/cesar1884/cancel_hotel_prediction/assets/94693373/e8efaec9-b5e5-42a5-9f08-3387ad3daac1)

## 4. Modeling

We tested four different models: Logistic Regression, Random Forest, XGBoost and Decision Tree. 

Random Forest gave us the best results:

           precision    recall  f1-score   support

           0       0.90      0.93      0.91      7277
           1       0.88      0.83      0.85      4394

    accuracy                           0.89     11671

The model has a good recall and a good precision. It is important to have a good recall because we do not want to predict a cancellation when there is not as we said.

