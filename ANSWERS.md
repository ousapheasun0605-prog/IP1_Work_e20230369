# Week03 answers
1. Why should we not use the array index as :key?

Using the array index as :key can cause Vue to reuse a component for a different event when the list is filtered or reordered. If a card has local state, such as an open details panel, that state may appear on the wrong event. Using a stable identifier such as event.id allows Vue to track each event correctly.

2. Why is visible a computed property?

visible is a computed property because its value depends on the events, search text, and selected category. Vue automatically recalculates it when one of these reactive dependencies changes, and caches the result until a dependency changes. A regular function called in the template may run again during each render, even when its inputs have not changed.

3. Why does EventCard emit book instead of changing event.booked?

Emitting a book event keeps EventCard responsible for displaying the event and reporting the user's action, rather than modifying shared data itself. The parent component can validate the booking, update the event, and record the user's booking in one place. This makes the data flow easier to understand and maintain.

4. Why does destructuring booked from reactive(event) cause problems?

In const { booked } = reactive(event), destructuring copies the current value of booked into a separate local variable. Incrementing that variable does not update the original reactive object's property, so Vue does not detect a change to event.booked. Updating event.booked directly or using toRef(event, "booked") preserves the reactive connection.

5. Where does myBookings live, and why?

myBookings lives in App.vue because it represents the user's bookings across the application, not just the state of one event card or the event list. Keeping it in the parent allows App.vue to update the booking count, handle booking logic, and persist bookings across reloads. EventCard and EventList can then focus on displaying events and forwarding user actions.