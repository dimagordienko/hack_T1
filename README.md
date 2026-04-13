# T1 Hackathon

# The Easiest Solution at the Hackathon!

## TOPIC — Optimization of Clinic Placement in the City of Seversk

**Team:** Suetolog

**Member:** Dmitrii Gordienko

---

## Task Description:

The main goal is to distribute clients between different clinics in the city in order to **minimize travel time** from home to the clinic.

**Input:** coordinates of clients
**Output:** coordinates of 250 clinics that are optimally placed in the city

---

## Evaluation Metrics:

There are internal **metrics** to evaluate the solution quality:

1. **Total Travel Time** — total time spent by all clients
2. **Clinics Overload** — how overloaded the clinics are
3. **Location Convenience Score** — average convenience rating of clinic locations

---

## Dataset Features:

The dataset includes the following **features**:

* **Feature 1:** Population density around a possible clinic location (`density_area`)
* **Feature 2:** Distance to existing clinics (`clinic_distance`)
* **Feature 3:** Age distribution of clients (`client_age`)
* **Feature 4:** Distance to the nearest park or green area (`park_distance`)
* **Feature 5:** Density of socially vulnerable groups (`vulnerable_group_density`)
* **Feature 6:** Social infrastructure rating (`social_infrastructure_rating`)

Each feature can influence clinic placement and affect the final result.

---

## Solution:

At first, it was difficult to understand where to start. I decided to begin with a simple approach — using the **K-means algorithm** to place clinics, and then slightly adjust their positions.

The solution is mostly **algebraic**, but it is also possible to solve this task by building a machine learning model.

---

## Fresh Look at the Data:

<img width="618" height="478" alt="Снимок экрана 2025-12-22 в 23 12 20" src="https://github.com/user-attachments/assets/2770405b-8de5-45ce-be55-e6cd0499a1d9" />

After performing clustering, I calculated the centroids for each cluster. For better visualization, I displayed them as coordinates:
<img width="600" height="479" alt="Снимок экрана 2025-12-22 в 23 13 50" src="https://github.com/user-attachments/assets/611d7c8f-681c-425d-943e-b494662da31c" />

This way, I got my first and simplest result! I decided not to stop there, saved the file, and moved on to implementing metrics to evaluate the solution.

I calculated the following metrics:

1. **Total Travel Time (TTT)**
2. **Clinics Overload (CO)**
3. **Location Convenience Score (LCS)**

---

## First Results:

* **TTT** — 2374.98
* **CO** — 0
* **LCS** — 42.393325

**Total score** — 2328
**Leaderboard** — 3rd place

---

## Stage 2

The next day, I decided to improve the solution.

The first step was to replace standard K-means with a median-based approach to reduce the impact of outliers (`mediana_same_ttt.ipynb`).

The second idea was to split the data into two large clusters (you can see them on the map), and then apply K-means manually (`two_clasters_2356.ipynb`).

These ideas sounded promising, and I expected some improvement. However, they did not give any better results, so I decided to keep the original solution to avoid making the code more complex.

Later, I noticed that my final score changed every time I ran the code. After checking the code, I realized that I did not set `random_state` in the K-means method.

This led to a new idea:

* If the result changes every time, and I can control it using `random_state`,
* then I can try multiple seeds and compare results,
* and finally choose the best one.

This is how the file `broutforcer.ipynb` appeared. I ran it overnight for about 7 hours and checked the results in the morning.

This method worked — the result improved by 11 points. The new **TTT** was **2344**.

At the same time, I continued testing other ideas.

---

## Stage 3 (`move_impovment.py`)

I iterated over each clinic and tried to slightly move its position:

* shift the clinic by **N** units
* recalculate the metrics
* check the result

If the result was worse, then reduce the step:
**N = N / 2**

Simple but effective.

In the end, I got a small improvement in the main metric (**TTT**).

---

## Final Results:

* **TTT** — 2335.55
* **CO** — 0
* **LCS** — 42.38

All project files are attached!
