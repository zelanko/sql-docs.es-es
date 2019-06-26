---
title: Implementación sin conexión
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo realizar una implementación sin conexión de un clúster de macrodatos de SQL Server.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0f3bfcfba0cfb972c7d02042bc98aa461eb110bb
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388814"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Realizar una implementación sin conexión de un clúster de macrodatos de SQL Server

En este artículo se describe cómo realizar una implementación sin conexión de un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Clústeres de macrodatos deben tener acceso a un repositorio de Docker desde la que extraer imágenes de contenedor. Una instalación sin conexión uno es donde se colocan las imágenes necesarias en un repositorio privado de Docker. Ese repositorio privado, a continuación, se utiliza como el origen de la imagen de una nueva implementación.

## <a name="prerequisites"></a>Requisitos previos

- Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Cargar imágenes en un repositorio privado

Los pasos siguientes describen cómo incorporar el clúster de macrodatos de imágenes de contenedor desde el repositorio de Microsoft y, después, impleméntelas en su repositorio privado.

> [!TIP]
> Los pasos siguientes explican el proceso. Sin embargo, para simplificar la tarea, puede usar el [script automatizado](#automated) en lugar de ejecutar manualmente estos comandos.

1. En primer lugar, inicie sesión en el registro de Docker de Microsoft con el **inicio de sesión de docker** comando. Utilice el nombre de usuario y la contraseña que proporcionó como parte del programa de adopción temprana de Microsoft.

   ```PowerShell
   docker login private-repo.microsoft.com -u  <SOURCE_DOCKER_USERNAME> -p <SOURCE_DOCKER_PASSWORD>
   ```

   > [!TIP]
   > Estos comandos usan PowerShell como ejemplo, pero puede ejecutar desde cualquier shell de comandos que se puede ejecutar docker, bash o cmd. En Linux, agregar `sudo` a cada comando.

1. Extraiga imágenes de contenedor para el clúster de macrodatos, repita el comando siguiente. Reemplace `<SOURCE_IMAGE_NAME>` con cada [nombre de la imagen](#images). Reemplace `<SOURCE_DOCKER_TAG>` con la etiqueta para los datos de gran tamaño de clúster versión, como **ctp3.1**.  

   ```PowerShell
   docker pull private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Inicie sesión en destino privado del registro de Docker.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Etiquetar las imágenes locales con el siguiente comando para cada imagen:

   ```PowerShell
   docker tag private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Insertar la imagen local al repositorio privado de Docker:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> Imágenes de contenedor del clúster de macrodatos

Las siguientes imágenes de contenedor de clúster de macrodatos son necesarias para una instalación sin conexión:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-java**
 - **mssql-mlservices-pythonserver**
 - **mssql-mlservices-rserver**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**
 - **mssql-mleap-serving-runtime**
  

## <a id="automated"></a> Script automatizado

Puede usar un script de python automatizada que extraerá todas las imágenes de contenedor necesarios automáticamente e insertarlas en un repositorio privado.

> [!NOTE]
> Python es un requisito previo para usar la secuencia de comandos. Para obtener más información sobre cómo instalar Python, consulte el [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. En bash o PowerShell, descargue el script con **curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. A continuación, ejecute el script con uno de los siguientes comandos:

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Siga las indicaciones para especificar el repositorio de Microsoft y la información del repositorio privado. Una vez finalizada la secuencia de comandos, todos los necesarios imágenes deben estar ubicadas en su repositorio privado.

## <a name="install-tools-offline"></a>Instalar las herramientas sin conexión

Las implementaciones de clústeres de datos de gran tamaño requieren varias herramientas, como **Python**, **mssqlctl**, y **kubectl**. Utilice los pasos siguientes para instalar estas herramientas en un servidor sin conexión.

### <a id="python"></a> Instalar python sin conexión

1. En un equipo con acceso a internet, descargue uno de los siguientes archivos comprimidos que contienen Python:

   | Sistema operativo | Descargar |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie el archivo comprimido en el equipo de destino y extráigalo en una carpeta de su elección.

1. Para Windows, ejecutan `installLocalPythonPackages.bat` desde esa carpeta y pase la ruta de acceso completa a la misma carpeta que un parámetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="mssqlctl"></a> Instalar mssqlctl sin conexión

1. En un equipo con acceso a internet y [Python](https://wiki.python.org/moin/BeginnersGuide/Download), ejecute el siguiente comando para descargar todos los desactivado el **mssqlctl** paquetes a la carpeta actual.

   ```PowerShell
   pip download -r https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

1. Descargue el **requirements.txt** archivo.

   ```PowerShell
   curl -o requirements.txt "https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt"
   ```

1. Copie los paquetes descargados y el **requirements.txt** archivo a la máquina de destino.

1. Ejecute el siguiente comando en el equipo de destino, especificando la carpeta que ha copiado los archivos anteriores a.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> Instalar sin conexión kubectl

Para instalar **kubectl** a un equipo sin conexión, siga estos pasos.

1. Use **curl** descargar **kubectl** en una carpeta de su elección. Para obtener más información, consulte [instalar binario kubectl con curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).

1. Copie la carpeta en el equipo de destino.

## <a name="deploy-from-private-repository"></a>Implementar desde el repositorio privado

Para implementar desde el repositorio privado, siga los pasos descritos en la [Guía de implementación](deployment-guidance.md), pero usar un archivo de configuración de implementación personalizado que especifica la información del repositorio de Docker privada. La siguiente **mssqlctl** comandos muestran cómo cambiar la configuración de Docker en un archivo de configuración de implementación personalizado denominado **custom.json**:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.docker.repository=<your-docker-repository>"
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.docker.registry=<your-docker-registry>"
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.docker.imageTag=<your-docker-image-tag>"
```

La implementación le pide el nombre de usuario de docker y la contraseña, o puede especificarlos en el **DOCKER_USERNAME** y **DOCKER_PASSWORD** variables de entorno.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de las implementaciones de clústeres de datos de gran tamaño, vea [de clústeres de cómo implementar grandes de datos de SQL Server en Kubernetes](deployment-guidance.md).
