# app-mpi

run MPI App under Docker.

### 1. Create and use a directory

```
mkdir app-mpi
cd app-mpi
```

### 2. Add ``hello_world.c`` script
```
#include <mpi.h>
#include <stdio.h>

int main(int argc, char* argv[]) {

	int numberOfProcessors;
	int rank;
	int namelen;
	char processor_name[MPI_MAX_PROCESSOR_NAME];

    MPI_Init(&argc,&argv);
	printf("Hello MPI\r\n");

	MPI_Comm_size(MPI_COMM_WORLD,&numberOfProcessors);
	printf("Jumlah processor = %d\r\n", numberOfProcessors);

	MPI_Get_processor_name(processor_name, &namelen);
	printf("Nama Processor = %s\r\n", processor_name);

	MPI_Comm_rank(MPI_COMM_WORLD, &rank);
	printf("Proses pada %d\r\n", rank);	

	MPI_Finalize();
	return 0;

}
```

### 3. Run this script
```
linux/mac

docker run -it --mount src="$(pwd)",target=/home,type=bind wildanbudiawanz/app-mpi:1.0


windows:
docker run -it --mount src="C:\Users\User Name\Documents\MPI",target="/home",type=bind wildanbudiawanz/app-mpi:1.0
```

### 4. Select ``/home`` directory under docker container
```
cd /home
```

### 5. Check the directory
`ll` or 'ls' the directory, it should be one file ``hello_world.c``

### 6. Compile MPI Code
```
mpicc hello_world.c -o hello_world -Wall
```
### 7 Run
```
mpiexec --allow-run-as-root -n 2 ./hello_world
```
