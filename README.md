# TravelPack

## Description

A travel web application that allows members to join a pack and plan a vacation together. Users can join multiple packs, and each pack is composed of one or more schedule(s) created by the members, which then filled with events. Users can also keep track of money owed to other pack members as well as upload photos to the group.

## Technologies Used

* MERN: mongoDB, Express, React, Node.js
* Amazon Web Services
* Chart.js

## Link

[TravelPack](http://travel-pack.herokuapp.com/)

## Site Features

---

### Pack Show

![Pack Show](/readme_media/pack-show.png)

> Shows Pack Information, and has links to the schedules, expenses and photo sections. Pack Code and Password are distributed to other people in order for them to join the pack as well.

### Expenses

![Pack Expenses](/readme_media/expenses.gif)

> Expenses allow pack members to keep track of any debt owed to other pack members. Also has a breakdown of what the money is being spent on.

### Schedule and Events

> Allow pack members to create schedules and events for their pack. Schedules can have many events.

```
Schedule's Backend API for updating nested objects with MongoDB.

router.put("/:scheduleId", (req, res) => {
  let packId = parseURL(req.baseUrl);
  Pack.findOneAndUpdate(
    { _id: packId, "schedules._id": req.params.scheduleId },
    { $set: {"schedules.$.startDate": req.body.startDate,
            "schedules.$.endDate": req.body.endDate,
            "schedules.$.title": req.body.title
    }}).then(() => { 
      Pack.find({_id: packId, "schedules._id": req.params.scheduleId},
        { "schedules.$": 1})
        .then(schedule => res.json(schedule[0].schedules[0]))
    });
});
```

```
Event's axios API call. Deeply nested.

export const updateEvent = data => {
  return axios.put(`api/packs/${data.packId}/schedules/${data.scheduleId}/events/${data.eventId}`, data)
}
```

---

### Distribution of Tasks

* User Authentication: Mary, Justin
* Packs CRUD: Mary
* Schedules CRUD: Kevin
* Events CRUD: Kevin
* Payments CRUD: Mary, Mohit
* AWS Photo Uploading: Justin
