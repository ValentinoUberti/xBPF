# xBPF
Studying eBPF

# Brendan Greg tutorial:
- https://www.youtube.com/watch?v=16slh29iN1g&feature=emb_logo

1) Search for syscall using funccount (bcc-tools)

sudo /usr/share/bcc/tools/funccount '*input_handle_event*'

2) Search for kernel source code 

https://elixir.bootlin.com/linux/latest/source/drivers/input/input.c#L367

sudo /usr/share/bcc/tools/trace 'input_handle_event(struct input_dev *dev,unsigned int type, unsigned int code, int value)'

sudo bpftrace -e 'kprobe:input_handle_event { printf("%u\n", arg3); }'


3) Traces

- Trace file opens

bpftrace -e 'tracepoint:syscalls:sys_enter_openat { printf("%s %s\n", comm, str(args->filename)); }'

- Getting infos about generated struct by bpftrace

bpftrace -vl tracepoint:syscalls:sys_enter_openat


