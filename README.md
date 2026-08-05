# Useful Commands

### Prerequisites 

Connect to Kelvin2 first :smile:

## Basic Commands

### Check Queue

Check jobs in the queue by user ID:
```
squeue -u USER_ID
```

Example output:
```
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           9558945 k2-gpu-h1 yolov26n 12312399  R    8:58:16      1 gpu121
```
Status: R => running, PD => pending

Check jobs by job ID:
```
squeue -j JOB_ID
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

***
Author: [Arek Jaworski](https://github.com/iaforek/)



  
