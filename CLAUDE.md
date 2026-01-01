# CLAUDE.md - Travel Planning System Reference

## Project: Brutus (Travel Recommendation Engine)

### Philosophy

"Brutus" refers to a curation style inspired by the Japanese magazine Brutus - design-forward, considered, anti-tourist-trap. Recommendations prioritise: local authenticity, architectural/design merit, seasonal appropriateness, and family practicality over guidebook standards.

-----

## Core Recommendation Logic

### Selection Criteria Hierarchy

```
1. Design/architectural merit (spaces worth experiencing)
2. Local authenticity (where locals actually go)
3. Seasonal appropriateness (what's good RIGHT NOW)
4. Family logistics (kid energy, timing, proximity)
5. Counter-programming (avoid peak crowds)
```

### Anti-Patterns (What to Avoid)

- Tourist-trap restaurants near major attractions
- Overpriced hotel dining as default
- Chain establishments when local alternatives exist
- Peak-hour visits to popular sites
- Over-scheduled days that exhaust kids

-----

## Recommendation Categories

### Food & Dining

```python
dining_tiers = {
    "market_grazing": {
        "description": "Assemble meals from market stalls",
        "examples": ["Ōmi-chō Market Kanazawa", "Toyosu Market Tokyo"],
        "best_time": "Early morning (6:30-9am)",
        "strategy": "Multiple small purchases, eat as you go"
    },
    "local_specialty": {
        "description": "Single-focus establishments",
        "examples": ["Menya Uguisu (ramen)", "Sushi Ikuta"],
        "timing": "Arrive 11:30 to beat lunch queue"
    },
    "kaiseki_experience": {
        "description": "Multi-course seasonal Japanese",
        "examples": ["Ichirin Kanazawa"],
        "context": "Special occasion, book ahead"
    },
    "hotel_room_picnic": {
        "description": "Market raid for in-room dining",
        "when": "Kids exhausted, need downtime",
        "strategy": "Sashimi, onigiri, seasonal fruit, local sake"
    }
}
```

### Cultural Sites

```python
site_approach = {
    "timing_strategy": {
        "temples_shrines": "Early morning or late afternoon",
        "museums": "Midday (when outdoor sites crowded)",
        "markets": "First thing (6:30-8am for fish markets)",
        "gardens": "Golden hour for photography"
    },
    "crowd_avoidance": {
        "primary": "Arrive at opening or 2hrs before close",
        "secondary": "Visit B-list alternative to A-list site",
        "example": "Kazue-machi over Higashi Chaya (quieter geisha district)"
    },
    "kid_energy_calibration": {
        "high_energy": ["Markets", "Interactive museums", "Castle grounds"],
        "medium_energy": ["Walking districts", "Craft workshops"],
        "recovery_zones": ["D.T. Suzuki Museum", "Hotel room", "Quiet cafes"]
    }
}
```

### Experiences & Activities

```python
experience_selection = {
    "hands_on_craft": {
        "gold_leaf_workshop": "Kanazawa - Gold Leaf Sakuda",
        "pottery": "Kutani Kosen Kiln - make, they ship to home",
        "value": "Kids remember making things > seeing things"
    },
    "observation_decks": {
        "purpose": "Contextualise city layout early in visit",
        "examples": ["Shibuya Sky", "Umeda Sky Building Osaka"],
        "timing": "Morning for shorter queues, sunset for drama"
    },
    "walking_routes": {
        "samurai_district": "Nagamachi earthen walls, Nomura House garden",
        "chaya_districts": "Higashi (main) → Kazue-machi (quiet alternative)"
    }
}
```

-----

## Day Structure Templates

### Full Day Pattern

