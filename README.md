# I am A.I

# Iniciación en la I.A.

- [Componentes](#componentes)
- [Puesta en marcha](#puesta-en-marcha)
- [Empezando con JupyterLab](#empezando-con-jupyterlab)

***

## Componentes
- NVIDIA JETSON NANO 2GB Developer Kit con Adaptador USB WIRELESS.
- Tarjeta Memoria Micro SD 64GB.
  - microSD Card (UHS-1 32 GB minimum)
  - 64 GB o más recomendado
  - Se recomienda una tarjeta de alta resistencia
- Teclado y ratón USB
- Pantalla HDMI y cable HDMI.
- Fuente de alimentación USB-C (5V⎓3A).
- Adaptador wireless 802.11ac y cable de extensión.
- Camara webcam compatible, tales como: 
  - Logitech C270 Webcam (USB webcam camera)
  - Raspberry Pi V2 Camera

***

## Puesta en marcha

1. Nos bajamos la imagen del firmware `Jetson Nano 2GB Developer Kit SD Card Image` de 6GB.

[https://developer.nvidia.com/jetson-nano-2gb-sd-card-image](https://developer.nvidia.com/jetson-nano-2gb-sd-card-image)

2. La introducimos en la memoria microSD de 64GB con por ejemplo Etcher desde un ordenador.

[https://www.balena.io/etcher/](https://www.balena.io/etcher/)

3. Conectamos la memoria microSD a la placa Jetson Nano, el teclado y el ratón, la pantalla HDMI, el adaptador USB WiFi y conectamos la alimentación al conector USB-C.

La tarjeta microSD se tiene que conectar al puerto microSD de la Jetson con los pines metálicos de la tarjeta microSD mirando hacia arriba.
  
![Placa Jetson Nano 2GB](./jetson-nano-2gb.png)

4. Realizamos el proceso de instalación de la imagen Ubuntu, creando nuestro usuario para acceder a la Jetson.

5. Actualizamos la distribución.

        apt update & apt upgrade

6. Conectamos nuestra webcam a la Jetson.

Podemos mirar el video en el apartado `URLs` para ver como conectar la `Rasberry PI Camera V2` al conector `MPI CSI-2`.

7. Creamos el directorio donde compartiremos los datos con la imagen docker del servidor JupyterLab.

        mkdir -p ~/nvdli-data

8. Arrancamos el servidor JupyterLab dockerizado:

Si tenemos una camara USB, ejecutaremos los siguientes comandos.

        echo "sudo docker run --runtime nvidia -it --rm --network host \
            --volume ~/nvdli-data:/nvdli-nano/data \
            --device /dev/video0 \
            nvcr.io/nvidia/dli/dli-nano-ai:v2.0.1-r32.4.4" > docker_dli_run.sh
        chmod +x docker_dli_run.sh
        ./docker_dli_run.sh

Si tenemos una camara CSI, ejecutaremos los siguientes comandos.

        echo "sudo docker run --runtime nvidia -it --rm --network host \
              --volume ~/nvdli-data:/nvdli-nano/data \
              --volume /tmp/argus_socket:/tmp/argus_socket \
              --device /dev/video0\
              nvcr.io/nvidia/dli/dli-nano-ai:v2.0.1-r32.4.4" > docker_dli_run.sh
        chmod +x docker_dli_run.sh
        ./docker_dli_run.sh

Este proceso puede tardar un rato, ya que se tiene que bajar las imágenes docker.

9.  Una vez docker ha arrancado tenemos el servicio JupyterLab en el puerto 8888. Y nos aparecerá un mensaje parecido al siguiente:

> Logging Into The JupyterLab Server \
> browser: 192.168.55.1:8888 \
> password: dlinano 

10. Ahora podremos acceder desde nuestro portatil al servidor JupyterLab usando un navegador web. Por ejemplo:

[http://192.168.55.1:8888/](http://192.168.55.1:8888/)

## Empezando con JupyterLab

La interfaz de JupyterLab es un panel que proporciona acceso a los cuadernos interactivos de Jupyter.

  **... continuará ...**

***

## URLs Referencia:
- [Getting Started with Jetson Nano 2GB Developer Kit](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit)
- [Welcome to Getting Started with AI on Jetson Nano!](https://courses.nvidia.com/courses/course-v1:DLI+S-RX-02+V2/)
- [Raspberry Pi Camera Connection Demonstration](https://dli-lms.s3.amazonaws.com/data/c-rx-02/videos/3_Camera-insertion.mp4)
