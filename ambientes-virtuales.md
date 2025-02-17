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

### 2.1 Requisitos previos

Antes de instalar WSL, es necesario descargar e instalar **Microsoft Visual C++ Redistributable**:

1. Ve al siguiente enlace: [Última versión de VC++ Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
2. Descarga la versión **x86**.
3. Instala el paquete descargado.

### 2.2 Habilitar WSL

Ejecuta en **Windows PowerShell** como Administrador:

```powershell
wsl --install
```

Esto instalará WSL junto con la distribución predeterminada (Ubuntu). Si ya tienes WSL instalado, puedes actualizarlo con:

```powershell
wsl --update
```

### 2.3 Configurar Ubuntu tras la instalación

1. Una vez completada la instalación, se descargará **Ubuntu** por defecto.
2. Se te pedirá que configures un nombre de usuario y una contraseña.
3. Luego, cierra la terminal.

### 2.4 Abrir Ubuntu en Windows

1. Dirígete al **buscador de Windows** y abre la aplicación **Ubuntu**.
2. Si por alguna razón la aplicación no aparece, puedes descargarla desde la Microsoft Store en el siguiente enlace:
   - [Descargar Ubuntu](https://apps.microsoft.com/detail/9pdxgncfsczv?hl=es-ES&gl=ES)

### 2.5 Verificar Instalación

Para verificar que WSL está instalado correctamente, ejecuta:

```powershell
wsl --list --verbose
```

Esto mostrará las distribuciones instaladas y su estado.

### 2.6 Instalar una Distribución Específica

Si deseas instalar una distribución diferente, usa el siguiente comando:

```powershell
wsl --install -d <Distribución>
```

Reemplaza `<Distribución>` con el nombre de la distribución deseada, por ejemplo:

```powershell
wsl --install -d Debian
```

### 2.7 Actualizar y configurar Ubuntu

Una vez dentro de la terminal de Ubuntu, ejecuta:

```bash
sudo apt update && sudo apt upgrade
```

Esto actualizará los paquetes del sistema a la última versión disponible.

### 2.8 Referencia al tutorial original

Este tutorial está basado en el siguiente video:
[Ver tutorial en YouTube](https://youtu.be/xJtmj6hX5Lg?si=3TqBPOITtpBmX52l&t=791)

### 3. Fuentes adicionales

Para más información sobre instalación y configuración, consulta los siguientes enlaces:
- [Instalación de TensorFlow con pip](https://www.tensorflow.org/install/pip?hl=es-419)
- [Repositorio de Miniforge en GitHub](https://github.com/conda-forge/miniforge)

---
