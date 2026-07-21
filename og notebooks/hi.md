I’m reviewing the calculation path in the attached method and will explain it step by step in plain language.

The final HI is computed as a cumulative degradation score that starts at 1 and decreases as the system appears to worsen.

Here is the full flow:

1. Baseline and test data are separated
- The first part of the data, up to train_size, is treated as the “normal” or healthy baseline.
- The remaining rows are treated as test samples.

2. A distance is computed for each test sample
- The method compares each test sample to the average of the baseline samples.
- If cumulative_method is "euclid", it uses Euclidean distance.
- Otherwise, it uses Mahalanobis distance, which also accounts for the covariance structure of the baseline data.

So for each test sample $i$, a value called raw_hi[i] is produced:
- For Euclidean:
  $$
  raw\_hi[i] = \|x_i - \mu\|
  $$
  where $\mu$ is the mean of the baseline data.
- For Mahalanobis:
  $$
  raw\_hi[i] = D_M(x_i, \mu, \Sigma^{-1})
  $$

3. The change from one sample to the next is measured
- The code then computes the absolute difference between consecutive distance values:
  $$
  \Delta_i = |raw\_hi[i] - raw\_hi[i-1]|
  $$
- The first value is treated as zero by prepending the first distance value, so the initial step does not create artificial degradation.

This gives a sequence of incremental degradation amounts.

4. These increments are accumulated
- The cumulative degradation is built by summing those increments:
  $$
  cum\_hi[i] = \sum_{j=1}^{i} \Delta_j
  $$
- Because it is a cumulative sum, it is monotonic: it never decreases.

5. The cumulative score is normalized
- If the maximum cumulative value is zero, there is no detected degradation, so the function returns an array of ones:
  $$
  HI = 1
  $$
- Otherwise, the cumulative score is normalized by its maximum:
  $$
  cum\_hi\_norm = \frac{cum\_hi}{\max(cum\_hi)}
  $$

6. The final HI is inverted
- Finally, the normalized cumulative degradation is subtracted from 1:
  $$
  final\_hi = 1 - cum\_hi\_norm
  $$

Interpretation:
- At the start, $final\_hi = 1$, which means “fully healthy”.
- As degradation accumulates, the value decreases toward 0.
- So a lower HI indicates a more degraded state.

In short:
- The method turns distance-to-baseline into a cumulative degradation curve,
- then rescales it so the result ranges from 1 (healthy) to 0 (highly degraded).