---
title: Implementar sin conexión
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo realizar una implementación sin conexión de un clúster de macrodatos de SQL Server.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd8b3128fc11037a5ade494813611d473c995f8f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419369"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Realización de una implementación sin conexión de un clúster de macrodatos SQL Server

En este artículo se describe cómo realizar una implementación sin conexión de un clúster de macrodatos SQL Server 2019 (versión preliminar). Los clústeres de Big Data deben tener acceso a un repositorio de Docker desde el que extraer las imágenes del contenedor. Una instalación sin conexión es aquella en la que las imágenes necesarias se colocan en un repositorio privado de Docker. Ese repositorio privado se usa a continuación como el origen de la imagen para una nueva implementación.

## <a name="prerequisites"></a>Requisitos previos

- Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Cargar imágenes en un repositorio privado

En los pasos siguientes se describe cómo extraer las imágenes de contenedor del clúster de Big Data del repositorio de Microsoft y, a continuación, insertarlos en el repositorio privado.

> [!TIP]
> En los pasos siguientes se explica el proceso. Sin embargo, para simplificar la tarea, puede usar el [script automatizado](#automated) en lugar de ejecutar estos comandos manualmente.

1. Extraiga las imágenes del contenedor de clúster de Big Data repitiendo el siguiente comando. Reemplazar `<SOURCE_IMAGE_NAME>` por cada [nombre de imagen](#images). Reemplace `<SOURCE_DOCKER_TAG>` por la etiqueta de la versión del clúster de Big Data, como **2019-CTP 3.2-Ubuntu**.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Inicie sesión en el registro de Docker privado de destino.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Etiquete las imágenes locales con el siguiente comando para cada imagen:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Inserte las imágenes locales en el repositorio privado de Docker:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a>Imágenes de contenedor de clúster de Big Data

Las siguientes imágenes de contenedor de clúster de Big Data son necesarias para una instalación sin conexión:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
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
 - **MSSQL-seguridad-compatibilidad**

## <a id="automated"></a>Script automatizado

Puede usar un script de Python automatizado que extraerá automáticamente todas las imágenes de contenedor necesarias y las incluirá en un repositorio privado.

> [!NOTE]
> Python es un requisito previo para usar el script. Para obtener más información sobre cómo instalar Python, consulte la [documentación de Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. En bash o PowerShell, descargue el script con **rizo**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. A continuación, ejecute el script con uno de los siguientes comandos:

   **Windows**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linuxun**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Siga las indicaciones para especificar el repositorio de Microsoft y la información privada del repositorio. Una vez completado el script, todas las imágenes necesarias deben encontrarse en el repositorio privado.

## <a name="install-tools-offline"></a>Instalar herramientas sin conexión

Las implementaciones de clúster de Big Data requieren varias herramientas, como **Python**, **azdata**y **kubectl**. Siga los pasos siguientes para instalar estas herramientas en un servidor sin conexión.

### <a id="python"></a>Instalación de Python sin conexión

1. En una máquina con acceso a Internet, descargue uno de los siguientes archivos comprimidos que contienen Python:

   | Sistema operativo | Descargar |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie el archivo comprimido en el equipo de destino y extráigalo en una carpeta de su elección.

1. Solo para Windows, ejecute `installLocalPythonPackages.bat` desde esa carpeta y pase la ruta de acceso completa a la misma carpeta que un parámetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a>Instalación de azdata sin conexión

1. En una máquina con acceso a Internet y [Python](https://wiki.python.org/moin/BeginnersGuide/Download), ejecute el siguiente comando para descargar todos los paquetes de **azdata** en la carpeta actual.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. Copie los paquetes descargados y el archivo **requirements. txt** en el equipo de destino.

1. Ejecute el siguiente comando en el equipo de destino, especificando la carpeta en la que copió los archivos anteriores.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a>Instalación de kubectl sin conexión

Para instalar **kubectl** en un equipo sin conexión, siga estos pasos.

1. Use **rizo** para descargar **kubectl** en una carpeta de su elección. Para obtener más información, consulte [instalación del archivo binario kubectl con rizo](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).

1. Copie la carpeta en el equipo de destino.

## <a name="deploy-from-private-repository"></a>Implementación desde un repositorio privado

Para realizar la implementación desde el repositorio privado, siga los pasos descritos en la [Guía de implementación](deployment-guidance.md), pero use un archivo de configuración de implementación personalizado que especifique la información privada del repositorio de Docker. Los siguientes comandos de **azdata** muestran cómo cambiar la configuración de Docker en un archivo de configuración de implementación personalizado denominado **control. JSON**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

La implementación le pedirá el nombre de usuario y la contraseña de Docker, o puede especificarlos en las variables de entorno **DOCKER_USERNAME** y **DOCKER_PASSWORD** .

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre las implementaciones de clúster de Big Data, consulte [cómo implementar clústeres de macrodatos SQL Server en Kubernetes](deployment-guidance.md).
