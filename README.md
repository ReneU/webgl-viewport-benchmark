# WebGL Performance Test: Viewport vs Resize

A benchmarking tool to compare the performance of using `gl.viewport()` versus canvas resizing for rendering to different output sizes in WebGL applications.

⚠️ **Warning**: This tool allocates GPU resources and may temporarily impact system performance. Extreme test configurations (many renders, complex scenes) may cause browser slowdowns on lower-end hardware.

## Metrics Explained

### Average Time
Mean render time across all operations. Lower is better.

### Median Time
Middle value when sorted. Less affected by outliers than average.

### 95th Percentile (p95)
95% of renders completed faster than this time. Indicates typical worst-case performance.

### 99th Percentile (p99)
99% of renders completed faster than this time. Catches rare performance spikes.

### Min / Max
Fastest and slowest individual render times.

## Interpreting Results

### When Viewport Wins
- Similar output sizes (variation < 4×)
- Frequent rendering operations
- Memory-stable workloads

**Use viewport approach for**: thumbnail grids, split-screen views, multi-viewport editors

### When Resize Wins
- Extreme size differences (variation > 8×)
- Infrequent rendering operations
- Memory-constrained environments

**Use resize approach for**: occasional high-res exports, zoom operations with large scale changes

### Watch Out For
- **High p95/p99 values**: Indicates inconsistent performance, may cause visible stuttering
- **Large average-median gap**: Suggests frequent performance spikes
- **Memory differences**: Important on mobile devices with limited RAM

## Technical Details

The tool uses:
- `gl.viewport(x, y, width, height)` for the viewport approach
- `canvas.width/height` modification for the resize approach
- `gl.finish()` to force GPU completion for accurate timing
- `performance.now()` for high-resolution timing