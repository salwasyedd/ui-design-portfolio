## Affordances & Physical Properties

The smart closet is a walk-in closet: a fixed, room-sized storage space, not a
portable object. It is built into the physical structure of a home. Its affordances include:

- **Enterable space**: users physically walk into it, unlike a cabinet or drawer they'd reach into.
- **Multiple surfaces**: hanging rods, shelves, floor space, drawers, and a door/entryway. This means any smart interface has to span more than one surface. Perhaps have multiple of screens differing in location within closet.
- **Threshold/entry point**: the door or entryway is a natural place to check information *before* entering, without needing to step inside.
- **Interior storage surfaces**: rods, shelves, and drawers are where sensing (ex. item usage, humidity) would need to physically live, since that's where the clothes are.
- **Fixed location, ambient conditions**: unlike a portable object, its environment (temperature, humidity, airflow) is tied to the room it's in.


## Assumed Smart/Sensing Features

- Temperature and humidity sensors inside the closet, reported on an exterior panel
- Per-item usage tracking - records when an item was last worn and how many times
- Weight/motion sensors on the hamper or laundry bin to estimate how much is dirty vs. clean
- Ability to tag/categorize items (ex. by color, type, occasion) for filtering
- A simple recommendation engine that cross-references weather + activity type to suggest an outfit
- Task/scenario-based interaction: user selects an activity (ex. "gym," "work," "dinner") and the closet highlights or suggests relevant items

## Interview Questions

1. Walk me through how you use your closet on a typical morning.
2. How do you decide what to wear each day?
3. How do you keep track of what's clean, what needs washing, or what's in between?
4. How organized, how full, etc. is your closet?
5. What would you say the ideal temperature and humidity is for a closet, if you had to guess?
6. Imagine your closet could sense and report things about itself — like temperature, humidity, or how often items are used. What kinds of information would be useful to you, if any?
7. What kinds of information would you rather it not track or show, if any?
8. If your closet had a screen or panel on it, how big and where would you want it?
9. Is there anything else about how you use or organize your closet worth mentioning?

## Interview 1 — Hana

1. Walks into her closet and thinks about her activity for the day. Looks at the temperature and decides how formal or informal she wants to be based on that activity. Gets dressed in order: undergarments, then pants, then top, then shoes.
2. Decides based on the day's activity and the temperature. Sometimes needs multiple outfits in a day. Also depends on how much time she has in the morning.
3. Clean clothes stay hung up; dirty clothes go into the hamper. Her closet is organized enough that she generally knows what she's worn and how often. She doesn't keep clothes she doesn't like, so she doesn't end up with many unworn items sitting around.
4. Pretty organized, but very full.
5. About 72°F, maybe a little warmer in the morning for a "cozy wake-up" feeling.
6. Mainly just the weather. Also stats on how often she's worn certain items, so she can decide if something should be given away or thrown out.
7. No response given.
8. On the door or an inside wall. Doesn't need to be big — iPad mini size is enough.
9. Nothing further.

## Interview 2 — Shahar

1. Doesn't interact with her closet much in the morning — usually picks her outfit the night before, since mornings are rushed and she wants that routine to be as efficient as possible. In the morning she just grabs undergarments.
2. Depends on her mood — whether she wants to look put together or not — and on the day's activity.
3. For jeans: she rewashes them after riding public transit or sitting outside, depending on what she did while wearing them. For tops: if she's worn one for a long stretch, it goes in the wash; if it was brief (ex. just dinner), it goes back in the closet.
4. Feels full and organized to her, though others might not agree. She'd like to organize it more, but since she's moving soon, she isn't prioritizing it right now.
5. Doesn't have a strong preference — whatever matches the rest of the house.
6. Weather, plus outfit recommendations based on it. She liked the idea of the closet lighting up the area where a suggested clothing type is (ex. lighting up long-sleeve tops on a chilly day). Also wants to know when she last wore something, especially for work clothes. She'd like to select an activity/scenario and get an outfit recommendation for it, or select clothes and see how they'd look together or on her. She also wants inventory tracking - ex. knowing she has 2 clean sweatpants and knowing when laundry is needed based on what's clean vs. dirty and what's coming up. She'd also want to filter by tags or descriptions (ex. "how many red bags do I have?" or "how many fancy outfits do I have?").
7. Nothing — she said it doesn't track anything right now, so there's nothing she's currently opposed to.
8. Wants it mounted outside the closet door, before entering. iPad mini size.
9. Nothing further.