```
MORNING (8-12)
├── Active/outdoor site (energy high)
├── Market breakfast or cafe
└── One major attraction before crowds

MIDDAY (12-3)
├── Lunch (arrive 11:30 for popular spots)
├── Indoor museum/gallery (heat/crowd escape)
└── Flexible: workshop OR rest at hotel

LATE AFTERNOON (3-6)
├── Second walking district
├── Garden or temple (golden hour)
└── Kid decompression activity

EVENING (6+)
├── Dinner decision based on energy level
├── Options: restaurant / market grazing / hotel room
└── Night view or illumination if energy permits
```

### Recovery Day Pattern (Post-Travel or Low Energy)

```
MORNING
├── Sleep in
├── Late breakfast at hotel or nearby cafe
└── Single low-key activity (museum, quiet garden)

AFTERNOON
├── Lunch
├── Return to hotel for rest/pool/downtime
└── Kids free time

EVENING
├── Easy dinner nearby
└── Early night
```

-----

## Japan Trip Specific Data

### Confirmed Itinerary Structure

```yaml
trip:
  dates: "December 18, 2025 - January 5, 2026"
  travelers:
    - Andrew
    - Sharmila (art curator - prioritise design/art venues)
    - Taj (10)
    - Maya (8)

segments:
  tokyo_arrival:
    dates: "Dec 18-21"
    accommodation: "Asakusa View Hotel"
    cost: "¥230,000"
    nights: 3
    purpose: "Jet lag recovery + initial exploration"

  nozawa_onsen:
    dates: "Dec 21-28"
    accommodation: "Tanuki Nozawa"
    nights: 7
    purpose: "Skiing with extended family"
    activities:
      - "Snowboard lessons Dec 23-24 (8:30am-12pm)"
      - "Meeting point: Schuss (Hikage area)"
      - "Provider: Nozawa Hospitality Ski School"
      - "Cost: ¥98,000 total"
    family_joining: "Rohana + others"

  matsumoto:
    dates: "Dec 28-30"
    accommodation: "Kaeru (frog street)"
    nights: 2
    transport_in: "Taxi Nozawa → Iiyama, train Iiyama → Matsumoto"

  kanazawa:
    dates: "Dec 30 - Jan 2"
    accommodation: "Shiori Machiya"
    location: "Nagamachi Samurai District"
    nights: 3
    transport_in: "Train via Nagano (~2.5hrs total)"
    highlights:
      - "Ōmi-chō Market (breakfast, 6:30-9am)"
      - "Higashi Chaya District (geisha quarter)"
      - "21st Century Museum of Contemporary Art"
      - "D.T. Suzuki Museum (contemplative architecture)"
      - "Kenroku-en Garden"
      - "Gold leaf workshop (Sakuda)"

  tokyo_final:
    dates: "Jan 2-5"
    accommodation: "Grand Nikko Tokyo Daiba"
    location: "Odaiba"
    nights: 2 (need Jan 2 gap night)
    cost: "¥139,060 (breakfast included)"
    booked_activities:
      - "teamLab Planets Jan 4 10:00am (¥13,400)"

flights:
  outbound:
    date: "Dec 18, 2025"
    routing: "Perth → Singapore (SQ224) → Tokyo Haneda (SQ634)"
    arrival: "21:40 Tokyo time"

  return:
    date: "Jan 5, 2026"
    routing: "Tokyo Haneda (SQ631 08:50) → Singapore → Perth (SQ215)"
    arrival: "23:55 Perth time"
```

### Transport Booking Status

```yaml
needs_booking:
  - "Nozawa → Iiyama taxi (Dec 28)"
  - "Iiyama → Matsumoto train (Dec 28)"
  - "Matsumoto → Kanazawa train (Dec 30)"
  - "Kanazawa → Tokyo Shinkansen (Jan 2)"
  - "Tokyo hotel for Jan 2 night (gap before Grand Nikko)"

shinkansen_notes:
  - "Book from Dec 2 (one month ahead)"
  - "Kanazawa → Tokyo: Kagayaki ~2h30m, ~¥14,000/person"
  - "Peak season - book early"
```

-----

## Location-Specific Brutus Recommendations

### Kanazawa

