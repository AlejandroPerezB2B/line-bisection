# Line Bisection Experiment

## Overview

This repository contains a MATLAB implementation of a computerized line bisection experiment designed to investigate whether performing a perceptual task alone or in the simultaneous presence of another person alters perceptual processing.

The experiment includes two experimental conditions:

1. **Individual condition**  
   Participants perform the task alone inside an isolated laboratory cubicle.

2. **Shared condition**  
   Two participants perform the exact same task simultaneously while seated side by side using interconnected laptops.

The perceptual task itself is identical across conditions. The critical manipulation concerns whether the task is performed:
- in isolation,
- or in a shared perceptual environment.

The experiment was designed to explore how commonly perceived environments may influence:
- spatial attention,
- perceptual organization,
- and potentially low-level perceptual processing.

---

# Experimental Task

Participants are presented with:
- a horizontal white line,
- displayed centrally on a black background,
- intersected by a short vertical tick mark.

Participants must estimate where the tick is located along the line.

The response scale is:

```text
-1000 -------------------- 0 -------------------- +1000
```

where:
- `-1000` corresponds to the far-left end of the line,
- `0` corresponds to the exact center,
- `+1000` corresponds to the far-right end.

Participants type their estimate directly using the keyboard and confirm the response by pressing `ENTER`.

Example valid responses:

```text
-350
+420
+0
```

---

# Trial Structure

- 73 equally spaced tick positions
- ranging from `-900` to `+900`
- each repeated twice
- total: 146 trials

Two fixed pseudorandom trial orders are generated:
- one for the individual condition,
- one for the shared condition.

All participants receive exactly the same order within each condition.

---

# Timing

The task is self-paced.

Before each trial participants see:

```text
Press SPACE to start
```

Only the spacebar initiates the next trial.

After a valid response:
- a black screen appears,
- with a random inter-trial interval between 300–500 ms.

---

# Recorded Variables

For each trial the experiment records:

- participant ID
- condition
- trial number
- true tick position
- participant response
- estimation error
- RT_firstKey
- RT_enter
- editingTime
- timestamp
- participant triggering next trial (shared condition)

---

# Folder Structure

The experiment automatically creates a `data/` folder where all `.csv` output files are stored.

---

# Requirements

## Hardware

- Two laptops
- Ethernet cable
- Keyboards

## Software

- MATLAB installed on both laptops
- Windows 11 recommended

No Psychtoolbox is required for this version.

---

# Required MATLAB Files

The experiment folder should contain:

```text
create_line_bisection_files.m
make_trial_orders.m
run_line_bisection_individual.m
run_line_bisection_shared_host.m
run_line_bisection_shared_client.m
lb_draw_trial.m
lb_get_response.m
lb_save_row.m
```

---

# Initial Setup (steps 1 to 3 to be run only once, to generate the files needed)

## 1. Open MATLAB

On both laptops:

```matlab
cd('path_to_experiment_folder')
addpath(genpath(pwd))
```

---

## 2. Generate experiment files

Run:

```matlab
create_line_bisection_files
```

---

## 3. Generate fixed trial orders

Run:

```matlab
make_trial_orders
```

This creates:

```text
trial_orders.mat
```

containing:
- fixed order for individual condition,
- fixed order for shared condition.

---

# Running the Individual Condition

Run:

```matlab
run_line_bisection_individual('dyad001_A')
```

or:

```matlab
run_line_bisection_individual('dyad001_B')
```

The program automatically:
- creates the `data/` folder if needed,
- saves responses after every trial,
- appends data trial-by-trial to a `.csv` file.

---

# Shared Condition Setup

In the shared condition:
- two participants sit side by side,
- each using their own laptop,
- performing the exact same task simultaneously.

Participants:
- know they are performing the same task,
- but cannot see each other's responses.

One computer acts as:

- **HOST**
- the other as **CLIENT**

---

# Connecting the Two Laptops

## Step 1 — Connect Ethernet cable

Connect the two laptops directly using an Ethernet cable.

---

## Step 2 — Disable Wi-Fi

On both laptops:

```text
Settings → Network & Internet → Wi-Fi → Off
```

This prevents routing conflicts.

---

# Configure Static IPv4 Addresses

## HOST computer

Go to:

```text
Settings
→ Network & Internet
→ Advanced network settings
→ More network adapter options
```

Right-click:

```text
Ethernet → Properties
```

Select:

```text
Internet Protocol Version 4 (TCP/IPv4)
```

Click:

```text
Properties
```

Select:

```text
Use the following IP address
```

Enter:

```text
IP address:     192.168.10.1
Subnet mask:    255.255.255.0
Gateway:        leave empty
```

---

## CLIENT computer

Repeat the same process.

Enter:

```text
IP address:     192.168.10.2
Subnet mask:    255.255.255.0
Gateway:        leave empty
```

---

# Test the Connection

On the CLIENT computer:

Open Command Prompt and type:

```bat
ping 192.168.10.1
```

If successful you should see:

```text
Reply from 192.168.10.1
```

If not:
- check cable connection,
- check IP configuration,
- ensure Wi-Fi is disabled,
- ensure Windows Firewall is not blocking MATLAB.

---

# Running the Shared Condition

## HOST

Run first:

```matlab
addpath(genpath(pwd))

run_line_bisection_shared_host( ...
    'dyad001', ...
    'dyad001_A', ...
    50000)
```

---

## CLIENT

Run second:

```matlab
addpath(genpath(pwd))

run_line_bisection_shared_client( ...
    'dyad001', ...
    'dyad001_B', ...
    '192.168.10.1', ...
    50000)
```

---

# Shared Condition Logic

Both participants:
- see exactly the same stimulus,
- at exactly the same moment,
- on every trial.

Responses remain private.

Participants cannot:
- communicate,
- view partner responses,
- or modify partner timing directly.

---

# Trial Coordination

After both participants submit valid responses:
- the next trial remains blocked,
- until one participant presses the spacebar.

When either participant presses `SPACE`:
- the next stimulus appears simultaneously on both laptops.

The system records:
- which participant initiated the trial:
  - `HOST`
  - `CLIENT`

---

# Output Files

## HOST saves

```text
data/dyad001_A_shared.csv
data/dyad001_shared_sync.csv
```

## CLIENT saves

```text
data/dyad001_B_shared.csv
```

---

# Practical Recommendations

Before collecting real data:

- perform a full pilot session,
- test synchronization,
- verify Ethernet connection,
- verify file saving,
- verify trial progression.

Recommended order:

1. Turn on both laptops
2. Connect Ethernet cable
3. Disable Wi-Fi
4. Verify `ping`
5. Open MATLAB
6. Run HOST
7. Run CLIENT

Important:
- always start HOST first,
- do not close MATLAB during acquisition,
- backup `.csv` files after each session.

---

# Notes

The shared condition was designed to create:
- minimal interpersonal coordination,
- while preserving independent responding.

Participants:
- perform the same task,
- share the same temporal structure,
- but remain perceptually and behaviorally independent regarding their responses.
