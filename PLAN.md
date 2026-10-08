# Split: proof of concept plan

_Draft prepared with AI assistance: requires review. Training and fuelling content is general guidance, not advice from a qualified coach or dietitian._

Agreed 8 October 2026.

## 1. What Split is
A website that plans a full triathlon season with AI, then **adapts the plan to actual performance** using Garmin data.

The long-term vision is a platform where anyone can author, share and follow programs for any sport or goal. The proof of concept is **for Max only**, to use and refine before sharing it with anyone.

Core features:
1. AI-generated programs based on a sport and goal
2. A program that reacts to performance (from Garmin or entered manually)
3. A history of completed workouts
4. A training calendar

## 2. The season
- **Start:** Monday 12 October 2026. The first two weeks include benchmark tests: swim (timed 400 m and 200 m), run threshold, and Zwift FTP.
- **Total length:** about 60 weeks.

| Race | Date | Role | Goal |
|---|---|---|---|
| Gold Coast T100, Olympic | Sat 20 Mar 2027 | A race inside the 70.3 build. Short ease-off before, short reset after. | Good time, about 2:30–3:00 |
| Ironman Western Sydney 70.3 | Sun 2 May 2027 | Focus of the first block. Key data point for Busselton. | About 5:30 (last 70.3: 6:20) |
| Ironman Busselton | Sun 5 Dec 2027 | **Primary goal (A race)** | Finish first; time goal possibly set later |

**Structure:** base → 70.3 build (Olympic inside it) → final 70.3 block → taper → 70.3 → reset → Busselton build → taper → Busselton.

Gaps between races, worked out from the dates:
- Start to Olympic: about 23 weeks
- Olympic to 70.3: about 6 weeks (43 days)
- 70.3 to Busselton: 31 weeks, which leaves about 28 weeks of building after a 2–3 week reset

## 3. Athlete starting point
| Sport | Status | Benchmarks |
|---|---|---|
| Swim | Weakest sport. Mostly pool, occasional open water. Not swum since winter. | 70.3 swim 46 min. Needs a test. |
| Bike | Strongest sport. Heart-rate strap; power only on Zwift (smart trainer). No outdoor power meter. | FTP about 245 W. 70.3 ride 3:06. |
| Run | Much improved since the last 70.3, where it faded through running out of energy. Easy runs by heart rate and pace, intervals by pace. | Watch threshold 4:50/km at 170 bpm (probably optimistic). 10 km race 51:00 (5:06/km). 70.3 run 2:15. |

Experience: every triathlon distance except a full Ironman.

## 4. Weekly template
- **Sessions:** 1–2 a day, with **no more than one session per sport per day**
- **Friday:** rest. **Saturday:** long ride. **Sunday:** long run.
- **Gym:** 2 sessions a week (3 at most), 45–55 minutes each, written by the AI. Focus on supporting swim, bike and run, and injury prevention. Full commercial gym.
- **Bricks:** two separate sessions (bike, then run) labelled as linked
- **Race weeks:** break the usual template as needed (for example, the Olympic is on a Saturday)
- **Weekly hours:** not fixed yet; adjust as we go

## 5. How the plan adapts
Principles:
- **Performance is the source of truth.** Only training performance triggers suggestions.
- **Sleep, body weight and gym work are context only.** They help explain changes in performance but never trigger changes themselves.
- **Every program change is a suggestion the user accepts.** Nothing changes automatically.
- **Only information updates automatically**, such as estimated finish times and trend charts.

Rules:
| Situation | What happens |
|---|---|
| One missed session | Nothing |
| A pattern of missed sessions (default: 3 or more in 7 days, or the same key session missed twice) | Ask: **carry on**, **ease back in**, or **make up the key sessions**. Then watch performance, and suggest an adjustment if it drops. |
| A deleted session | Counts as missed |
| One great session | Nothing, apart from updating the estimated finish time |
| A consistent improvement (default: 2–3 weeks) | *"Based on your recent performance you could aim for X. Do you want to adjust your program to aim for that?"* |
| A race result | Feeds forward. For example, the 70.3 result updates the Busselton projection, with the same suggest-and-accept prompt. |

- **Estimated finish time:** shown for every race, based on recent performance.
- **Thresholds:** all the defaults above are **settings that can be changed**, not hard-coded values.
- **Measuring performance:**
  - Run: pace, and pace against heart rate on easy runs.
  - Bike: power on Zwift; heart rate (and speed, with caution) outdoors.
  - Swim: pace per 100 m from pool sessions.

## 6. Data
| Data | Source | Use |
|---|---|---|
| Swim, bike and run activities | Garmin Connect (Zwift rides sync to Garmin) | Performance (source of truth) |
| Sleep | Garmin | Context only |
| Body weight | Garmin scale | Context only |
| Gym sessions | RepCount at the gym, then **logged manually** on the website: tick off, plus optional sets, reps and weights | Context only |
| Food | Not tracked | — |

**Matching:** a recorded activity is matched to the planned session for the same sport on the same day. If nothing matches, it's saved as a standalone activity. To move a session, change its day on the website.

## 7. Workouts and devices
- **Garmin:** workouts should appear in the Garmin calendar so they can be started from the watch. This depends on Garmin access (see section 10).
- **Zwift:** the website describes the session (for example "3 × 10 min at 95% FTP"), and Max chooses a similar Zwift workout.
- **Outdoor rides:** the website sets the session goal. Max plans the routes.
- **Fuelling:** long sessions and race days include fuelling suggestions, such as carbs per hour and practising race nutrition.

## 8. The website
- A season calendar with **drag and drop**, **edit** and **delete**
- Workout history comparing planned with actual
- Estimated finish time for each race
- Suggestions to accept or decline
- Gym logging that works on a phone screen

## 9. How we build and run it
- **Runs locally** on Max's Mac
- **AI work happens in Claude Code chat sessions.** Max asks, for example to generate the season or review the last 2 weeks, and Claude writes the results into the project. No API key yet.
- **If an API key is ever needed,** it will be under a **personal** Claude account, not the aXcelerate account.
- **Roles:** Max is the product owner and tester. Claude does most of the building and explains key decisions.

## 10. Garmin access (biggest risk)
Research done on 8 October 2026:
- **Official access isn't available to us.** Garmin's developer program is for businesses only, not personal use. It's also reported that new applications are currently paused.
- **Community Garmin "MCP servers" exist.** These are add-ons that let Claude read your Garmin Connect data (activities, sleep, heart rate, weight) directly in a chat. They fit the "AI work in chat sessions" approach well.
- **The downsides of MCP servers:**
  - They're unofficial and use your own Garmin login, so they can break when Garmin changes things, and they may conflict with Garmin's terms of use.
  - They're third-party code with access to your account. Pick a well-maintained, read-only one, and review it before installing.
  - Max enters the Garmin login directly. Claude never handles it.
  - Most are read-only. **Sending workouts to the Garmin calendar** needs separate checking.

## 11. Not in the proof of concept
- Sharing, other users, accounts, and other sports' programs
- Food logging
- Outdoor route planning
- Sending workouts to Zwift
- Online hosting
- An automatic AI connection through an API
- Reading RepCount screenshots with AI
- Working out weekly hours from Garmin history (to confirm)

## 12. Next steps
1. Choose and vet a Garmin MCP server. Max installs it and confirms Claude can read recent activities.
2. Check whether workouts can be sent to the Garmin calendar, and how.
3. Decide on the tech setup and data structure, then build the calendar and data model.
4. Generate the season plan for 12 October 2026 to 5 December 2027.
