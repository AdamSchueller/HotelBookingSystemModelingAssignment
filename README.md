
# Hotel Booking System: A Design & Modeling Exercise

**Home Assignment:**  Model a booking software system for a single hotel and document the design. This is not a coding exercise – the output should be documentation only, in whatever format(s) you choose (UML, ArchiMate, C4, flow charts, block diagrams, sequence diagrams, etc.). The focus is on decomposing a complex system into smaller, more manageable functional parts and how those parts interact with each other, completely independent of any specific technology choices. 

The following details should be fully documented: 

- Interactions between users (both the guests & the hotel employees)
   and the system at all points in the workflow
- All major logical system components, clearly separated   
- Any important data used by the system components  
- How the system components communicate and coordinate, including any
   cross-component commands, events, or shared data 
- Usage of any abstract data types or patterns (like queues, brokers,
   buses, messages, etc.) that are part of your solution

**Out of scope:** 
- Multiple hotel locations 
- Booking multiple rooms at once 
- Managing the # of guests checking in 
- Guest reviews/comments 
- Additional hotel services (Pay-Per-View, minibar, etc.) 
- User authentication/authorization 

 
## Use Cases
The system must support the following use cases: 

**Use Case #1:** Guest searches for rooms by date range, price, and/or type 
- List rooms, including additional details associated with the different room types (photos, amenities, etc.) 

**Use Case #2:** Guest reserves a room for a given date range 
- User selects room (by type only, not by specific room #) 
- Collect guest information 
- Collect payment information (multiple credit cards and PayPal supported) 
- Book room @ current rate (price fluctuate seasonally & based on current occupancy rate) 

**Use Case #3:** Guest checks into the hotel  
- Find the user’s reservation 
- Fulfill reservation with an unoccupied room at the hotel 
 
**Use Case #4:** Guest cancels reservation 
- Free if done 24 hours prior to check-in 
- Bill guest for 1 night if canceled within 24 hours of check-in 

**Use Case #5:** Guest checks out 
- On last night, print summary of expected bill for stay 
- During checkout, bill guest for final amount using either the payment info from the reservation, or a new payment method chosen by the user at this time 
- Make room available again after checkout completes 


## Modeling Tips
Breaking down the system into components is all about finding the boundaries between them. A highly modular monolithic solution is possible, but the documentation should be equally applicable to a service-oriented solution, and be able to answer the following questions: 

How many independent services in different contexts/domains could the system be built with? What business functionality is each service responsible for? 

What data does each service own – meaning it is the source of truth for that data? How is that data leveraged by other services that don’t own it? 

How do the various UI’s (for both guests and hotel workers) interact with the different services at different points in the workflow? What data do they show? Where do they get that data from? What actions can be executed from each one? 

What important business events exist in the system? At what point in the workflow are they triggered? Which services publish & subscribe to those events?  

  

## Edge Cases to Include
The documentation should cover solutions for the following scenarios: 

- EC#1: Only one room left, two people trying to book at the same time – how to handle this scenario gracefully? (note: overbooking is OK, but not infinitely!) 

- EC#2: How would no-shows be handled? Which component owns and triggers the no-show logic, and which are impacted by the event? (note: consider factors like a reasonable grace period, and assume a 1-night charge is applied for no-shows) 

- EC#3: How should the system behave when payment is declined at different points in the workflow? (note: assume credit holds are placed when making reservations) 

- EC#4: How would the system deal with guests that want to switch rooms mid-stay? Which components would be impacted by that action? Which would not? 
