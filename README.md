basiccoin retargeting scheme

Abstract.
Difficulty retargeting schemes allow a DAC (Distributed Autonomous Corporation) to maintain consistent blocktimes, even if the mining power changes over time. In this paper we propose a scheme with these properties:
1) recovers from a 90% loss of mining power within 10 blocks.
2) Holding mining power constant, oscillations in difficulty due to random chance stay within 5% of average difficulty.

1. Introduction
Bitcoin takes 2024 blocks before it begins reacting to a change in the mining power of the network. Normally, this only takes 2 weeks of time, but if 90% of the miners left at once, each block would take 10x longer than normal. In such a situation, it would take 20 weeks before bitcoin is able to react to the change in hashpower. During those 20 weeks, bitcoin would only support 1/10th the normal volume of transactions. In this paper we propose a difficulty retargeting scheme which needs only 10 blocks of time to react to a change in mining power.

2. Target
The target is a 64-digit hexidecimal number which is used to represent how difficult it is to mine the next block. Each block has a target which can be computed by looking at the targets and timestamps of the previous 1000 blocks. SHA256 also outputs 64-digit hexidecimal numbers. For a block to be valid, the SHA256 of that block must return a number which is smaller than that block's target.

3. formula for target of next block:
(estimate of the target over last 1000 blocks)*(estimate of blocktime for last 1000 blocks)/(correct blocktime)

4. Geometric series 
examples: 0.5 0.25 0.125 0.0625 0.03125 ...
0.9 0.81 0.729 0.6561 ...
let w=0.985
The geomtric series we use in this paper:
1, w, w^2, w^3, w^4... w^1000

This series is used because the first 50 numbers summed together are as big as the rest of the numbers together:
1+w+w^2+...+w^50=w^51+w^52+...+w^998+w^999+w^1000
let total_weight=1+w+w^2+...+w^999+w^1000

5. How to estimate blocktime
let w(i)=weights, so w(0)=1, w(1)=0.98...
let b(i)=blocktime of block number i, so b(0) is how long the first block too to mine, etc.
estimated_blocktime= sum from i=0 to i=1000 w(i)*b(i)/total_weight

6. How to estimate difficulty
let w(i)=weights, so w(0)=1, w(1)=0.98...
let t(i)=target of block number i, so t(0) is target of first block, etc.
1/estimated_target= sum from i=0 to i=1000 w(i)/t(i)/total_weight