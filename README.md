# Useful Commands

### Prerequisites 

Connect to Kelvin2 first :smile:

## Basic Commands

### Check Queue

Check jobs in the queue by user ID:
```
squeue -u USERID
```

Example output:
```
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           9558945 k2-gpu-h1 yolov26n 12312399  R    8:58:16      1 gpu121
```
Status: R => running, PD => pending

Check jobs by job ID:
```
squeue -j JOBID
```

Check all jobs on given partition:
```
squeue -p k2-gpu-h100
```

Check estimated start time of pending jobs in the queue. Add `--start` parameter:
```
squeue -p k2-gpu-h100 --start
```

## Start node in interactive mode (basic)

```bash
srun -p k2-hipri -N 1 -n 10 --mem-per-cpu=1G --time=1:00:00 --pty bash
```
This command requests:
* `-p k2-hipri` => `k2-hipri` partition
* `-N 1` => one compute node
* `-n 10` => ten Slurm tasks (normally ten CPUs in total as one CPU per one task)
* `--mem-per-cpu=1G` => 1 GB per allocated CPU, normally 10 GB total
* `--time=1:00:00` => one hour
* `--pty bash` => open interactive Bash session

## Using GPU partition
```bash
srun -p k2-gpu-interactive -N 1 -n 1 --cpus-per-task=4 --gres=gpu:h100:1 --time=03:00:00 --mem=20G --pty bash
```

## List all GPU partitions

```
sinfo | grep -i gpu
```

## List every partition and GRES configuration

```
sinfo -h -o "%P %G" | grep -i gpu
```
* `-h` => hide the column header
* `%P` => partition name
* `%G` => configured Generic RESources (GRES), such as GPU type and count

Example:
```
k2-gpu-interactive gpu:3g.40gb:4(S:2-3,6-7,10-11,14-15),gpu:2g.20gb:8(S:2-3,6-7,10-11,14-15)
```
* `k2-gpu-interactive` => partition name
* `gpu` => GRES name
* `3g.40gb` and `2g.20gb` => GPU type
* `4` and `8` => quantity of GPU resources
* `(S:2-3,6-7,10-11,14-15)` => CPU socket groups

## Monitor partition utilisation

```
srun --jobid=JOBID --overlap nvidia-smi dmon -s pucm -d 2
```

This command shows following output, example:
```
# gpu    pwr  gtemp  mtemp     sm    mem    enc    dec    jpg    ofa   mclk   pclk     fb   bar1   ccpm 
# Idx      W      C      C      %      %      %      %      %      %    MHz    MHz     MB     MB     MB 
    0    147     47     54     37      0      0      0      0      0   2619   1980   3953   3952      0 
    0    146     47     54     43      1      0      0      0      0   2619   1980   3953   3952      0 
    0    148     48     55     38      0      0      0      0      0   2619   1980   3953   3952      0 
    0    146     47     54     52      4      0      0      0      0   2619   1980   3953   3952      0 
    0    147     47     52     38      0      0      0      0      0   2619   1980   3953   3952      0 
    0    146     47     54     37      0      0      0      0      0   2619   1980   3953   3952      0 
    0    145     47     54     44      2      0      0      0      0   2619   1980   3953   3952      0 
    0    146     47     54     38      0      0      0      0      0   2619   1980   3953   3952      0 
    0    148     47     53     38      0      0      0      0      0   2619   1980   3953   3952      0 
    0    147     47     54     38      0      0      0      0      0   2619   1980   3953   3952      0 
    0    147     47     53     51      4      0      0      0      0   2619   1980   3953   3952      0 
    0    152     47     54     55      7      0      0      0      0   2619   1980   3953   3952      0 
    0    146     47     52     37      0      0      0      0      0   2619   1980   3953   3952      0 
    0    150     47     54     46      2      0      0      0      0   2619   1980   3953   3952      0 
    0    152     47     54     41      1      0      0      0      0   2619   1980   3953   3952      0 
    0    150     47     54     59      7      0      0      0      0   2619   1980   3953   3952      0 
    0    151     48     54     62      7      0      0      0      0   2619   1980   3953   3952      0 
    0    141     48     54     44      0      0      0      0      0   2619   1980   3953   3952      0 
```

***
Author: [Arek Jaworski](https://github.com/iaforek/)



  
