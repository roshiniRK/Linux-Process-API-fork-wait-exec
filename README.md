# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to print process ID and parent Process ID using Linux API system calls

```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main(void)
{
    pid_t process_id;
    pid_t p_process_id;
    process_id = getpid();
    p_process_id = getppid();
    printf("The process id: %d\n", process_id);
    printf("The process id of parent function: %d\n", p_process_id);
    return 0;
}

```




## OUTPUT



![image](https://github.com/roshiniRK/Linux-Process-API-fork-wait-exec/assets/118956165/fcc1b775-21dc-4db4-8c3b-aa612a41d744)










## C Program to create new process using Linux API system calls fork() and exit()

```

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main()
{
    int pid;
    pid = fork();
    if (pid == 0)
    {
        printf("I am child, my pid is %d\n", getpid());
        printf("My parent pid is: %d\n", getppid());
        exit(0);
    }
    else
    {
        printf("I am parent, my pid is %d\n", getpid());
        sleep(100);
        exit(0);
    }
}

```



## OUTPUT


![image](https://github.com/roshiniRK/Linux-Process-API-fork-wait-exec/assets/118956165/17913556-870e-4260-bc66-ac22ba24ba86)






## C Program to execute Linux system commands using Linux API system calls exec() family

```

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
int main()
{
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("Fork failed");
        exit(EXIT_FAILURE);
    }
    else if (pid == 0)
    {
        printf("This is the child process. Executing 'ls' command.\n");
        execl("/bin/ls", "ls", "-l", NULL); // Lists files in long format
        perror("execl failed");
        exit(EXIT_FAILURE);
    }
    else
    {
        int status;
        waitpid(pid, &status, 0); // Wait for the child to finish
        if (WIFEXITED(status))
        {
            printf("Child process exited with status %d.\n", WEXITSTATUS(status));
        }
        else
        {
            printf("Child process did not exit normally.\n");
        }
        printf("Parent process is done.\n");
    }
    return 0;
}

```



## OUTPUT



![image](https://github.com/roshiniRK/Linux-Process-API-fork-wait-exec/assets/118956165/36d986ed-d919-4e4c-86f8-ca76b5152f64)





# RESULT:
The programs are executed successfully.
