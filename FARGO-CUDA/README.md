# FARGO-CUDA
## Autor
* Matias Flores - Universidad de Santiago de Chile
## Instalación Previa
Es necesario instalar CUDA.
1. Descargar e instalar CUDA: 
    * [Link de descarga CUDA](https://developer.nvidia.com/cuda-downloads)
2. Agregar CUDA al PATH:
    * Abrir archivo .bashrc con el siguiente comando: 
        * gedit ~/.bashrc
    * Agregar la siguiente linea al final del archivo:
        * export LD_LIBRARY_PATH=/usr/local/cuda-9.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
        * Cabe recalcar que la carpeta en la cual se encuentra cuda puede variar respecto a la version que se haya instalado.
    * Guardar y cerrar.
## Intalación del programa
1. Solo basta clonar el repositorio desde el siguiente link:
    * [Link Repositorio](https://github.com/MatiasFloresS/CudaProtoplanetaryDisksFloat.git)

## Compilación
Abrir una terminal, acceder a la carpeta que ha sido clonada y ejecutar el siguiente comando:
```
$ make
```

## Previo a Ejecución 
Ingresar a la carpeta clonada y crear una carpeta llamada "out". Está carpeta contendrá la salida de la ejecucion del programa. (esto se podria hacer dentro el makefile).

## Ejecución 
Para ejecutar el programa se debe utilizar el siguiente comando:
```
$ /bin/fargoGPU in/template.par
```
* fargoGPU es el programa ejecutable.
* template.par es el arhivo de entrada para el programa.
