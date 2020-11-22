## Simulation Object
### attributes
* UUID
* Isoscape raw data file format 1-D array, indexed by cell #
* Isoscape coordinate file format 2-D array indexed by dell #
* cell weighting file format 1-D array, indexex by cell # : 0 means disallowed cell.
* track raw data file format 1-D array, indexed by track location #
* maximum step radius: dx^2+dy^2
* starting cell number
* starting track position
* intermediate data product directory
 
### Intermediate data products
#### Potential next step cells
1 file per isoscape cell, contains cell number array for all cells within walk radius of specified cell. Each file is variable length, depending on cell location. isoscape topology isn't assumed. Could be square, could variable density.
 
#### track isoscape cell probability    
1 file per track location. Contains 2-D array representing the probability

## Simulation Initializer Function (run once)
* Reads in raw isoscape data and save it into internal cell format arrays
* Reads in raw cell weighting and saves into internal cell format array
* Reads in raw track data and saves into internall track format
* set step radius
* set starting cell
* Sets UUID
* calculates intermediata data products and saves into internal file format

## Random Walk Iterator (can be run multiple times in parallel)
### Inputs
* simulation object UUID
* number of steps

### Attributes
* current step number
* current track number
* cell history

### Walker init
* starts with empty cell history
* takes simulation starting cell # as current isoscape cell
* takes simulation starting track position as current isoscape cell

### Iteration Execution
1. Reads in track isoscape probability file for position (t)
2. Read in potential next step file for cell (i)
3. Reads in simulaton cell weighting array
4. builds next step cell probability distribution 
5. uses numpy.random.choice to select cell for next step.
6. update cell history and prepare for next track position


