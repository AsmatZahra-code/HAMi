# Kunlunxin XPU Support

HAMi supports Kunlunxin XPUs (e.g., P800) for heterogeneous AI clusters, providing both Memory Isolation and Core Isolation capabilities.

## Prerequisites

- Compatible Kunlunxin XPU device (P800-OAM)
- Kunlunxin driver version >= 5.0.21.16 installed on the host
- xpu-container-toolkit >= xpu_container_1.0.2-1 installed and configured

## Resource Allocation

You can request Kunlunxin XPU resources in your Pod specifications using the following labels:

- `kunlunxin.com/xpu`: Request a physical Kunlunxin XPU count.
- `kunlunxin.com/vxpu`: Request a virtual Kunlunxin XPU (device) count.
- `kunlunxin.com/vxpu-memory`: Request virtual XPU memory allocation (in MiB); compute/core allocation is derived from this memory value.

### Example

Here is an example Pod specification requesting Kunlunxin virtual XPU resources:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: kunlunxin-test-pod
spec:
  containers:
  - name: test-container
    image: your-kunlunxin-image:latest
    resources:
      limits:
        kunlunxin.com/vxpu: 1
        kunlunxin.com/vxpu-memory: 4000
```

## Known Limitations

- Multi-card support for Kunlunxin is not currently available.
- Dynamic MIG or similar dynamic partitioning is not supported natively via this plugin.