## Interview 3 — Ekra

1. Uses an over-the-door hook to hang the outfit she plans to wear that day.
2. Usually picks her outfit the night before, though not always — it depends on her mood and mental state. When she plans ahead, she feels more organized and ready for the day; when she doesn't, she tends to rush and is less happy with what she ends up wearing. The overall "vibe" of the outfit depends on her plans (ex. a work uniform requires no real decision-making).
3. Uses three baskets: one for dirty clothes, one for clothes worn outside that aren't dirty but haven't been put away, and one for clean clothes or try-on items that haven't been hung up yet.
4. Currently messy due to recently returning from travel — her closet's state tends to reflect her routine and mental state; when she's in a good routine, it's very organized, and clutter bothers her. She organizes by material type and color.
5. Slightly below room temperature, especially since the closet is dark.
6. Would like the closet to alert her when she needs to do laundry, especially when running low on essentials like socks or underwear. Would also like a digital tracker/catalog of everything in her closet.
7. Not sure.
8. Wants the panel on the outside of the closet door for easy access, and would like it linked to a phone app as well.
9. Uses an app called Whering that lets her photograph every clothing item to build a digital catalog and put together outfits. She likes that it's made her more intentional about what she buys, and that seeing her wardrobe visually/numerically helps her remember pieces she forgets she owns and be more creative with outfits.

## Summary of Findings

All three users make outfit decisions based on the day's planned activity, with weather/temperature as a secondary factor. Time of decision varies — some choose the night before to reduce morning stress, others decide in the moment — suggesting the interface should support both a "plan ahead" and a "quick decision" mode rather than assuming one routine.

Tracking clean vs. dirty clothes is currently informal and physical (baskets, hampers, hanging habits) rather than digital. Two users independently expressed interest in the closet flagging laundry needs before running low on specific items (ex. socks, underwear, sweatpants), reinforcing this as a core feature rather than a nice-to-have.

Closet organization was described as closely tied to routine and mental state — clutter builds up during disruptions (ex. travel) and clears up when things are going well. This suggests the interface could offer help re-organizing or catching up after a disruption, rather than assuming a static, ever-tidy closet.

All three users independently wanted the panel mounted on the outside of the closet door, consistently around iPad-mini size — a strong, unanimous signal for placement and scale. Two users also wanted the system to connect to a phone app, extending the closet's information beyond the physical panel.

Desired feature depth varied: one wanted just the basics (weather, usage stats), while the other two wanted richer functionality — outfit recommendations, visual matching/highlighting, digital inventory cataloging, and phone integration. This supports a layered design: essential status visible at a glance, with deeper tools (recommendations, inventory, filtering) available on demand rather than forced onto the main screen.

## User Needs & Design Requirements

| User Need | Design Requirement |
|---|---|
| Users want to know the weather/temperature before choosing an outfit | Panel must display current temperature (and ideally forecast) |
| Users want outfit suggestions based on weather and activity | System must let user select an activity/scenario and return a suggested outfit |
| Users want to know when an item was last worn | Each item must have a "last worn" timestamp visible on demand |
| Users want to be alerted before running low on clean essentials (socks, underwear, everyday items) | System must track clean/dirty counts per category and flag low-stock items |
| Users want to know how much needs washing before laundry day | System must display counts of clean vs. dirty items across categories |
| Users want a digital catalog/inventory of everything they own | Interface must support a browsable digital inventory of clothing items |
| Users want to filter/search their wardrobe by attributes (color, type, formality) | Interface must support tag-based filtering |
| Users want visual guidance on where a suggested item is physically located | Closet should indicate item location physically (ex. a light near matching clothes) |
| Users want the option to visualize outfits together before committing | Interface should allow selecting multiple items to preview as a combined outfit |
| Users want a compact interface that doesn't dominate the space | Panel should be small (tablet/iPad-mini sized) |
| Users want the panel accessible before entering the closet | Primary panel must be mounted outside/near the entry, not deep inside |
| Some users want closet data extended to their phone | System should support (or at least conceptually allow for) a companion mobile app view |
| Some users want minimal tracking
