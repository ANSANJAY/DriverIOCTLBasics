Sending a signal from module to process
=========================================

The function for doing this is

int send_sig(int signal, struct task_struct *task, int priv);

signal --> Signal to send

task   --> Corresponds to task_struct corresponding to the process

priv   --> 0 for user applications, 1 for kernel


