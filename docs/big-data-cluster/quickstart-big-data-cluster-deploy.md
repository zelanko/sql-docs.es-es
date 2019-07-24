---
title: Script de implementación
titleSuffix: SQL Server big data clusters
description: 'Tutorial: implementación de clústeres de macrodatos SQL Server 2019 (versión preliminar) en Azure Kubernetes Service (AKS).'
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7ff1ec3672fbcf101d98ad30913742186dea574d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419400"
---
# <a name="deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Implementación de SQL Server clúster de macrodatos en Azure Kubernetes Service (AKS)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial, usará un script de implementación de ejemplo para implementar SQL Server clúster de macrodatos de 2019 (versión preliminar) en Azure Kubernetes Service (AKS). 

> [!TIP]
> AKS es solo una opción para hospedar Kubernetes para el clúster de Big Data. Para obtener información sobre otras opciones de implementación, así como sobre cómo personalizar las opciones de implementación, consulte [cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md).

La implementación de clúster de Big Data predeterminada que se usa aquí consta de una instancia maestra de SQL, una instancia de grupo de proceso, dos instancias de grupo de datos y dos instancias de grupo de almacenamiento. Los datos se conservan con Kubernetes volúmenes persistentes que usan las clases de almacenamiento predeterminadas de AKS. La configuración predeterminada que se usa en este tutorial es adecuada para entornos de desarrollo y pruebas.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Requisitos previos

- Una suscripción de Azure.
- [Herramientas](deploy-big-data-tools.md)de macrodatos:
   - **azdata**
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server extensión 2019**
   - **CLI de Azure**

## <a name="log-in-to-your-azure-account"></a>Inicie sesión en su cuenta de Azure.

El script usa CLI de Azure para automatizar la creación de un clúster de AKS. Antes de ejecutar el script, debe iniciar sesión en su cuenta de Azure con CLI de Azure al menos una vez. Ejecute el siguiente comando desde un símbolo del sistema.

```
az login
```

## <a name="download-the-deployment-script"></a>Descargar el script de implementación

En este tutorial se automatiza la creación del clúster de Big Data en AKS con un script de Python **deploy-SQL-Big-Data-AKS.py**. Si ya ha instalado Python para **azdata**, debería poder ejecutar el script correctamente en este tutorial. 

En un símbolo del sistema de Windows PowerShell o Linux Bash, ejecute el siguiente comando para descargar el script de implementación de GitHub.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>Ejecutar el script de implementación