```yaml
morning_priorities:
  - venue: "Ōmi-chō Market"
    time: "6:30-9am"
    order: "Kaisendon, crab, seasonal sashimi"
    strategy: "Graze multiple stalls vs sit-down"

  - venue: "Higashi Chaya District"
    time: "9-10am (before crowds)"
    highlight: "Geisha House Shima - matcha + wagashi"
    alternative: "Kazue-machi (quieter, along river)"

lunch_spots:
  - venue: "Menya Uguisu"
    cuisine: "Toripaitan ramen"
    order: "Noodles katame (firm)"
    timing: "Arrive 11:30"
    location: "Tatemachi"

  - venue: "Sushi Ikuta"
    highlight: "Scraped squid nigiri"
    location: "Across from Menya Uguisu"

  - venue: "Amatsubo"
    location: "Ōmi-chō Market"
    order: "Omakase - tell them budget, they select"
    tip: "Trust the chef, skip the English menu photos"

afternoon:
  - venue: "21st Century Museum of Contemporary Art"
    highlight: "Swimming Pool installation (Leandro Erlich)"
    good_for: "Sharmila (art curator background)"

  - venue: "D.T. Suzuki Museum"
    architect: "Yoshio Taniguchi"
    vibe: "Contemplative, minimal, water garden"
    good_for: "Adult decompression while kids rest"

  - venue: "Gold Leaf Sakuda"
    activity: "Gold leaf pressing workshop"
    good_for: "Kids - hands-on making"
    note: "Kanazawa = 99% of Japan's gold leaf"

  - venue: "Kutani Kosen Kiln"
    activity: "90-min pottery with master"
    output: "They fire and ship to Perth"
    good_for: "Lasting memory/souvenir"

evening:
  - venue: "Kenroku-en Garden"
    time: "Late afternoon light"
    note: "One of Japan's three great gardens"

  - venue: "Ichirin"
    cuisine: "Kaiseki in renovated machiya"
    history: "Former home of printmaker Clifton Karhu"
    context: "Special dinner, book ahead"

walking_districts:
  - name: "Nagamachi (Samurai District)"
    highlights: ["Earthen walls", "Nomura Family House (exceptional garden)"]
    cafe: "Isotope - coffee or amazake"

  - name: "Higashi Chaya"
    type: "Main geisha district"
    temple: "Hohsen-ji (bamboo, peaceful, up the hill)"

  - name: "Kazue-machi"
    type: "Smaller geisha district"
    advantage: "Quieter, along Asano River"
```

### Tokyo (Odaiba Base)

```yaml
day_one_local:
  morning:
    - venue: "Toyosu Market"
      time: "6:30-7am arrival"
      activity: "Tuna auction viewing deck"
      breakfast: "Sushi Dai or Daiwa Sushi (queue worth it)"

  late_morning:
    - venue: "SMALL WORLDS TOKYO"
      description: "1/80 scale miniature worlds"
      sections: ["Sailor Moon", "Evangelion", "Working airport"]
      good_for: "Kids - obsessive detail"

  afternoon:
    - venue: "Miraikan (National Museum of Emerging Science)"
      highlights: ["ASIMO demos", "Geo-Cosmos globe"]
      good_for: "Interactive, playful science"

  evening:
    - venue: "DECKS Tokyo Beach"
      highlight: "Daiba 1-chome Shotengai (1960s retro street)"
      vibe: "Tacky but fun with kids"
      view: "Rainbow Bridge sunset"

day_two_shibuya_daikanyama:
  description: "Brutus heartland"

  morning:
    - venue: "Shibuya Sky"
      time: "Early (shorter queues)"
      purpose: "Contextualise Tokyo from above"

  midday:
    - venue: "Daikanyama T-Site"
      description: "Design-focused bookstore complex"
      good_for: "Sharmila - architecture, design books"
      cafe: "Ivy Place or Anjin"

  afternoon:
    - venue: "Nakameguro"
      activity: "Canal walk, independent shops"
      coffee: "Onibus Coffee"

day_three_culture:
  options:
    - venue: "Nezu Museum"
      description: "Art + exceptional garden"
      location: "Omotesando area"

    - venue: "21_21 Design Sight"
      architect: "Tadao Ando"
      location: "Roppongi"
      good_for: "Design exhibitions"

    - venue: "Yanaka"
      description: "Old Tokyo neighbourhood"
      activity: "Cemetery walk, shotengai shopping street"
      vibe: "Slow pace, local feel"
```

