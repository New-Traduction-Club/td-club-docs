# Persistent Variables Reference

This page summarizes high-impact `persistent` variables used by the mod.

It is not a full dump of every variable in the project, but a practical reference for contributors and submodders.

---

## Core profile and progression

Primary source: `game/core/definitions.rpy`

* `persistent.playername`: Player name.
* `persistent._fae_sayori_nickname`: Current Sayori nickname.
* `persistent.fae_intro_complete`: Intro completion gate.
* `persistent.fae_disclaimer_seen`: Disclaimer acceptance state.
* `persistent.fae_first_visit_date`: First visit timestamp.
* `persistent.fae_last_visit_date`: Last visit timestamp.
* `persistent.fae_visit_counter`: Visit count.
* `persistent.first_run`: First-run flow flag (`game/core/script-ch30.rpy`).

---

## Dialogue databases

Sources: `game/dialogs/*.rpy`

Each system keeps a dictionary/list in persistent:

* `persistent._chat_db`
* `persistent._greet_db`
* `persistent._farewell_db`
* `persistent._event_db`
* `persistent._mood_db`
* `persistent._flatter_db`
* `persistent._regret_db`
* `persistent._fae_fun_facts_db`
* `persistent._event_list` (queued events/topics)

---

## Affection system

Primary source: `game/dialogs/script-affection.rpy`

* `persistent.affection`
* `persistent.affection_day_gain`
* `persistent.affection_reset_date`
* `persistent._affection_daily_bypasses`

Related runtime/flow variables used by affection-dependent logic:

* `persistent._fae_absence_time` (computed from last visit)
* `persistent._fae_player_confession_accepted` (checked by affection cap logic)

---

## Gifting

Primary source: `game/core/new_gifting_core.rpy`

* `persistent.js_gift_log`: Gift receive counters by filename.

Common unlock flags from registrations (`game/dialogs/gifting-implementation.rpy`):

* `persistent.js_gift_cookies_unlocked`
* `persistent.js_gift_otter_unlocked`

Other gift-related state currently used:

* `persistent.js_gifts_otter`

---

## Rooms / backgrounds

Primary source: `game/additional/bgs.rpy`

* `persistent._present_room`: Current room id.
* `persistent.fae_sunup`
* `persistent.fae_sundown`
* `persistent.fae_moonup`
* `persistent.js_bgs_change_seen` (tutorial flag in topic flow, set in `game/dialogs/script-topics.rpy`)

---

## Outfits and wearables

Primary source: `game/core/new_outfits.rpy`

Registry and save-state:

* `persistent.fae_outfit_list`
* `persistent.fae_wearable_list`
* `persistent.fae_outfit_quit`
* `persistent.fae_custom_outfits`
* `persistent.fae_sayori_auto_outfit_change_enabled`

Current selected pieces:

* `persistent.sayo_hairstyle`
* `persistent.sayo_clothes`
* `persistent.sayo_accessory`
* `persistent.sayo_eyewear`
* `persistent.sayo_headgear`
* `persistent.sayo_necklace`

---

## Minigames

Sources:

* `game/core/mg_core.rpy` (new hub)
* `game/additional/game-handler.rpy` (legacy structures)

Main variables:

* `persistent.mg_registry` (new minigame registry metadata)
* `persistent.games_reset_redo` (legacy list still present)
* `persistent._fae_game_db`
* `persistent._fae_mg_list`

---

## UI and player preferences

Sources: `game/core/screens.rpy`, `game/core/styles.rpy`, `game/core/gui.rpy`, `game/core/preferences.rpy`, `game/additional/*`

* `persistent.animate_room`
* `persistent._fae_dark_mode_enabled`
* `persistent.use_alt_font`
* `persistent._fae_weather_setting`
* `persistent._fae_notifs_enabled`
* `persistent._fae_notif_sounds`
* `persistent.fae_player_music_allowed`
* `persistent.fae_player_music_explained`

Random-chat settings (`game/core/utilities.rpy`):

* `persistent._fae_random_chat_freq`
* `persistent.fae_random_chat_rate`
* `persistent.fae_repeat_chat`

---

## Music player state

Primary source: `game/core/custom_music_player.rpy`

* `persistent.js_music_player_tutorial_seen`
* `persistent.music_playlist`
* `persistent.current_song_index`
* `persistent.music_is_playing`

---

## Contributor note

When adding new persistent fields:

* prefer clear, namespaced names (for example `js_` or `_fae_` conventions used in this codebase),
* initialize with `default persistent.<name> = ...` when possible,
* avoid silently changing semantics of existing keys (migration-safe changes only).