Siga estos pasos para ejecutar el script de implementación. Este script creará un servicio AKS en Azure y, a continuación, implementará un clúster de macrodatos SQL Server 2019 en AKS. También puede modificar el script con otras [variables de entorno](deployment-guidance.md#configfile) para crear una implementación personalizada.

1. Ejecute el script con el siguiente comando:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Si tiene python3 y python2 en el equipo cliente y en la ruta de acceso, tiene que ejecutar el comando con python3: `python3 deploy-sql-big-data-aks.py`.

1. Cuando se le solicite, escriba la siguiente información:

   | Valor | Descripción |
   |---|---|
   | **IDENTIFICADOR de suscripción de Azure** | El identificador de suscripción de Azure que se usará para AKS. Puede enumerar todas las suscripciones y sus identificadores ejecutando `az account list` desde otra línea de comandos. |
   | **Grupo de recursos de Azure** | Nombre del grupo de recursos de Azure que se va a crear para el clúster de AKS. |
   | **Región de Azure** | La región de Azure para el nuevo clúster de AKS (westus predeterminado). |
   | **Tamaño de la máquina** | El [tamaño](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) de la máquina que se va a usar para los nodos del clúster de AKS (valor predeterminado **Standard_L8s**). |
   | **Nodos de trabajo** | El número de nodos de trabajo en el clúster de AKS (el valor predeterminado es **1**). |
   | **Nombre del clúster** | El nombre del clúster de AKS y del clúster de Big Data. El nombre del clúster de Big Data debe ser solo caracteres alfanuméricos en minúsculas y no espacios. (valor predeterminado **sqlbigdata**). |
   | **Contraseña** | Contraseña del controlador, la puerta de enlace HDFS/Spark y la instancia maestra ( **MySQLBigData2019**predeterminado). |
   | **Usuario del controlador** | Nombre del usuario del controlador (predeterminado: **admin**). |

Los siguientes parámetros eran necesarios para los participantes en el programa de la aplicación del SQL Server 2019 Big Data Cluster: **Nombre de usuario**de Docker y **contraseña**de Docker. A partir de la versión CTP 3,2 ya no son necesarias.

   > [!IMPORTANT]
   > Es posible que el tamaño de máquina **Standard_L8s** predeterminado no esté disponible en todas las regiones de Azure. Si selecciona un tamaño de máquina diferente, asegúrese de que el número total de discos que se pueden conectar a través de los nodos del clúster es mayor o igual que 24. Cada demanda de volumen persistente en el clúster requiere un disco conectado. Actualmente, el clúster de Big Data requiere 24 notificaciones de volumen persistentes. Por ejemplo, el tamaño de la máquina [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#lsv2-series) admite 32 discos conectados, por lo que puede evaluar los clústeres de Big Data con un solo nodo de este tamaño de máquina.

   > [!NOTE]
   > La `sa` cuenta es un administrador del sistema en la SQL Server instancia maestra que se crea durante la instalación. Después de crear la implementación `MSSQL_SA_PASSWORD` , la variable de entorno es reconocible al `echo $MSSQL_SA_PASSWORD` ejecutar en el contenedor de la instancia maestra. Por motivos de seguridad, cambie `sa` la contraseña en la instancia maestra después de la implementación. Para obtener más información, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

1. El script se iniciará mediante la creación de un clúster de AKS con los parámetros especificados. Este paso tarda varios minutos.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>Supervisar el estado

Después de que el script cree el clúster de AKS, procede establecer las variables de entorno necesarias con la configuración que especificó anteriormente. A continuación, llama a **azdata** para implementar el clúster de Big Data en AKS.

La ventana de comandos de cliente generará el estado de implementación. Durante el proceso de implementación, debería ver una serie de mensajes en los que está esperando el POD del controlador:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Después de 10 a 20 minutos, se le notificará que el POD del controlador se está ejecutando:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> Toda la implementación puede tardar mucho tiempo debido al tiempo necesario para descargar las imágenes de contenedor de los componentes del clúster de Big Data. Sin embargo, no debería tardar varias horas. Si tiene problemas con la implementación, consulte [supervisión y solución de problemas](cluster-troubleshooting-commands.md)de clústeres de macrodatos SQL Server.

## <a name="inspect-the-cluster"></a>Inspeccionar el clúster

En cualquier momento durante la implementación, puede usar **kubectl** o **azdata** para inspeccionar el estado y los detalles sobre el clúster de Big Data en ejecución.

### <a name="use-kubectl"></a>Usar kubectl

Abra una nueva ventana de comandos para usar **kubectl** durante el proceso de implementación.

1. Ejecute el siguiente comando para obtener un resumen del estado de todo el clúster:

   ```
   kubectl get all -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Si no cambió el nombre del clúster de Big Data, el script tiene como valor predeterminado **sqlbigdata**.

1. Inspeccione los servicios de kubernetes y sus puntos de conexión internos y externos con el siguiente comando de **kubectl** :

   ```
   kubectl get svc -n <your-big-data-cluster-name>
   ```

1. También puede inspeccionar el estado de los pods de kubernetes con el siguiente comando:

   ```
   kubectl get pods -n <your-big-data-cluster-name>
   ```

1. Obtenga más información sobre un pod específico con el siguiente comando:

   ```
   kubectl describe pod <pod name> -n <your-big-data-cluster-name>
   ```

> [!TIP]
> Para más información sobre cómo supervisar y solucionar problemas de una implementación, consulte [supervisión y solución de problemas](cluster-troubleshooting-commands.md)de clústeres de macrodatos SQL Server.

## <a name="connect-to-the-cluster"></a>Conexión al clúster

Cuando finalice el script de implementación, la salida le notificará que se ha realizado correctamente:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

El clúster de macrodatos de SQL Server ahora está implementado en AKS. Ahora puede usar Azure Data Studio para conectarse al clúster. Para más información, consulte [conexión a un clúster de SQL Server Big Data con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="clean-up"></a>Limpieza

Si está probando SQL Server clústeres de Big Data en Azure, debe eliminar el clúster de AKS cuando termine para evitar cargos inesperados. No quite el clúster si desea seguir utilizándolo.

> [!WARNING]
> En los pasos siguientes se anula el clúster de AKS, que también quita el clúster de macrodatos SQL Server. Si tiene bases de datos o datos de HDFS que desea conservar, vuelva a los datos antes de eliminar el clúster.

Ejecute el siguiente comando de CLI de Azure para quitar el clúster de Big Data y el servicio AKS en Azure `<resource group name>` (reemplace por el **grupo de recursos de Azure** que especificó en el script de implementación):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>Pasos siguientes

El script de implementación configuró el servicio Kubernetes de Azure y también implementó un clúster de macrodatos SQL Server 2019. También puede optar por personalizar las implementaciones futuras a través de instalaciones manuales. Para obtener más información sobre cómo se implementan los clústeres de Big Data y cómo personalizar las implementaciones, consulte [cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md).

Ahora que el clúster de macrodatos SQL Server está implementado, puede cargar los datos de ejemplo y explorar los tutoriales:

> [!div class="nextstepaction"]
> [Tutorial: Carga de datos de ejemplo en un clúster de macroSQL Server 2019 Big Data](tutorial-load-sample-data.md)