:::warning
- Due to the large blast radius of this fault, we recommend you do not execute it in the production environment.
- Through the fault execution, the application pod can potentially fail to perform successful IO writes if the `write` system call is being targeted. This can cause any data produced in this duration to be lost.
- Any data produced before the execution of the fault is not harmed as a result of its execution.
:::

:::warning
It is recommended to use "mistake" only for READ and WRITE file system calls. Applying "mistake" to other file system calls can result in unforeseen issues, such as file system damage and program crashes.
:::
