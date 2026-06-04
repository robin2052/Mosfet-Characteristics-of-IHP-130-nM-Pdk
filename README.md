# Mosfet-Characteristics-of-IHP-130-nM-Pdk


## Id VsL 
<img width="992" height="634" alt="image" src="https://github.com/user-attachments/assets/b1d71ccf-2314-4b54-bc69-6a667c8c1644" />

What I am observing in the $I_d$ vs. $L$ curve (where drain current increases as channel length increases from $130\text{ nm}$ to around $336\text{ nm}$ before finally decreasing) is a classic short-channel phenomenon known as the **Reverse Short-Channel Effect (RSCE)**.

In long-channel, textbook transistors, $I_d$ is inversely proportional to $L$ ($I_d \propto 1/L$), meaning current should immediately drop as $L$ increases. However, at $130\text{ nm}$ and similar deep-submicron nodes, non-uniform doping Profiles completely change this behavior.

Here is exactly why this happens:

---

## 1. Halo / Pocket Implants (The Root Cause)

To combat Severe Short-Channel Effects (SCE) like punch-through and Drain-Induced Barrier Lowering (DIBL) at the minimum channel length ($130\text{ nm}$), foundry PDKs implement **halo (or pocket) implants**. These are highly doped regions of the same dopant type as the substrate (e.g., p-type for an nMOS) implanted right at the edges of the source and drain junctions.

## 2. Why $I_d$ Increases from $130\text{ nm}$ to $336\text{ nm}$

* **At $130\text{ nm}$ (Minimum $L$):** The halo implants from the source and drain sides overlap significantly in the middle of the short channel. This heavily increases the net doping concentration ($N_{sub}$) across the entire channel. A higher $N_{sub}$ causes the threshold voltage ($V_{th}$) to spike significantly. Because $V_{th}$ is high, the overdrive voltage $(V_{gs} - V_{th})$ is smaller, which **suppresses the drain current ($I_d$)**.
* **Moving toward $336\text{ nm}$:** As you increase $L$, the two halo regions begin to separate. The middle of the channel returns to the lower, nominal baseline substrate doping. Because the average channel doping drops, **$V_{th}$ decreases** (a phenomenon called **$V_{th}$ roll-up**).
* **The Result:** The drop in $V_{th}$ increases your overdrive voltage $(V_{gs} - V_{th})$ so rapidly that it temporarily overpowers the $1/L$ geometric degradation. Consequently, $I_d$ increases as you scale $L$ up toward $336\text{ nm}$.

## 3. Why $I_d$ Decreases After $336\text{ nm}$

* **Beyond $336\text{ nm}$:** Once the channel length becomes long enough, the halo implants become negligible, confined strictly to the edges. The threshold voltage plateaus and becomes constant because the bulk of the channel experiences a uniform, nominal doping concentration.
* **The Result:** With $V_{th}$ stabilized, standard long-channel physics takes over again. The geometric effect ($I_d \propto 1/L$) becomes the dominant factor, causing the drain current to steadily decrease as $L$ grows larger.

---

> ### Summary
> 
> 
> The peak around $336\text{ nm}$ represents the transition point where the **Reverse Short-Channel Effect ($V_{th}$ roll-up)** stops dominating the transistor behavior, and standard **long-channel geometric scaling ($1/L$)** takes back control.

