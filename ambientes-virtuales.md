# Creación de Ambientes Virtuales en Linux y la Instalación de WSL en Windows

## Introducción

Este documento proporciona una guía paso a paso para:

- Crear y administrar ambientes virtuales en sistemas Linux utilizando Mamba.
- Instalar y configurar el Subsistema de Windows para Linux (WSL) en Windows.

Estas herramientas son esenciales para desarrolladores y científicos de datos que buscan entornos aislados para sus proyectos.

---

## 1. Creación de Ambientes Virtuales en Linux con Mamba

Mamba es una alternativa rápida a Conda para la gestión de paquetes y entornos.

### 1.1 Actualización del Sistema y Herramientas Necesarias

Antes de instalar Mamba, asegúrate de actualizar los paquetes del sistema y tener Git y Curl instalados:

```sh
sudo apt update
sudo apt install git curl
```

### 1.2 Instalación de Mamba

Nos dirigimos al directorio `/tmp`:

```sh
cd /tmp
```

Descargamos el ejecutable de Mamba:

```sh
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```

Lo instalamos:

```sh
bash Miniforge3-$(uname)-$(uname -m).sh
```

Cuando aparezca la siguiente pregunta, seleccionamos **yes**:

```
Do you wish to update your shell profile to automatically initialize conda? This will activate conda on startup and change the command prompt when activated. If you'd prefer that conda's base environment not be activated on startup, run the following command when conda is activated:

conda config --set auto_activate_base false

You can undo this by running conda init --reverse $SHELL? [yes|no] [no]
```

### 1.3 Creación y Activación de un Entorno con Mamba

Para crear un nuevo ambiente virtual con Mamba:

```sh
mamba create -n mi_entorno python=3.10
```

Activamos el entorno:

```sh
mamba activate mi_entorno
```

### 1.4 Creación del Ambiente Virtual del Curso

#### CPU

Para crear un entorno específico para TensorFlow:

```sh
mamba create -n tf-env python=3.11
```

Para activarlo:

```sh
mamba activate tf-env
```

Instalamos TensorFlow y otras dependencias necesarias:

```sh
pip install tensorflow ipykernel notebook scikit-learn matplotlib pandas numpy
```

#### GPU

Para crear un entorno con soporte para GPU:

```sh
mamba create -n tf-gpu-env python=3.11
```

Para activarlo:

```sh
mamba activate tf-gpu-env
```

Instalamos TensorFlow con soporte para CUDA y otras dependencias necesarias:

```sh
pip install tensorflow[and-cuda] ipykernel notebook scikit-learn matplotlib pandas numpy
```

### 1.5 Instalación de Dependencias

Con el entorno activado, instala paquetes con:

```sh
mamba install paquete1 paquete2
```

Para guardar las dependencias en un archivo:

```sh
mamba list --explicit > requirements.txt
```

Para restaurarlas en otro entorno:

```sh
mamba create --name nuevo_entorno --file requirements.txt
```

### 1.6 Desactivación del Ambiente Virtual

Para salir del entorno virtual, usa:

```sh
mamba deactivate
```

---

### 1.7 Comandos Útiles de Mamba

A continuación, se presentan algunos comandos útiles para la gestión de entornos con Mamba:

#### Listar todos los entornos disponibles

```sh
mamba env list
```

#### Eliminar un entorno virtual

Para eliminar un entorno virtual específico:

```sh
mamba env remove -n nombre_del_entorno
```

#### Restaurar el entorno base

Si necesitas restablecer el entorno base de Mamba:

```sh
mamba install --file $CONDA_PREFIX/conda-meta/pinned
```

#### Ver información sobre un entorno

```sh
mamba info -e
```

#### Actualizar Mamba

Para mantener Mamba actualizado:

```sh
mamba update mamba
```

#### Buscar paquetes disponibles

Para buscar un paquete específico:

```sh
mamba search nombre_del_paquete
```

#### Ver paquetes instalados en un entorno

```sh
mamba list
```

Estos comandos te ayudarán a gestionar eficientemente los entornos virtuales con Mamba.

---

## 2. Instalación de WSL en Windows

WSL permite ejecutar un entorno Linux en Windows sin necesidad de una máquina virtual.

### 2.1 Habilitar WSL

Ejecuta en PowerShell como Administrador:

```powershell
wsl --install
```

Esto instalará WSL con la distribución predeterminada (Ubuntu). Si ya tienes WSL instalado, puedes actualizarlo con:

```powershell
wsl --update
```

### 2.2 Verificar Instalación

Para verificar que WSL está instalado, ejecuta:

```powershell
wsl --list --verbose
```

Esto mostrará las distribuciones instaladas y su estado.

### 2.3 Instalar una Distribución Específica

Para instalar una distribución diferente, usa:

```powershell
wsl --install -d Ubuntu
```

Reemplaza `Ubuntu` con la distribución deseada.

