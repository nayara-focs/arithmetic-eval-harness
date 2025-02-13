# Arithmetic Task Spacing Bug Fix

## Issue Description
The arithmetic tasks in LM-Evaluation-Harness exhibited inconsistent behavior between zero-shot and few-shot evaluation due to a spacing issue in example construction. This caused significant performance degradation in few-shot settings.

## Problem Details
The issue arose from inconsistent spacing between few-shot examples and evaluation in arithmetic tasks because:
1. Target values in dataset start with a space (e.g., " 143")
2. The task config's default target_delimiter was defined as " " (a space)
3. The original code concatenated both, leading to double spaces in few-shot examples

## Before vs. after
For example, with Phi-1.5 on arithmetic_2da:
- Zero-shot: ~55.1% accuracy
- Two-shot (before fix): ~0.5% accuracy
- Two-shot (after fix): 78.5% accuracy

## Implementation
The fix is implemented in `samplers.py`, which shows both the original (commented out) and fixed versions of the relevant code. The key change prevents double spacing when both the delimiter and target start with whitespace.

## Status
- Issue reported: [EleutherAI/lm-evaluation-harness#2695](https://github.com/EleutherAI/lm-evaluation-harness/issues/2695)
