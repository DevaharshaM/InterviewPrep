# What is a Kernel?

---

The Kernel is the core component of an operating system (OS). It acts as a bridge between software applications and the physical hardware of a computer. Its primary responsibility is to manage system resources, such as the CPU, memory, and I/O devices, ensuring that different programs and users operate efficiently and securely.

## Key Functions of a Kernel:

- **Process Management**: Creates, schedules, and terminates processes.
- **Memory Management**: Allocates and deallocates memory space as needed.
- **File System Management**: Provides a structured way to store and retrieve data on storage devices.
- **Device Management**: Facilitates communication between software and hardware via device drivers.
- **System Calls Handling**: Provides an interface for user applications to interact with hardware.

## Types of Kernels:

| Type	                | Description                                                                  |
|-----------------------|------------------------------------------------------------------------------|
| **Monolithic Kernel**	| All OS services run in the kernel space (e.g., Linux).                       |
| **Microkernel**	      | Minimal set of services in kernel; rest run in user space (e.g., Minix, QNX).|
| **Hybrid Kernel**	    | Combines elements of monolithic and microkernel (e.g., Windows NT, macOS).   |

### Example-

When you open a file, the kernel:
1. Checks permissions
2. Allocates memory for buffers
3. Passes commands to the file system and device drivers
