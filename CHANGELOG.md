# RimThreaded changelog

One entry per build, newest first. Each build has a git tag (`git checkout build-NNN` shows exactly what it contained) and,
once published, the commit it has in the private mirror DrPeppere/rimworld-1.7-mods. "Tested" says on which game versions a
build was run and what came out. Details and measurements live in PERFORMANCE.md; mod bugs in MOD_ISSUES.md; this file is the
short "what changed and why" a later session reads first. Builds 1-104: `git log` and PERFORMANCE.md (build numbers are in the
commit messages).

## Build 144 (2026-11-15 14:38, tag build-144; cut automatically by cut-build.ps1 at the end of build 143's round)
- a525ab6 Merge branch 'feat/t55-draw'
- 131e367 Merge branch 'fix/t57-geyser'
- 58182e6 Merge branch 'feat/t56-pacing'
- d10c30e T55: draw cap off by default, round robin over dirty sections, one-time draw-cap log line
- 53b420e T57: flecks updated once per drawn frame at high speed (geyser wait behind the fleck update); fleck count in the profile
- 23b316d T55: opt-in frame profiler (-rtframeprofile, -rtframebaseline); draw cap never switched on (fixed)
- 7b24d16 T56: frame pacing at speeds 1-3 (frame-time budget for the tick loop, -rtframepacing=off), design in helpers/t56-pacing.md
- 0e7bf2f T51: room things kept - Room.ContainedAndAdjacentThings no longer builds a new set and list per ask
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 143 (2026-11-15 12:19, tag build-143; cut automatically by cut-build.ps1 at the end of build 142's round)
- 019ec03 Merge branch 'feat/searchhelp2'
- 5b6b1d1 T47: per-thread static scratch arrays (GasGrid.beqCells race), RTBench removes letters that wait for an answer
- df199ca Merge fix/t45-dobill into feat/searchhelp2: T45 tests kept read-only on a helper (HolderSafe for haul sources)
- 436ee4b Search help: Vanilla Traits Expanded bill prefix reviewed and listed; start line names every unreviewed patch
- bcee7ee T45: bill scan copy makes the same tests as the 1.7 game's WorkGiver_DoBill
- 23203ae T41 search help stage 1b: bills on helping workers, reviewed mod patches
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 142 (2026-11-15 08:50, tag build-142; cut automatically by cut-build.ps1 at the end of build 141's round)
- f589908 Room things field rule: the log names each file that names the field (mod, method count, path)
- ce9a724 Merge fix/davies (T40: a deferred job start is kept for a pawn already downed when given; a worker that placed a pawn starts its job at once; -rtdownedstart=off, -rtplacedstart=off, -rttracepawn=NAME)
- 30533dc T40: a job given to a downed pawn is started; a pawn just put on the map gets its job at once
- 034404a Merge feat/searchhelp (search help: owner worker calls PawnCanUseWorkGiver before publishing; helpers only scan)
- 2cc200a T41 search help: PawnCanUseWorkGiver is only called by the pawn's own worker
- 43f37bb Room things field rule: walk the module's method table by token (the type walk read 603 of 2825 DBH methods)
- dd3dd0a Merge feat/searchhelp (T41 search help stage 1a: idle workers scan the next work givers of a long job search; default off, -rtsearchhelp=on|check)
- 65416f4 T41 search help, stage 1a: idle workers scan the next work givers of a long job search
- 1408431 T42 haul check batch: the rolling haulables check asks its things on all workers, applies in the game's order
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 141 (2026-11-15 07:03, tag build-141; cut automatically by cut-build.ps1 at the end of build 140's round)
- 225381b Build 16b: room things field rule finds the DBH reader; T39 move guard long wait; build 16 rules default off
- f7ab786 Build 16: door pawn set, room stats once, recount things, held tick claim, pollution statics
- 3e7e35c Build 15: bill fast check, merge partner check, governor early stop, need timers
- 1c29544 Bill quick skip default off (b12 +1.5%, b13 +1.2%: under the 2% rule); managed as a lever
- 60198d5 Levers: fleck queue and room count hooks only when adaptive is report/on at start
- 5aef933 Adaptive phase 1: lever registry, governor with self A/B, modes, error link
- f5b7afc Profiler: time the steam geyser spray calls (sprayer tick, air puff, snow melt, sound)
- cdd5d1f Merge branch 'feat/billskip' into feat/findings
- 88a9d09 Adaptive phase 0: profile Findings section and always-on LiveStats
- 519aa01 Bill quick skip v2: forbidden/area, reserved and skill tests before the map walk
- e4f06e3 Bill quick skip: skip a bill work search no bill of which the pawn could start now
- bec7256 Bill-search probe: why bill ingredient searches fail (adaptive P0.3, owner-save T28)
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 140 (2026-11-15 01:18, tag build-140; cut automatically by cut-build.ps1 at the end of build 139's round)
- f60c454 Owner save: door reachability-clear memo (+6%), pawn move guard and baby-in-transit guard (Davies errors), unproven rules off by default
- 31aff44 Owner save speed: workers take any ready tick list (prep event never reset), turret range rule, races found by real parallelism
- 2738a2b STATE: owner 1.7-only order, OSB limiter findings, check-in 21:2x
- 44f75dc 1.6: CompIngredients scratch lists per thread (owner-game meal merge race); profiler 'stacks' request word: allocation call sites; OSB kit notes
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 139 (2026-11-14 07:17, tag build-139; cut automatically by cut-build.ps1 at the end of build 138's round)
- 38ad1b6 Jumbo guard: plant-work and hauling closest-first searches no longer index outside their grid
- What: RimThreaded's closest-first work searches (plant sow/harvest in JumboCell, hauling in HaulingCache) assumed a square map and kept a cache built for another map size. On a map wider than tall (or resized after the cache was built) every search threw IndexOutOfRange, so colonists stopped sowing/harvesting/hauling on that map. Now rows are checked against the row count, the cache is rebuilt when the map size changes, an index outside the grid is skipped and reported once. Off switch -rtnojumboguard. Once-lines contain "jumbo guard".
- Found: LT c18 b138 RT stopped (home map 400x100). Proof before the cut: main PC c01 RT with a 300x200 second map: build 138 = 320 IndexOutOfRange + run stopped; side build (same code as 139) = 0, autotest DONE, 36 plants sown, line "map 1 is not square (300 x 200) ... jumbo guard". The new gravship phase G1 (300x250 landing map) also hit it on 138.
- Tested: build-both BUILD_OK (1.7 2c855d617fc71339, 1.6 d1b8eb75795d938f). Round 139 = release-candidate round (replaces 138 as RC once clean).

## Build 138 (2026-11-13 08:32, tag build-138; cut automatically by cut-build.ps1 at the end of build 137's round)
- 09af442 Merge fix/billstack-nre: bill stack locks (BillStack writers atomic per stack, mod patches that change bill lists run under the stack lock, readers skip empty slots; -rtbillstacklocks=off). Proven 1.6 c16-150-5 x3 DONE 49/50/50, NRE gone
- eeeb357 Bill stack locks: bill lists stay whole under parallel job searches (-rtbillstacklocks=off)
- 7f794ce S41 scan cache part 2: class locks, component locks, main-thread guards
- 5cc06db S41 R13: start-up scan cache (mod scan + cache lock selection per mod assembly)
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 137 (2026-11-13 04:40, tag build-137; cut automatically by cut-build.ps1 at the end of build 136's round)
- c7c8179 O78: NullGuard reads guarded fields as volatile reads
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 136 (2026-11-13 00:37, tag build-136; cut automatically by cut-build.ps1 at the end of build 135's round)
- 5445f83 O77: one hediff add's part test, add and missing-part step run under the per-pawn health lock; a part another thread removed in the same tick is handled as 'that hit came first' (-rtnohediffaddlock)
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 135 (2026-11-12 20:54, tag build-135; cut automatically by cut-build.ps1 at the end of build 134's round)
- bbd43db Merge perf/slowpawn (S34 long-tick profiler rows, wealth recount warm-up on all workers): JH bench ForceRecount spikes 10/12 -> 2-3/12 profiles, 77 -> 53 ms, TPS unchanged
- 0fca834 HediffSet: every list loop reads one snapshot; cache builders one at a time per pawn (-rtnohediffsnap)
- 8f860e2 Wealth recount warm-up (S34): item and building values for a due colony wealth recount computed ahead on all workers; off: -rtnowealthwarm; profile row
- eae73a7 Tick profiler: longest thing per tick (S34) - kind, whose pawn, job, job search, top call, start offset, GC; summary row + two tables
- ca4165d Tick profiler: ticks over 16 ms by cause, longest ticks, worker idle cause row (R01, R03 measurement)
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 134 (2026-11-12 15:51, tag build-134; cut automatically by cut-build.ps1 at the end of build 133's round)
- 588d354 O71 faction leader replacement window, O72 quiet failed reservations of queued job starts
- f069a87 Job-gap rules, patched-frame attribution, burst stop
- ea105b8 O30: companion list locks - the list behind a mod's memo dictionary gets atomic calls (CacheLocks)
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 133 (2026-11-12 11:17, tag build-133; cut automatically by cut-build.ps1 at the end of build 132's round)
- e1be08e Merge fix/noduty-hive: lord duty trace for O64 (chain 27 clean: c19, c18, 1.6 c16-150-3)
- ce7d49e Merge fix/pathconsume (O63 path guard): proven chain 25 + JH raid x3 619f11c
- 69b8e5a Lord duty history: diagnosis line for lord members without a duty (-rtnodutytrace)
- f602679 Merge fix/lordfreepawn (lord/world pawn sync, proven chain 24)
- eb13246 Merge perf/profilerfix-s42b (S42b profiler GC/alloc read + FleckBatch closure, proven chain 22)
- fe50dff Path guard: a pooled PawnPath is released once; a pawn left holding a released path plans again (-rtnopathguard)
- 55b4d3d Lord sync: a member that left the map as a free world pawn is reported lost before lords tick
- 92e7825 S42b: profiler reads GC/allocation at window end before removing timers (Harmony unpatch garbage was counted); FleckBatch no closure per call. Lock stubs (S26 part) left on perf/allocsrc-s42 per DECISIONS 18
- 2c62292 Job read guard: mod code using pawn.CurJob right away gets a blank job, not null (O49)
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 132 (2026-11-12 04:13, tag build-132; cut automatically by cut-build.ps1 at the end of build 131's round)
- a85bbaf Merge branch 'fix/listerthings' into merge/b132-prep
- 982b345 Merge branch 'perf/auto-threads' into merge/b132-prep
- 59e3bfc Merge branch 'fix/offswitches' into merge/b132-prep
- c93b16a Merge branch 'fix/mountfinish' into merge/b132-prep
- f84748e Merge branch 'fix/destres' into merge/b132-prep
- 3216998 Merge branch 'fix/texturethread' into merge/b132-prep
- 21c89b1 Merge branch 'fix/ce-melee-height' into merge/b132-prep
- b6c3f35 S31: ListerThings.Add/Remove/Clear, IsFighting and OffsetForcedByJob run the vanilla code with edits
- 5e0a969 Off switches for four merged features (R11); worker thread list is always replaced, never changed in place (R12)
- 75f54f1 DeferGuard start-up line lists up to 60 guarded patch methods (was 12; Giddy-Up's was hidden behind '...' on 1.7 c10)
- ae32ddb DeferGuard: a queued kill or downing runs other mods' patches once, when it really runs
- 960c797 Unstarted deferred job starts give back their reservations (CE RunForCover destination leak); -rtnodestres
- 3f746ca Solid-colour errands: SolidColorMaterials textures/materials asked for by a worker are made by the main thread
- a59b072 Steady effects: serialize game condition list changes, fix deteriorate finalizer name match (-rtnosteadyfx)
- 54e11ef Borrowed pawn parts: mod methods that null a pawn's part and put it back do not do so while workers run
- 5bc9f1e S24: automatic worker count (CPU default + adaptive active count)
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 131 (2026-11-11 19:32, tag build-131; cut automatically by cut-build.ps1 at the end of build 130's round)
- a1da21a Merge perf/safelane-finer into release/b131
- 3db37c3 Merge perf/joygivers into release/b131
- 4e3a173 Merge perf/jobsearch into release/b131
- 7747810 Merge perf/ce-cover into release/b131
- be9b2b0 Merge perf/ce-suppress into release/b131
- 0893f0d Merge perf/fewer-locks into release/b131
- 1ed0caa Merge feat/idle-dilation into release/b131
- 09c3210 Merge feat/linked-pawns into release/b131
- 05efdf8 Merge feat/serial-part into release/b131
- 42107f2 Merge feat/mod-projectiles into release/b131
- c520fde Merge feat/mod-cache-locks into release/b131
- 4395bfe Merge fix/records-tick into release/b131
- 6ed2d3c Merge fix/worksettings-priority into release/b131
- 7dcd027 Lazy def workers are made on the main thread before the first tick (RecordWorker.ShouldMeasureTimeNow NRE on 1.6); off with -rtnodefworkerwarmup
- 4b9b4b9 S21: learned safe-lane lines from load/init failures no longer keep a kind serial; profile rows Learned list + Safe lane causes
- ce745ed S25: lock-free reads behind -rtnofewerlocks (apparel stats, GenTypes, DangerFor, goodwill)
- eacd0e5 S23: fires of a learned Fire def tick on workers between interval ticks; foreign Fire.Tick patches judged by PlainIL
- a3ab7f9 S10b: CE suppression holds the worn-apparel lock only for the gear copy
- 25c85e2 S14: time dilation for sleeping humanlikes, idle prisoners/slaves and parked mechs
- 8cef66d S13: recreation option that found nothing for a pawn is not searched again for 300 ticks (-rtnojoymemo); JobGiver_GetJoy chances per thread; profile row
- 58fe25c S07: CE shot-height memo per cast-position search + shoot lines shared between searches of a tick
- 2aa1d40 S12: work scan checks the work giver's own test before reachability in whole-list passes (-rtnoworkscanorder)
- fae34d9 Merge branch 'master' into feat/linked-pawns
- d71b9a0 Merge branch 'master' into feat/serial-part
- cd627f8 Merge branch 'master' into feat/mod-projectiles
- 21cffaa Merge branch 'master' into feat/replace-to-transpiler
- 8efc00b Work settings: make shared WorkGivers complete before a rebuild; name the cause of a short priorities table
- a119794 ReplaceToTranspile group 4: atomic ID counter, build-then-publish rule cache, per-thread scratch, timed lock run vanilla code
- 9a8e598 ReplaceToTranspile group 3: 37 copy-on-write, scratch-list, guard and lock replacements run vanilla code
- edc54fe ReplaceToTranspile group 2: ItemAvailability lock wraps, validator checks, TRANSPILE.md (group 2 done, direct Patch inventory, next groups)
- 5677956 Mod cache locks: new switch names, one log line per locked field / generic class, users in other classes, offline LockCheck tool
- 4cff0b6 ReplaceToTranspile group 2: 29 lock wraps and guards run vanilla code through transpilers
- 5b338f5 Slowest pawns first (-rtslowfirst=off) and an Explosions group in the profiler
- a3128a8 Mod projectiles: profiler timers no longer make projectiles serial; direct fleck creation and mote/effecter writes are plain; ILCheck tool
- e6f2b3a Convert the first 18 replacements: Archive, Messages, Thing.get_Map, HediffSet.Clear, SignalManager, SoundSizeAggregator, DynamicDrawManager, RegionLinkDatabase
- 7a92a70 ReplaceToTranspile: turn replacing prefixes into edits of the vanilla method, with fallback to the old replacement
- 85185b8 Linked pawns tick in one worker claim (mount + rider, lord members without a duty); -rtlinkedticks=off
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 130 (2026-11-11 04:37, tag build-130; cut automatically by cut-build.ps1 at the end of build 129's round)
- fdd1547 Verb list of a tracker is built completely before other threads can see it
- 482e692 Lord.RemovePawn keeps the duty of the pawn's current lord; no-duty diagnosis line
- Tested: build-both BUILD_OK (1.7 and 1.6); not run in a game yet. Proof runs: see each fix's helper log / STATE.

## Build 129 (2026-11-10 17:30, tag build-129; first build under the owner's "one build per full round" rule)
- Job-search objects' own collections are guarded (ModHazardScan, commit 22ead88, Fable helper log
  helpers/20261110-1720-inventory-loadout-race.md): the game makes ONE object per think-tree node, WorkGiverDef and JoyGiverDef,
  and every pawn's job search runs through it on several worker threads. Instance Dictionary/HashSet fields of mod classes
  derived from ThinkNode (JobGivers included), WorkGiver or JoyGiver now go to the cache locks (each call atomic), like static
  collections already did. Found by Compositable Loadouts (Wiri.compositableloadouts): ThinkNode_LoadoutRealisation's
  nextUpdateTick dictionary was corrupted by two pawns at once, then threw on every call ("Operations that change
  non-concurrent collections must have exclusive access", 133x, 1.6 c16-150-3 rt2 on 128; also 4-6x in rt runs on 125-127,
  never in a control). The mod-scan start-up line has a new count: "collections of mod think nodes / work givers / joy givers".
- Why now: build 128 finished its full round (every 1.7 c-batch 3 RT rows, every 1.6 list rt + nort) by 14:11.
- Tested: BUILD_OK (1.7 and 1.6). Proof due: 1.6 c16-150-3 rt on 129 without the LoadoutRealisation group and a non-zero new count.

## Build 128 (2026-11-10, tag build-128, local b887900, not published yet)
- THE MOD IS RENAMED: "RimThreaded Overclocked", packageId `drpepper.rimthreaded.overclocked` (was `majorhoff.rimthreaded`), author
  "DrPepper; original RimThreaded by Major Hoff". About.xml lists the old id as incompatible (the two must not run together); the
  settings page is "RimThreaded Overclocked". The Harmony ids stay `majorhoff.rimthreaded*` (other mods and the compat mod match on
  them). RimWorld's About.xml has NO alias for an old packageId (checked the fields of ModMetaData): a mod list or save made with
  the old id shows RimThreaded as missing until the new one is switched on once. Old id = documented alias in the test kit only.
- Map removal never runs on a worker (MapRemoval_Patch, STATE O54b, commit bbd7b28): a map parent that decides on a worker to remove
  its map hands the removal to the main thread. 127 crashed natively in a mod's MapRemoved (ComputeBuffer freed on a worker).
- Portraits asked for on a worker are made on the main thread (PortraitsCache_Patch, STATE O58, commit 95e7dec): the worker gets
  the cached texture, or a placeholder for that one frame, and the real portrait is rendered by a main-thread errand. 127 crashed
  natively in RenderTexture naming under a pawn's mood tick. New in 128: the placeholder is created at first use, not at patch
  time, and its field is typed `object`, so the game's start-up check no longer warns about a texture in a static field.
- Test kit (Generations repo tools/): both packageIds mean RimThreaded. The c-batch and 1.6 lists KEEP the old id (a list's hash
  is the key of its banked controls); gen-test.ps1 / gen-test16.ps1 rewrite the list at launch to the id the installed build has.
  CONTROL GUARD: a control run (new -Control switch, or a list named *-nort*) gets every RimThreaded entry removed and is stopped at
  once with "CONTROL GUARD FAILED" if RimThreaded loads anyway; an RT run in which RimThreaded never loaded ends with "RT GUARD
  FAILED". Neither is a result row (main-pc-queue.ps1 retries after 10 min). deps.py, run-batches.ps1, bank-control.ps1,
  run-chain.ps1, bisect16.py, bisect-run.sh, make-batches.py, make-big-lists.py know both ids.
- Tested: BUILD_OK (1.7 and 1.6). 1.6 (main-PC queue, c16-150, 2026-11-10 08:15): RT run autotest DONE, 38 errors (127: 41), the
  old-id list was rewritten to the new id and RimThreaded loaded, no start-up warning for PortraitsCache_Patch, no new error kind
  (the pawnkind-generation failures differ only in which kinds were sampled; no RimThreaded frame in them). Control 08:27:
  autotest DONE, 38 errors, RimThreaded not loaded. 1.7: built, not run yet (JH/LT kits must be updated first).

## Build 127 (2026-11-09, tag build-127, local 2f95276, published d125bbe)
- NotInSpace / InSpace stat conditions no longer throw (new SpaceStat_Patch, STATE O37). Vanilla InSpace.Applies does "if
  (thing.SpawnedOrAnyParentSpawned) thing.MapHeld.Tile": walking a broken holder chain throws, or ends without a map (JH c02 on 126:
  Big and Small's cache tick failed 2x on a dead, unspawned pawn, retry gave the same exception; control 0). Finalizers on both
  Applies methods: on a NullReferenceException InSpace answers false and NotInSpace true (as for any thing with no map). A call that
  works is untouched. Off with -rtnospacesafe. The root cause (which holder link is null) is still unknown: StatNullDiag's
  "holders=" now names each link before asking for its parent (it used to throw itself and print only the exception).
- Harness: phase-0 "space stat check" (pawn in a holder whose ParentHolder throws): FAIL on 126, pass on 127 (1.6).
  AutoTestPawnGenDiag logs who patches PawnGenerator.GenerateTraitsFor (JH: NREs in GenerateTraitsFor_Patch2 but no PAWNGEN line).
- Tested: 1.6 harness run on 127 passes the new check, no new errors. 1.7: JH c02 on 127 needed.

## Build 126 (2026-11-09, tag build-126, local 9cc3cc9, published ce8da8f)
- Section dirty flags are set under a lock (new MapMeshDirty_Patch, STATE O43). Vanilla MapDrawer.MapMeshDirty marks a section with
  "dirtyFlags |= flags" (and the drawer's globalDirtyFlags): a read-modify-write vanilla only does on the main thread. Workers mark
  sections too (glow, terrain, things, roofs in a raid or fire); two at once lose one's bit, and a layer whose bit is lost is never
  rebuilt - the owner saw a darker map rectangle exactly one section in size. Same logic as vanilla with every OR under a lock on
  that section. Off with -rtnodirtylock. NOT done: Section.TryUpdate clears dirtyFlags after rebuilding, so a bit marked
  in between is wiped (workers are normally idle then); a fix would clear only the bits it read.
- Harness: dirty bits check (16 threads mark one section with 16 different bits, 50 rounds); the render check's "dirty > 10 s" now
  counts a section only if it was not rebuilt (Section.TryUpdate) for 10 s - fires re-dirty sections every tick, the old check
  flagged those (false alarms in raid runs). RimThreaded's DrawCap never skipped a rebuild in 6 raid runs: not the cause.
- Tested: 1.6: dirty bits check 125 FAIL (1 of 16 bits lost by round 10), 126 pass x2 (one raid run); same error kinds as 125.
  1.7: pending (JH).

## Build 125 (2026-11-09, tag build-125, local 12eedad, published bdfdaf7)
- Combat Extended's ThingsTrackingModel (STATE O19): its writers were already locked per model, but its range queries
  (ThingsInRangeOf, ThingsNearSegment) are lazy iterators that walk the sorted array across yields with no lock while pawns moving
  on workers re-sort it (NullReferenceException in ThingsInRangeOf from a bullet's tick, LT b32), and CE marks DeRegister
  AggressiveInlining so its callers could inline it past the lock. Each query now runs to the end under the model's reader lock
  and returns a list (2 s bounded wait, then no things once, logged), and every CE call of Register / DeRegister /
  Notify_ThingPositionChanged goes through a wrapper that takes the writer lock (MethodLocker.InstanceLockOf, compiled callers).
- Tested: 1.6: ce16 with raids, 124 vs 125: both DONE, start-up line "writer calls locked in 3 CE methods", no
  LockRecursionException, no tracker errors, raid phase 1382 -> 1832 TPS, same other error lines. No harness check (needs CE).
  1.7: pending (JH, a CE batch).

## Build 124 (2026-11-09, tag build-124, local 4ff9905, published 999848d)
- Vanilla static scratch in two strict shapes is made per-thread by default (ModHazardScan; the broad by-use rule stays opt-in):
  (1) handed out: a private static collection that every method clears first, before any branch, and that a method returns to its
  caller (VerbUtility.ThingsToHit's cellThingsFiltered: two projectiles impacting on two workers indexed it while the other
  refilled it, IndexOutOfRange in Projectile.ImpactSomething, 1.6 raid run on 123); (2) a per-call stack: one method pushes
  (List.Add) and later pops (GenCollection.RemoveLast) it and nothing else removes from it (PawnGenerator.pawnsBeingGenerated:
  two generations on two workers popped each other's entries, ArgumentOutOfRange in TryGenerateNewPawnInternal, MechAssembler).
  38 fields on bis-18-37 (start-up line names them). A first version took 64 incl. persistent lists (Messages.liveMessages,
  PortraitsCache's texture pool: 486 OnGUI errors) and dirty-flag caches; both shapes were narrowed before release.
  Off with -rtnohandedscratch.
- Tested: 1.6: harness handed-out scratch check (16 threads x 200 ThingsToHit on own cells): 123 FAIL (other cells' things), 124
  pass x4; raid run DONE, no projectile / pawn generation errors, no OnGUI errors, same error lines as 123. 1.7: pending (JH).

## Build 123 (2026-11-09, tag build-123, local cac827a, published 368f084)
- HistoryEventsManager.RecordEvent (RimThreaded's replacement, STATE O20): the colonist records were trimmed with no lock (the
  original's lock never runs under the replacement), so two workers recording one event both passed "Count > maxRemembered" and
  the second RemoveRange got a negative count ("Non-negative number required", VME job-start postfix, JH c16 on 122, LT on 112).
  Copied from vanilla, customGoodwill was trimmed by ticksGame's count after ticksGame was trimmed (0), so it grew without bound
  and drifted from ticksGame. Now every write runs under one lock per manager, each record gets new lists (readers see a whole
  pair) and each list is trimmed by its own count.
- HaulingCache awaiting-hauling cells: Remove copied a cell's set with no lock while Add changed it in place under the set's lock
  (IndexOutOfRange in HashSet.CopyFrom inside Thing.DeSpawn, 699x in a 1.6 bis-18-37 run on 122; the despawn guard caught the
  half-despawned thing). Every user of a cell's set takes that set's lock (changes in place, readers copy under it); a new cell
  set is created once under the grid lock.
- Mods' own ContentFinder<T>.Get calls go to RimThreaded's main-thread handoff like vanilla call sites (GraphicErrands' mod
  scan; 119 call sites in the c16-150-2 list). O42 itself (RimPacts' emblem textures) was the harness's lazy-cache check calling a
  texture-loading getter from its own threads; the harness now skips such getters.
- Tested: 1.6: harness history events check 121/122 FAIL (customGoodwill 60 of 20), 123 pass x4 (16 threads x 50 records, no
  exception); mech clamor check (O41, vanilla mechs + sleeping lord, wake-up held back) 121 FAIL (3 jobs/mech/tick), 122/123
  pass; no HashSet copy errors in 4 runs on 123. A raid run (bis-18-37) showed two other vanilla static-list races, Projectile
  checkedCells and PawnGenerator.pawnsBeingGenerated (not touched by this build; next item). 1.7: pending (JH).

## Build 122 (2026-11-09, tag build-122, local 4d46ad6, published c5cb233)
- A clamor ends a pawn's job at most once per tick (new ClamorOnce_Patch, STATE O41). Vanilla Pawn.HearClamor ends a not-awake
  pawn's job (Harm, Construction, Ability, Impact) and notifies its lord; for a dormant mech cluster the lord's clamor transition
  wakes the mechs, so later clamors that tick do nothing. RimThreaded runs lord transitions asked for on a worker after the workers
  (Lord_Patch.DeferSignal), so the mechs stayed asleep for the rest of the tick and every Combat Extended impact clamor ended
  their job again: "Mech_Annihilator started 10 jobs in one tick" 41x (+13x Mech_BlackApocriton), TPS 478 vs 2229 without RT
  (JH c16 on 119). HearClamor's EndCurrentJob now runs once per pawn per tick; the lord notification still runs every time.
  Off with -rtnoclamoronce.
- Tested: 1.6: harness clamor once check (3 impact clamors in one tick on a colonist whose driver is marked asleep): 121 ends the
  job 3x (FAIL), 122 1x (pass) in 3 runs; ce16 with raids on 122 DONE, no '10 jobs' (no mech raid in that run); watch: one
  'Pawn_EquipmentTracker container tried to drop CE_FlareGun which it didn't contain' in that CE run. 1.7: pending (JH c16).

## Build 121 (2026-11-09, tag build-121, local b0bad45, published 80fa28b)
- Flood fills that throw no longer leave the filler "working" (STATE O39). Neither vanilla nor FloodFiller_Patch reset the flag
  when a passCheck or processor threw; a second non-worker thread that had picked the map's filler while it looked idle and waited
  on its lock then logged vanilla's "Nested FloodFill calls are not allowed" (JH c17 on 119, RT only). The fill now runs in
  try/finally; a filler still marked working when a fill takes its lock is noted once and reused. All four FloodFill overloads go
  through the patched one on 1.6 and 1.7 (no bypass).
- Realtime mote list calls go to the locked versions at every call site: vanilla RealtimeMoteList.MoteSpawned is one line and can
  be inlined into Mote.SpawnSetup, where the locking prefix never ran, so motes were added unlocked while MoteDespawned copied the
  list ("Exception ticking Mote_SparkThrown: Destination array was not long enough", 1.6 runs on 112, 116, 121; two unlocked adds
  leave a null slot = the 118 null mote). Callers rewritten at start-up: Mote.SpawnSetup, Mote.DeSpawn, Mote.Notify_MyMapRemoved,
  RealTime.Update (logged).
- Tested: 1.6: harness flood fill reset check (a fill whose processor throws): 120 FAIL, 121 pass x4; mote callers line present;
  no mote exceptions in 2 runs; same error lines as 120. 1.7: pending (JH).

## Build 120 (2026-11-09, tag build-120, local 1be9ffa, published 90e3daa)
- Mod LinkedList fields (new LinkedListLocks, STATE O38): every mod method (not constructors) that loads, stores or takes the
  address of a LinkedList<T> field, static or instance, in any class, runs under one lock per field (NestedMemoLocks' gate: 2 s
  on workers, 100 ms on the main thread, then unlocked once and logged). RimTalk walks each pawn's talk-request LinkedList node by
  node (First, Next, Remove(node)) from many methods; battle-log postfixes on several workers at once threw "The LinkedList node
  does not belong to current LinkedList" (JH c15 on 118). Per-call locks cannot cover a walk spanning calls. ILFieldScan rules can
  now gate methods (onMatch) instead of transpiling. Off with -rtnolinkedlistlocks.
- Tested: 1.6: harness phase-0 linked list race check (16 threads walking one LinkedList field, 20 rounds): 119 FAIL ('node does
  not belong'), 120 pass x2; start-up line: 7 methods (TickDelayScheduler.*); same error lines as 119. 1.7: JH c15 on 120: RimTalk LinkedList error 0 (118: 1), linked list race check passed.

## Build 119 (2026-11-09, tag build-119, local 10fe0ee, published e7da831)
- Half-spawned / half-despawned things are made whole (new DeSpawnGuard_Patch, STATE O37). Vanilla Thing.SpawnSetup marks a thing
  spawned before it adds it to map.spawnedThings, and Thing.DeSpawn removes it from there long before it marks it despawned; an
  exception in between (more likely on a worker) left a thing "Spawned" with no holder. For a pawn inside such a corpse,
  SpawnedOrAnyParentSpawned was true while MapHeld was null, and ConditionalStatAffecter_NotInSpace.Applies threw on every stat
  read (LT c02: Big and Small's cache tick on a dead Drifter with Odyssey's MoveSpeed_Space gene, RT 2x on 112 and 117, controls 0).
  Now a SpawnSetup that leaves the thing spawned without a holder gets it added to its map's things, and a DeSpawn that throws after
  the removal is finished (lister, grid, drawing, tickers, then marked despawned); first case per kind logged; exceptions still
  propagate. Off with -rtnodespawnguard.
- StatNullDiag's pawn description now includes the holder chain (each holder, spawned or not, and whether it has a holder).
- Tested: 1.6: harness despawn + spawn guard checks (forced failure inside DeSpawn / SpawnSetup on a steel stack): 118 FAIL both,
  119 pass both (3 runs for despawn, 1 for spawn), same error lines as 118 and the no-RT control. A probe read MoveSpeed of a
  MoveSpeed_Space pawn alive, dead in a spawned corpse, corpse despawned and destroyed: no exception with or without RT (so the
  NRE needs the half state). 1.7: pending (LT c02).

## Build 118 (2026-11-09, tag build-118, local 3d0e211, published d128d1f)
- New game / loaded save resets RimThreaded's own queues (new GameReset, STATE O36): deferred kills, cross-thread job changes,
  after-tick work, worker post-event actions, pawn overlay clears, safe lane things, hauling cache maps and RealTime.moteList drop
  the previous game's objects in the Game.InitNewGame / LoadGame prefix (ThreadStaticsGate.NewGame); what was dropped is logged.
  GameReset.Register adds more subsystems.
- RealtimeMoteList.MoteListUpdate loops over a snapshot taken under the list's lock and drops dead entries (null, destroyed,
  off-map). bis-18-37 on 117, harness L2 (second new game in one session): a null mote stuck in allMotes threw every frame
  (1 of 3 runs) and filled the game's 10,000-message log.
- Frame guard (new FrameGuard_Patch): exceptions in Game.UpdatePlay / Map.MapUpdate (main-thread frame update; the map is not
  drawn while one repeats) are counted, and the first stack per method and type goes through UnityEngine.Debug, which still
  reaches Player.log after the game's message limit. The exception still propagates.
- O36 itself (the owner's black map) is NOT RimThreaded: the harness's L2 new-game path draws a black map under a bright UI in
  vanilla too (bis-18-37 without RimThreaded 2/2, with -rtdrawcap=0 too). A DrawCap fairness change was tried and dropped.
- Tested: 1.6: bis-18-37 x2 'autotest DONE', no harness FAILs, same 8 error lines as the no-RT control (harness phase
  artifacts). 1.7: pending (test PC).

## Build 117 (2026-11-09, tag build-117, local 276fceb, published 78d358f)
- Fixes a build 116 regression on 1.7 (STATE O35, likely O34): InstanceScratch gave verb and ability lists a fresh list per call,
  but verb managers keep those lists between calls (MVCF, Combat Extended). JH c07 on 116: 6x MVCF.WorldComponent_MVCF tick NRE in
  RunAndGun's Verb_TryStartCastOn prefix (turret verb), 0 with -rtnoinstancescratch, 0 on 113-115; LT c04 on 116: 61x CE
  'Unable to find the weapon to be reloaded'. Now methods that return verb or ability lists (by method name or element type) are
  left alone; the start-up line names them. TraitSet.TraitsSorted (O29) stays covered.
- Tested: 1.6: dbh16 'autotest DONE', 0 scripted failures, instance scratch check passed. 1.7: JH c07 MVCF/RunAndGun 6 -> 0, instance scratch check passed;
  LT c04 CE reload 'weapon not found' 61 -> 0.

## Build 116 (2026-11-09, tag build-116, local 6d0757a, published 5ea8dad)
- Getters that hand out a per-object scratch collection give each call its own (new InstanceScratch, STATE O29). Vanilla's
  TraitSet.TraitsSorted cleared one instance list per pawn (tmpTraits), filled it and returned it; two threads asking about the
  same pawn cleared it under each other ("Collection was modified" in a Hauts Framework StatPart_Glow postfix, JH c09 on 114).
  RimThreaded's scratch rules covered static fields only. Rule, game and mod code: a private instance List/HashSet/Dictionary named
  tmp/temp/working/scratch, used by one method that clears it first and returns it, is replaced in that method by a fresh one per
  call. 17 methods on 1.6 (TraitsSorted, MapPawns.FactionsOnMap, HediffSet.GetHediffsVerbs, Pawn_AbilityTracker.AICastableAbilities,
  ...). Off with -rtnoinstancescratch.
- Harness: phase 0 instance scratch check (TraitsSorted twice must give two lists).
- Tested: 1.6: instance scratch check fails on 115 (same list twice) and passes on 116; dbh16 "autotest DONE" (0 scripted
  failures); c16-150 all phases DONE (tick 397k, 16 scripted failures, 115: 13); c16-150-3 without raids DONE. The main-PC queue's
  own c16-150 RT run on 115 was "autotest DONE" too (O18 confirmed). 1.7: JH c09 on 116: collmod 0/0, RT-only 0, instance scratch check passed (19 methods).

## Build 115 (2026-11-09, tag build-115, local 6cf28a8, published 534df50)
- A world pawn's tick counts as its own tick (STATE O18). The c16-150 1.6 list died natively in every RimThreaded run (ntdll access
  violation, no crash report, always around game tick 250-285k). Bisection: base + Deathpallcalypse (XML only: a shambler faction)
  + RimThreaded is enough; without RimThreaded it runs clean. Its shamblers are world pawns whose shambler timers run out around
  day 4. Their Pawn.Kill came from their own world tick on a worker, but world-pawn ticks did not set the own-tick mark, so
  DeferredKill postponed the death to after the tick; vanilla's health check saw a pawn that should be dead but was not and asked
  for the kill again - 369 times in one tick on one worker (harness kill watch) until the worker's stack ran out. Now world-pawn
  ticks and ticks of things inside containers set the mark (a death in its own tick happens at once, as for map things), and
  DeferredKill runs a kill at once on the third request for one pawn from one thread in one tick.
- Callers of mod methods that hand out a shared Dictionary/HashSet get atomic collection calls (new AccessorCacheLocks, STATE O26):
  an accessor is a small mod method returning a Dictionary or HashSet that reads a component field or a static and makes no
  collection itself. Smart Medicine's SmartMedicineGameComp.Settings() handed its per-pawn dictionary to StockUpSettings, which
  filled it from every worker's job search (LT c06 on 113: 134 NREs in StockUpIsFull, "ArgumentNullException key" on save). Off
  with -rtnoaccessorlocks.
- Harness (Generations): -autotestkillwatch, -autotestmainwatch, crash catcher names JIT methods on the crashing thread's stack
  (1.6), -autotestphase7ticks, -autotestraidstrategy (O28), '+' as a skip separator; the 1.6 harness now installs the start-up
  watches too (they only ran on 1.7 before).
- Tested: 1.6: c16-150 (159 mods, all phases incl. raids and L) "autotest DONE" to tick 400k - every earlier RimThreaded run of it
  died natively; base + Deathpallcalypse DONE to tick 326k (112/113/114 died at 243-275k; no-RT clean); the shambler's kill runs
  once. dbh16 DONE (0 scripted failures), Smart Medicine list DONE (0; 4 accessors, 14 callers locked). 1.7: builds; not run
  (needs LT c06 for O26).

## Build 114 (2026-11-09, tag build-114, local 95f4cf1, published 7edc751)
- Fixes build 113's world-generation regression (JH c03 on 1.7: trait generation NREs, "RandomElementByWeight with totalWeight=0" in
  Vanilla Social Interactions Expanded, "Error while generating a map"; fine on 112 and without RT). Cause: 113's O23 rule gave
  vanilla nested caches per-thread copies, but the same IL shape (look up, insert, fill the inner list) also builds an index once
  at load; a worker's fresh copy was empty. Now those fields stay shared and every method that touches one runs under one lock per
  field (new NestedMemoLocks; timed like ClassLocks, so it cannot stall). O23 (FoodUtility.ideoIngestThoughtsCache) stays covered.
  Off with -rtnovanillamemo.
- A stuck worker is never Thread.Abort-ed, also on 1.6 Mono: it is abandoned and replaced as on 1.7 (an abort is injected wherever
  the thread is, also into native code). The timeout message also goes through UnityEngine.Debug, so it reaches Player.log after
  the game's own log hit its message limit. (Investigated for STATE O18; not its cause.)
- Harness (Generations): vanilla memo check now checks the lock; -autotestskip=R skips the raids.
- Tested: 1.6: dbh16 "autotest DONE" (0 scripted failures; driver read, dissolved room, vanilla memo checks pass; 7 vanilla methods
  under nested cache locks), mp16 DONE (0 Map Preview RNG errors), c16-150-3 without raids DONE through every phase incl. L2/L3.
  c16-150 still dies natively at tick ~250-285k on 112/113/114 (STATE O18, open). 1.7: JH c03 x3 RT + control: 0 world-gen fatals, 0 NeedNewPath, RT-only 0, TPS back to 112 level; LT c14: non-concurrent 0 (O23 still fixed).

## Build 113 (2026-11-09, tag build-113, local b56b2c7, published ce4a8fc)
- Another pawn's job driver is read once (new DriverReads, STATE O21): every "jobs.curDriver" read directly followed by its
  ended / asleep / collideWithPawns (vanilla: GenHostility.GetPreyOfMyFaction, RestUtility.Awake, PawnBlockedBy, PawnBlockingPathAt,
  and the same pattern in mod code) becomes one null-safe call. Why: those methods check the other pawn's CurJob or curDriver and
  then read curDriver again; that pawn's own worker can end the job in between (JH c13: NRE in IsPredatorHostileTo inside
  EnemiesAreNearby). Off with -rtnodriverreads.
- Mod code that reads or writes Rand's state fields directly uses the per-thread state too (STATE O16): Map Preview's
  Map.FillComponents prefix read the stale shared Rand.iterations and logged "vanilla map components have modified the RNG state".
  Both rules run in one new start-up pass over game and mod IL (ILFieldScan: raw IL bytes, field tokens resolved once per module;
  ~160 ms on a small list).
- Vanilla nested memo caches are per thread (STATE O23): a private static Dictionary whose values are collections, created in the
  static constructor and afterwards only looked up and filled (never cleared, removed from or replaced), gets one copy per thread
  (7 fields on 1.6, among them FoodUtility.ideoIngestThoughtsCache). Why: every food search on the workers filled its outer and inner
  dictionaries at once and corrupted them (LT c14: 162x "Operations that change non-concurrent collections" in AddThoughtsFromIdeo).
  Flat memos stay shared (materials and designators have identity; giving them atomic calls broke RealtimeMoteList). Off with
  -rtnovanillamemo.
- A room whose map is gone is not updated (STATE O22): Room.UpdateRoomStatsAndRole skips a room whose Map is null (no districts
  left, or a district with map index -1), inside RoomDistrictLock. Why: a worker updated such a room's stats from a wound tale and
  Dubs Bad Hygiene's cleanliness postfix threw in DubUtils.Hygiene(null) (JH c15).
- Quarantine also moves things that keep throwing with only vanilla code on the stack (STATE O18): from the third worker throw (at
  once for a spawned pawn without a pather) the thing ticks on the main thread for a game hour; the error is still logged. Why: a
  mod comp threw in a raider's SpawnSetup (HAR AlienComp on PMP_PersonaMechanoid, also without RT) before vanilla gave it a pather,
  and vanilla's Pawn.Tick then threw on a worker every tick. (Not the cause of the c16-150 native exits: see STATE O18.)
- New harness checks (Generations): phase 0 driver read, dissolved room and vanilla memo checks; -autotestnrestress, -autotestnolazyrace,
  crash catcher (ntdll access violations: thread, stack alignment, return addresses), deconstruct watch, thread ids in heartbeats.
- Tested: 1.6: each new check fails on 112 and passes on 113: driver read (GetPreyOfMyFaction NRE on 112), dissolved room (NRE
  on 112 with DBH), vanilla memo (112: another thread filled the shared ideoIngestThoughtsCache), Map Preview mp16 (8 RNG-state
  errors on 112, 0 on 113, 0 without RT). dbh16 and mp16 on 113 "autotest DONE". NRE stress (20 pather-less pawns, 300 s) survives
  on 112, 113 and without RT; 113 moves those pawns to the main thread at once. c16-150 still dies natively in phase 7 on 113 as on
  112 (STATE O18, open). 1.7: builds; not run.

## Build 112 (2026-11-08, tag build-112, local 7210a33, published 87d7e38)
- Patched methods keep their own assembly (new KeepCallerAssembly, STATE O2): every method RimThreaded patched whose original IL
  calls Harmony's parameterless PatchAll()/PatchAllUncategorized(), PatchCategory(string), or Assembly.GetExecutingAssembly() gets
  one more transpiler that names the original method's assembly. Why: those calls find the assembly from the running method or the
  calling frame; a Harmony-rewritten method on 1.7 (CoreCLR) has no declaring type: "No Sympathy For Prisoners" Mod.Init (rewritten
  by cache locks for a static-list AddRange) died in Harmony.PatchAll with a NullReferenceException and none of its patches applied
  (JH big-1000 on 111). On 1.6 Mono keeps the owner type, so nothing broke there. Off with -rtnokeepcallerassembly.
- New harness checks (Generations): phase 0 "harmony patches applied" (a mod assembly with [HarmonyPatch] classes and no active
  patch fails) and an assembly probe (a method RimThreaded rewrites calls PatchAll/PatchCategory and GetExecutingAssembly).
- Tested: 1.6: builds, rule applies (probe method rewritten and kept), probe/patch checks pass on 111 and 112 (1.6 never broke);
  No Sympathy For Prisoners list loads with all its patches. 1.7: known-bad check passed on LT (No Sympathy For Prisoners: 111 patches never applied + Init_Patch1 NRE, 112 clean, start-up line names Mod.Init); JH c07 control fails the probe, RT 112 passes.

## Build 111 (2026-11-08, tag build-111, local c40baa0, published 4a0135c)
- World pawn clean-up (WorldPawnGC) runs after the workers on the main thread (MainThreadPostTick) instead of inside the world pawns'
  prepare step, which a worker ran while every pawn ticked. Its pass reads colonists' relations and memories and then discards
  the world pawns nobody keeps; vanilla never overlaps it with pawn ticks (RimThreaded's own soak NRE from a cancel landing mid-pass,
  2026-11-07, was one symptom). Not the cause of O10: those save warnings also come without RimThreaded (STATE).
- Compatibility code for a mod that is not installed (CE's EDShields callbacks without ED-Shields) is skipped silently by
  LazyCacheLocks, ClassLocks, ModThreadGuards and GraphicErrands, as CacheLocks already did (1.7 b18/b30 showed 4 warnings with stacks).
- Tested: 1.6 dbh16 x5 with RT (GC after workers) and c16-150-3 all phases ("autotest DONE", 348 errors, level of 109/110);
  1.7: builds; not run.

## Build 110 (2026-11-08, tag build-110, local 000a14c, published 61901d6)
- Lazy caches published before they are filled (new LazyCacheLocks, STATE O13): a mod method that stores a new collection into a
  static field and then reads that field again ("_c = new HashSet(); fill; return _c") runs under one lock per field until a run
  has finished; afterwards calls skip the lock while the field still holds what that run built. Workers wait up to 2 s (a first
  build can load graphics), the main thread 100 ms; a timeout runs unlocked once and is logged. Fields: every shared static
  collection of mod code (new ModHazardScan.sharedCollectionFields). Off with -rtnolazycachelocks.
  Why: Dubs Bad Hygiene's DefExtensions.FixtureDefs was built from parallel hygiene job searches; once in four 1.6 runs a null def
  stayed in the set and every fixture search threw "Invalid ThingRequest" (4,237 errors).
- CacheLocks: a getter that also stores its cache field (lazy init) is no longer skipped as "only hands the collection out";
  its Adds are atomic too (DBH's FixtureDefs getter had none).
- New autotest check (harness, phase 0, RimThreaded loaded): each mod getter of that shape is reset and called from 16 threads at
  once, 100 times; null entries, a wrong count or an exception fail. Build 109: DBH FixtureDefs "a null entry in the cache",
  SaunaDefs "4 entries instead of 2"; this build: 0 of 2 (dbh16) and 0 of 12 (c16-150-3, incl. Humanoid Alien Races'
  UniversalBodyAddons, which needed the wider field list).
- Tested: 1.6 c16-150-3 all phases, no crash, 0 "Invalid ThingRequest", no lock timeouts (60 methods / 57 fields locked); dbh16
  clean (6 methods). 1.7: builds; not run.

## Build 109 (2026-11-08, tag build-109, local d2e3a95 (source in d93cb25), published 30ef658)
- The old ContentFinder<Texture2D>.Get prefix is gone (STATE O12). Why: on 1.6, Mono compiles ContentFinder<T>.Get once for every
  reference T, so the prefix also ran for ContentFinder<Material>/<AudioClip> and, on a worker, handed back a Texture2D where a
  Material was expected (same family as O11). ContentFinder_Patch<T> already redirects every ContentFinder<X>.Get call site per X,
  which cannot mix up types; on 1.7 the prefix had no effect anyway.
- Tested: 1.6 c16-150-3 all phases, no crash, 0 "resource from a different thread"/"MatFrom null" errors (so nothing relied on the
  prefix), 0 container-type fails; RT-only groups vs control: O10 null pawn keys and spouse-relation NREs, one VEF projectile
  Spark index race (also seen on 107). dbh16: 0 errors. 1.7: builds; not run.

## Build 108 (2026-11-08, tag build-108, local c25f1aa, published a0bf48d)
- 1.6: ThingOwner<Thing>.Remove's copy-on-write copies the inner list as its own runtime type (CopyListKeepingType). Why: Mono
  compiles ThingOwner<T>.Remove once for every reference T, so the transpiler written for ThingOwner<Thing> also ran for
  ThingOwner<Apparel>, ThingOwner<ThingWithComps>...; its "new List<Thing>(innerList)" stored a List<Thing> in their typed field.
  Vanilla mostly got away with it, but Layered Apparel reads WornApparel as IReadOnlyList<Apparel> and the interface call landed
  in the wrong code: RimWorld 1.6 crashed natively (no exception, crash code 0xE0000001) the first time a pawn's apparel was
  removed (c16-150-3 at map generation, STATE O11). Same family as the 1.7 note in ThingOwnerThing_Patch (where the patch is off).
  Not a 107 regression: every 1.6 run that loaded RimThreaded crashed on that list; the "clean 106" runs had not loaded it.
- Includes 713bb73 (opt-in -rtrebuildcallees, off by default).
- New autotest check (harness, Generations repo): every heartbeat, each pawn's apparel/equipment/inventory container must hold a
  List<T> of its own T; on the unfixed build it flags "ThingOwner<ThingWithComps> holds a List<Thing>" in a 10-mod run.
- Tested: 1.6 c16-150-3 (159 mods): all phases incl. B/U/L in 7 min, no crash, 3 RT-only error groups vs control (null pawn keys at
  load = O10, one grammar, one EntitySwarm NRE); la16 (Layered Apparel only): crash before, clean now; dbh16: 0 errors, 0 DBH,
  0 container fails. 1.7: builds (the fix is in 1.6-only code); not run on 1.7 yet.

## Build 107 (2026-11-08, tag build-107, local 2967134, published 0a43ff2)
- Per-thread copies of mods' "current" fields (mod-scan "per-thread (current)", e.g. DBH/Rimatomics/Rimefeller `loccachecomp`,
  VEF `curPawn`) are cleared on every thread when a game starts or a save loads (ThreadStaticsGate game counter, prefixes on
  Game.InitNewGame/LoadGame). Why: the owner started 4 games in one session; DBH's constructor clears its static (constructor
  stores stay vanilla) but not the per-thread copies, the new map had the same uniqueID, so DBH used the previous game's
  torn-down map: NullReferenceException in GenGrid.InBounds every frame, latrines and toilet search broken.
- Finalizers that pass an exception on (28 places) store its stack first (RtExceptions.Keep): Harmony's rethrow had wiped every
  stack below the patched method, which hid the cause of the laptop's "non-concurrent collections" errors.
- Tested: 1.7 owner's game loads (141 rebuilt); desktop b07-b11: 0 freezes, 0 scripted fails, 2 small RT-only groups, no
  duplicate hediff ids. Not yet run on 1.6.

## Build 106 (2026-11-08, tag build-106, local 22e2e7c, published 08e5e56)
- Cache locks also cover vanilla helpers handed a cached collection (GenCollection.AddRange on a HashSet, AddDistinct on a
  Dictionary) and HashSet UnionWith/ExceptWith/IntersectWith/RemoveWhere. Why: Hospitality refills its PresentGuests set with
  Clear + GenCollection.AddRange while workers call IsGuest: "Operations that change non-concurrent collections" (laptop b17,
  353 errors in b18).
- Room.Fogged uses the first region that still owns a cell (a region the rebuild just emptied logged "Couldn't find any cell").
- Tested: 1.7 laptop: b18 0 RT-only groups (353 errors on 105), b32/b33 0 RT-only, b30 DMS fails = world-faction randomness
  (58 without RT). Not run on 1.6.

## Build 105 (2026-11-08, tag build-105, local 1d5f8e2, published dbd3d35)
- PatchWrapperRefresh (last start-up step): every patched method whose mod prefix/postfix/finalizer RimThreaded rewrote gets its
  Harmony code rebuilt. Why: Mono/CoreCLR inline tiny patch methods into Harmony's generated code before RimThreaded rewrites
  them, so per-thread "current" fields were never cleared: VEF GetMeleeVerb 8,000+ NREs and a raid freeze (1.6 c16-150-2).
- Tested: 1.6 c16-150-2: GetMeleeVerb errors 8,000+ -> 0, no freeze (192 methods rebuilt, 2.2 s). 1.7 laptop: 149 rebuilt, b17
  no RimThreaded-only errors.

## Build 104x (2026-11-08 morning, af09a55)
- 1.6: map-component check skips assemblies that reference no game/mod assembly (NAudio native crash); GenTypes lookup caches
  locked (Hospitality "same key" in GetTypeInAnyAssembly); per-method crash guard.
