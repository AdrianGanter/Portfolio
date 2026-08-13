# Grym Project

## Overview

Grym was an independent multimedia project that began as a solo heavy metal music venture and evolved into an interactive live entertainment experience combining original music, storytelling, automation, livestream production, virtual world-building, and audience participation.

The project was built around the character **Grym**, a Grim Reaper-inspired musician who existed within an original fantasy world known as the Nether Realm and later exploring the oceans of Hell on the Flying Dutchman. What started as a simple concept—a Grim Reaper performing heavy metal music live online—gradually expanded into a long-form narrative featuring original characters, locations, lore, and ongoing story arcs.

<img width="4000" height="2256" alt="Captain Grym" src="https://github.com/user-attachments/assets/f7ca2ece-a02d-4e10-b88a-6cd3cbb80e44" />

Over several years, the project grew into a highly interactive production that blended:

- Original music composition and performance
- Character acting and storytelling
- Livestream production
- Automation systems
- Unreal Engine world-building
- Audience-driven interactions
- Voice-controlled workflows
- Real-time visual effects

The goal was to create a unique live experience where music, narrative, technology, and community participation all existed within the same world.



---

## Project Evolution

### Phase 1 – Music Project

Grym initially started as a solo heavy metal project focused on:

- Writing and recording original music
- Performing live on Twitch and Kick
- Building a community around music, gaming, and entertainment
- Developing a unique stage persona

The visual identity centered around a Grim Reaper character performing music live using costumes, lighting, fog effects, and themed environments.

<img width="640" height="364" alt="SmartSelect_20201206-221345_Twitch" src="https://github.com/user-attachments/assets/b5b7917e-c48a-4bcc-bd79-7bdd0df9126e" />

---

### Phase 2 – Storytelling & World Building

As the project developed, the focus expanded beyond music into creating a larger fictional universe.

New elements included:

- Original lore
- Character development
- Locations like the Nether Realm and Hell
- Story-driven livestreams
- Narrative progression through music releases

Songs became connected to story events, allowing music releases to advance the world and characters rather than existing as standalone releases.

<img width="1920" height="1080" alt="card 2" src="https://github.com/user-attachments/assets/e61b8d6b-8212-4f26-b0e0-7850b33d0c2c" />


---

### Phase 3 – Advanced Livestream Production

The project evolved into a highly produced livestream experience.

A green-screen setup allowed Grym to perform inside custom digital environments while visual effects, camera angles, and scene transitions enhanced performances.




Production elements included:

- Layered environments
- Atmospheric effects
- Dynamic scene composition
- Multi-camera setups
- Automated visual sequences

A secondary low-angle camera was introduced to create dramatic action shots during heavy musical sections, helping performances feel more cinematic and energetic.




---

### Phase 4 – Unreal Engine Integration

A major milestone was the transition from static 2D environments to a fully realized 3D world built in Unreal Engine.

<img width="568" height="320" alt="Remembrance GIF" src="https://github.com/user-attachments/assets/0fd5b531-4305-4836-b976-b906dddaeeff" />


<img width="568" height="320" alt="FloorCam" src="https://github.com/user-attachments/assets/350d0dad-43b5-48a3-84f1-68004e096a00" />


Over approximately a year of development, a prototype virtual world was created featuring:

- Custom environments
- Cinematic camera systems
- Sequenced story events
- Character locations
- Interactive performance spaces

The project used Unreal Engine's cinematic tools to create camera movement, transitions, and narrative scenes that could be integrated directly into live performances.

A billboard-style character system was developed where the live green-screened performer continuously rotated to face the active camera, allowing dynamic camera movement around the performer while maintaining visual consistency.


<img width="1936" height="1096" alt="ScreenShot00006" src="https://github.com/user-attachments/assets/14f56622-06a7-48a7-8855-875ca38ef7a5" />

<img width="1472" height="838" alt="image" src="https://github.com/user-attachments/assets/c34bdf30-7576-4db7-8912-98a0f1da6fc1" />

---

## Story Development

The project's central narrative followed Grym's journey through the Nether Realm.

One major storyline focused on Grym's search for a mysterious Wizard character who had disappeared after being captured by the First Demon of Hell.

This storyline introduced:

