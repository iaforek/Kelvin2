# Useful commands:

### Prerequisites 

Connect to Kelvin2 first :smile:

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




  
