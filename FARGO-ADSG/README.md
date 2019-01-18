# FARGO-ADSG
## Instalación Previa
Es necesario instalar MPI, para ello se utiliza el siguiente comando:
```
sudo apt-get install mpich mpich-doc
```

## Intalación del programa
1. Se debe dirigir a la pagina oficial de [FARGO-ADSG](http://fargo.in2p3.fr/-FARGO-ADSG-) y descargar el programa
2. Descomprimir el programa con los siguientes comandos:
```
gzip -d fargoadsg.tar.gz
tar xvf fargoadsg.tar
```

## Instalacion de fftw
Primero se hace necesario instalar la librería fftw. Se debe dirigir a la pagina oficial de [fftw](http://www.fftw.org/download.html) y descargar la version 2.1.5.

Una vez descomprimida la carpeta, se entra a dicha carpeta y se hace:
./configure --enable-mpi --prefix='myfftwdir'
make
make install

donde myfftwdir puede ser por ejemplo:  --prefix='/home/user/Desktop/fftw'


## Agregar al PATH 
Abrir el archivo .baschrc con el siguiente comando:
```
gedit ~/.bashrc
```
o para editar desde una terminarl con el siguiente comando:
```
vim ~/.bashrc
```
Luego agregar al final del archivo las siguientes lineas:
```
export FFTW_PREFIX='/home/matias/Escritorio/fftw'
export MPI_PREFIX='/usr/lib/mpich'
```
Es necesario que los prefix vayan sin "/" al final, ya que se les agrega en el makefile del programa. Además, esas rutas depende donde fueron instalados mpi y la librería fftw.

## Compilación 
Para compila se utiliza el siguiente comando:
```
make BUILD=parallelfftw
```

## Ejecución
Primero es necesario modifiar el archivo de entrada:
```
### Disk parameters
	
	AspectRatio     	0.05            Thickness over Radius in the disc
	Sigma0			6.3661977237e-4	Surface Density at r=1
	Viscosity		1e-5		Uniform kinematic viscosity
	SigmaSlope		0.0		Slope of surface density profile.
						#here constant.
	
	### Planet parameters
	
	PlanetConfig		in/Jup.cfg
	ThicknessSmoothing 	0.6		Smoothing parameters in disk thickness
	
	### Numerical method parameters
	
	Transport		FARGO
	InnerBoundary		RIGID	choose : OPEN or RIGID or NONREFLECTING
	Disk			YES
	OmegaFrame     		1.0
	Frame			GUIDING-CENTER
	IndirectTerm		YES
	
	
	### Mesh parameters
	
	Nrad			128		Radial number of zones
	Nsec			384		Azimuthal number of zones (sectors)
	Rmin			0.4		Inner boundary radius
	Rmax			2.5		Outer boundary radius
	RadialSpacing 		ARITHMETIC      Zone interfaces evenly spaced
	
	
	
	### Output control parameters
	
	Ntot			10001		Total number of time steps
	Ninterm	 		20		Time steps between outputs
	DT			0.314159265359	Time step length. 2PI = 1 orbit
	OutputDir		out/
	
	
	SelfGravity	NO     #choose: Yes, Z or No
	
	Adiabatic	NO        #choose No for an isothermal eq. of state
	
	AdiabaticIndex	1.4 #Default value: 1.4
	
	Cooling	NO           #choose: Yes or No
	
	CoolingTime0	31.4 #Cooling time at r=1
	
	WriteQplus NO
	
	WriteEnergy NO

```

Para ejecutar con diferentes numeros de hebras se utilzia el siguiente comando:
```
mpirun -np 2 ./fargo -m in/template.par
```
* -np numero_procesos  
* -m merge (cada procesador hace una parte de la grilla y luego se hace un merge)