-----

## Decision Frameworks

### Restaurant Selection

```python
def select_restaurant(context):
    if context.kid_energy == "low":
        return "hotel_room_picnic" or "casual_nearby"

    if context.time_of_day == "lunch" and context.location.has_ramen:
        return "arrive_1130_beat_queue"

    if context.occasion == "special":
        return "kaiseki_book_ahead"

    if context.morning and context.near_market:
        return "market_grazing"

    return "local_izakaya"
```

### Activity Pacing

```python
def plan_day(energy_forecast, weather, interests):
    activities = []

    # Morning: highest energy activity
    if weather.outdoor_friendly:
        activities.append(select_outdoor_priority())
    else:
        activities.append(select_museum())

    # Midday: food + indoor/recovery
    activities.append(lunch_near_morning_activity())
    if energy_forecast.kids == "moderate":
        activities.append(workshop_or_museum())
    else:
        activities.append(hotel_rest())

    # Afternoon: calibrate to remaining energy
    if energy_forecast.remaining == "high":
        activities.append(second_walking_district())
    else:
        activities.append(quiet_garden_or_cafe())

    return activities
```

### Counter-Programming Logic

```python
timing_rules = {
    "popular_temples": {
        "avoid": ["10am-2pm weekends", "11am-3pm weekdays"],
        "prefer": ["Opening time", "Last 2 hours before close"]
    },
    "markets": {
        "avoid": ["After 10am"],
        "prefer": ["6:30-8:30am"]
    },
    "observation_decks": {
        "avoid": ["Sunset on clear days (everyone's idea)"],
        "prefer": ["Morning clear day", "Overcast sunset (fewer people)"]
    },
    "museums": {
        "prefer": ["Midday (outdoor crowd escape)", "Rainy days"]
    }
}
```

-----

## Output Formats

### Daily Itinerary Format

```markdown
## [LOCATION] — Day [N]

### MORNING
**[Venue Name]** (time)
Brief description. Specific order/action. Why it matters.

### MIDDAY
**[Lunch Spot]**
What to order. Timing strategy.

### AFTERNOON
**[Activity/Venue]**
Context. Kid-appropriateness note.

### EVENING
**Dinner options:**
*For [context]:* [Venue] - [description]
*For [alternative context]:* [Alternative]
```

### Booking Checklist Format

```markdown
## Action Items

| Priority | Task | When |
|----------|------|------|
| HIGH | [Urgent item] | ASAP |
| MEDIUM | [Important item] | [Timeframe] |
| LOW | [Nice to have] | [Timeframe] |
```

-----

## Sharmila-Specific Interests (Art Curator)

### Architecture Priorities

```yaml
architects_to_seek:
  - "Tadao Ando (21_21 Design Sight, Omotesando Hills)"
  - "Yoshio Taniguchi (D.T. Suzuki Museum)"
  - "SANAA (21st Century Museum Kanazawa)"
  - "Kengo Kuma"

museum_priorities:
  - "Contemporary art over historical"
  - "Architecture as experience"
  - "Design museums and bookstores"
  - "Gallery districts (Roppongi, Omotesando)"
```

### Design Shopping

```yaml
tokyo:
  - "Daikanyama T-Site (design bookstore)"
  - "Omotesando (architecture walk)"
  - "Spiral Building (Fumihiko Maki)"

kanazawa:
  - "21st Century Museum shop"
  - "Kutani pottery studios"
  - "Gold leaf craft shops"
```