- Quest-based narrative progression
- The Flying Dutchman
- New environments and locations
- Story milestones tied to music releases
- Character-driven world exploration

Songs from a planned album served as narrative chapters, advancing the story through both music and live performances.

Although the storyline ultimately remained unfinished, multiple chapters, locations, and narrative arcs were successfully developed and performed live.

<img width="1920" height="1080" alt="Card 1" src="https://github.com/user-attachments/assets/7315ea2f-bdfe-4a19-b57c-18fb230c10a3" />

---

# Systems I Built

## Livestream Automation System

One of the project's primary technical goals was reducing manual workload during performances.

Using automation tools and custom workflows, I built systems that synchronized multiple production elements in real time.

### Automated Camera Control

- Automatic camera switching based on song sections
- Dynamic transitions during key musical moments
- Low-angle performance shots triggered during breakdowns
- Hands-free operation during live shows

---

### Automated Visual Effects

Effects were synchronized to specific moments within songs, including:

- Fire effects
- Explosions
- Snowstorms
- Atmospheric effects
- Environmental changes
- Abstract visual sequences

This allowed performances to remain visually dynamic without requiring manual intervention.

---

### Guitar Effects Automation

Guitar tone changes were automated throughout songs.

The system automatically switched:

- Rhythm tones
- Lead tones
- Clean tones
- Effect chains

This ensured consistent performance transitions while reducing the need for manual pedal interaction during live shows.

---

### Voice Control System

A voice-controlled workflow was implemented using Streamer.bot and supporting automation tools.

Voice commands could trigger:

- Scene changes
- Teleportation events
- Song control
- Performance actions
- World navigation

Examples included commands that instantly moved Grym between locations within the virtual world while triggering corresponding animations and effects.

This allowed the majority of performances to be conducted hands-free.

---

### Unreal Engine Event Systems

Various gameplay-style systems were built using Unreal Engine Blueprints, including:

- Teleportation systems
- Cinematic sequences
- Camera management
- Interactive world events
- Trigger-based animations
- Environment transitions

These systems enabled real-time interaction between the performer, audience, and virtual world.

---

## Audience Interaction Systems

A major focus of the project was giving viewers direct influence within the world.

### Live Chat Integration

Viewers could use chat commands to interact with the Unreal Engine environment in real time.

Features included:

- Spawning skeleton characters
- Creating audience avatars
- Triggering actions
- Participating in world events

Each spawned skeleton displayed the viewer's username, creating a personalized connection between audience members and the virtual world.

---

### Interactive Arena System

A dedicated "Soul Arena" was created where viewers could participate through chat commands.

Interactions included:

- Skeleton spawning
- Mosh pits
- Circle pits
- Crowd actions
- Event participation

This transformed passive viewers into active participants within the performance space.

**▶️ Click the image below to watch the video**
[![▶ Watch Video](https://github.com/user-attachments/assets/7640c576-47ea-415d-8bed-08427a9aec6b)](https://www.youtube.com/watch?v=N84fiultTY0)

---

## Production Infrastructure

The complete production environment consisted of:

- Green screen capture
- Multi-camera setup
- Wireless guitar system
- Wireless in-ear monitoring
- Unreal Engine rendering
- Automated scene management
- Voice control systems
- Live audience integrations

All systems operated simultaneously during live broadcasts, requiring continuous troubleshooting, optimization, and maintenance.

---

## Live Performance Highlights

The project received recognition from Kick due to its unique blend of music, storytelling, and technology.

Notable opportunities included:

- Attending DreamHack Atlanta as a Kick representative
- Performing original music at DreamHack Melbourne
- Performing on the Rod Laver Arena stage
- Performing at DreamHack Dallas
- Showcasing original albums and live visual productions

These events provided opportunities to present both the music and technical systems developed throughout the project.

---

## Outcome

Over its lifespan, Grym evolved from a solo music project into a large-scale creative and technical undertaking that combined:

- Music production
- Character performance
- Storytelling
- Livestream production
- Automation engineering
- Unreal Engine development
- Interactive audience systems

The project ultimately concluded before its narrative was completed due to the scale of development and long-term sustainability challenges.

Despite its unfinished story, Grym served as a successful exploration of how music, technology, automation, virtual worlds, and live audience participation could be combined into a single immersive experience.
