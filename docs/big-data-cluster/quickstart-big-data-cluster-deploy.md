---
title: Guía de inicio rápido de implementación
titleSuffix: SQL Server 2019 big data clusters
description: Tutorial de una implementación de clústeres de macrodatos de 2019 de SQL Server (versión preliminar) en Azure Kubernetes Service (AKS).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 00810eb3f57fdaf8f87fc0db16744ab9e3334f70
ms.sourcegitcommit: 0c049c539ae86264617672936b31d89456d63bb0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58618152"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Inicio rápido: Implementar el clúster de macrodatos de SQL Server en Azure Kubernetes Service (AKS)

En este tutorial, usará un script de implementación de ejemplo para implementar el clúster de macrodatos de 2019 de SQL Server (versión preliminar) para Azure Kubernetes Service (AKS). 

> [!TIP]
> AKS es sólo una opción para hospedar Kubernetes para el clúster de macrodatos. Para obtener información sobre otras opciones de implementación, así como la forma para personalizar la implementación de opciones, consulte [de clústeres de cómo implementar grandes de datos de SQL Server en Kubernetes](deployment-guidance.md).

La implementación del clúster de macrodatos predeterminado usada aquí consta de una instancia de SQL Master, proceso de una instancia del grupo, dos instancias de grupo de datos y dos instancias del grupo de almacenamiento. Datos se guardan con volúmenes persistentes de Kubernetes que usan las clases de almacenamiento predeterminada AKS. La configuración predeterminada utilizada en este inicio rápido es adecuada para entornos de desarrollo y pruebas.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Requisitos previos

- Una suscripción de Azure.
- [Herramientas de macrodatos](deploy-big-data-tools.md):
   - **mssqlctl**
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **Azure CLI**

## <a name="log-in-to-your-azure-account"></a>Inicie sesión en su cuenta de Azure

El script usa la CLI de Azure para automatizar la creación de un clúster de AKS. Antes de ejecutar el script, debe iniciar sesión con su cuenta de Azure CLI de Azure al menos una vez. Ejecute el siguiente comando desde un símbolo del sistema.

```
az login
```

## <a name="download-the-deployment-script"></a>Descargar el script de implementación

En este tutorial rápido se automatiza la creación del clúster de macrodatos en AKS mediante un script de python **implementar-sql-big-data-aks.py**. Si ya ha instalado python para **mssqlctl**, debería poder ejecutar correctamente el script en este inicio rápido. 

En una solicitud de bash Windows PowerShell o Linux, ejecute el siguiente comando para descargar el script de implementación desde GitHub.

```
curl -o deploy-sql-big-data-aks.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/aks/deploy-sql-big-data-aks.py"
```

## <a name="run-the-deployment-script"></a>Ejecute el script de implementación

Utilice los pasos siguientes para ejecutar el script de implementación. Este script creará un servicio AKS en Azure y, a continuación, implementar un clúster de macrodatos de 2019 de SQL Server en AKS. También puede modificar el script con otros [variables de entorno](deployment-guidance.md#env) para crear una implementación personalizada.

1. Ejecute el script con el siguiente comando:

   ```
   python deploy-sql-big-data-aks.py
   ```

   > [!NOTE]
   > Si tiene python3 y python2 en el equipo cliente y en la ruta de acceso, tendrá que ejecutar el comando mediante python3: `python3 deploy-sql-big-data-aks.py`.

1. Cuando se le solicite, escriba la siguiente información:

   | Valor | Descripción |
   |---|---|
   | **Id. de suscripción de Azure** | El identificador de suscripción de Azure que se usará para AKS. Puede enumerar todas las suscripciones y sus identificadores ejecutando `az account list` desde otra línea de comandos. |
   | **Grupo de recursos de Azure** | El nombre del grupo de recursos de Azure para crear el clúster de AKS. |
   | **Nombre de usuario de docker** | El nombre de usuario de Docker proporcionada como parte de la versión preliminar pública limitada. |
   | **Contraseña de docker** | La contraseña de Docker proporcionada como parte de la versión preliminar pública limitada. |
   | **Región de Azure** | La región de Azure para el nuevo clúster AKS (valor predeterminado **westus**). |
   | **Tamaño de la máquina** | El [tamaño de la máquina](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) que se usará para los nodos del clúster AKS (valor predeterminado **Standard_L8s**). |
   | **Nodos de trabajo** | El número de nodos de trabajo en el clúster de AKS (valor predeterminado **1**). |
   | **Nombre del clúster** | El nombre de clúster AKS y el clúster de macrodatos. El nombre del clúster debe ser solo caracteres alfanuméricos en minúsculas y sin espacios en blanco. (valor predeterminado **sqlbigdata**). |
   | **Contraseña** | Contraseña para el controlador, la puerta de enlace de Spark o HDFS y la instancia maestra (valor predeterminado **MySQLBigData2019**). |
   | **Controlador para el usuario** | Nombre de usuario para el usuario del controlador (predeterminado: **admin**). |

   > [!IMPORTANT]
   > El valor predeterminado **Standard_L8s** tamaño de la máquina no estén disponible en todas las regiones de Azure. Si selecciona un tamaño de máquina diferentes, asegúrese de que el número total de discos que se puede conectar a través de los nodos del clúster es mayor o igual a 24. Cada notificación de volumen persistente en el clúster requiere un disco conectado. Actualmente, el clúster de macrodatos requiere 24 notificaciones de volumen persistente. Por ejemplo, el [Standard_L8s](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-storage#ls-series) tamaño de la máquina es compatible con 32 discos conectados, por lo que se pueden evaluar los clústeres de datos de gran tamaño con un solo nodo de este tamaño de la máquina.

   > [!NOTE]
   > El `sa` cuenta es un administrador del sistema en la instancia principal de SQL Server que se crea durante la instalación. Después de crear la implementación, el `MSSQL_SA_PASSWORD` variable de entorno es reconocible ejecutando `echo $MSSQL_SA_PASSWORD` en el contenedor de la instancia maestra. Por motivos de seguridad, cambiar su `sa` contraseña en la instancia principal después de la implementación. Para obtener más información, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

1. Se iniciará la secuencia de comandos mediante la creación de un clúster de AKS mediante los parámetros especificados. Este paso tarda varios minutos.

   <img src="./media/quickstart-big-data-cluster-deploy/script-parameters.png" width="800px" alt="Script parameters and AKS cluster creation"/>

## <a name="monitor-the-status"></a>Supervisar el estado

Después de la secuencia de comandos crea el clúster de AKS, continúa para establecer variables de entorno necesarias con la configuración que especificó anteriormente. A continuación, llama **mssqlctl** para implementar el clúster de macrodatos en AKS.

La ventana de comandos de cliente dará como resultado el estado de implementación. Durante el proceso de implementación, debería ver una serie de mensajes donde está esperando el pod del controlador:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Después de 10 a 20 minutos, se debería notificar que se está ejecutando el pod del controlador:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> Toda la implementación puede tardar mucho tiempo debido al tiempo necesario para descargar las imágenes de contenedor para los componentes del clúster de macrodatos. Sin embargo, no debería tardar varias horas. Si experimenta problemas con la implementación, consulte el [solución de problemas de implementación](deployment-guidance.md#troubleshoot) sección del artículo de guía de implementación.

## <a name="inspect-the-cluster"></a>Inspeccionar el clúster

En cualquier momento durante la implementación, puede usar kubectl o el Portal de administración de clúster para inspeccionar el estado y los detalles sobre el clúster de ejecución de macrodatos.

### <a name="use-kubectl"></a>Usar kubectl

Abra una ventana de comandos para usar **kubectl** durante el proceso de implementación.

1. Ejecute el siguiente comando para obtener un resumen del estado de todo el clúster:

   ```
   kubectl get all -n <your-cluster-name>
   ```

1. Inspeccionar los servicios de kubernetes y sus puntos de conexión internos y externos con el siguiente **kubectl** comando:

   ```
   kubectl get svc -n <your-cluster-name>
   ```

1. También puede inspeccionar el estado de los pods de kubernetes con el siguiente comando:

   ```
   kubectl get pods -n <your-cluster-name>
   ```

1. Obtener más información acerca de un pod específico con el siguiente comando:

   ```
   kubectl describe pod <pod name> -n <your-cluster-name>
   ```

> [!TIP]
> Para obtener más información acerca de cómo supervisar y solucionar problemas de una implementación, consulte el [solución de problemas de implementación](deployment-guidance.md#troubleshoot) sección del artículo de guía de implementación.

### <a name="use-the-cluster-administration-portal"></a>Usar el Portal de administración de clúster

Una vez que se está ejecutando el pod del controlador, también puede usar el Portal de administración de clúster para supervisar la implementación. Se puede acceder al portal mediante el número de puerto y dirección IP externo para la `endpoint-service-proxy` (por ejemplo: **https://\<ip-address\>: 30777/portal**). Las credenciales usadas para iniciar sesión en el portal coinciden con los valores para **controlador para el usuario** y **contraseña** que especificó en el script de implementación.

Puede obtener la dirección IP de la **proxy de servicio de punto de conexión** servicio, ejecute este comando en una ventana cmd o bash:

```bash
kubectl get svc endpoint-service-proxy -n <your-cluster-name>
```

> [!NOTE]
> En CTP 2.4, verá una advertencia de seguridad al obtener acceso a la página web, porque los clústeres de macrodatos actualmente está usando certificados SSL generados automáticamente.

## <a name="connect-to-the-cluster"></a>Conéctese al clúster

Cuando finalice el script de implementación, la salida le informa de éxito:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

Ahora se implementa el clúster de macrodatos de SQL Server en AKS. Ahora puede usar Azure Data Studio para conectarse al clúster. Para obtener más información, consulte [conectar a SQL Server del clúster macrodatos con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="clean-up"></a>Limpiar

Si va a probar los clústeres grandes de datos de SQL Server en Azure, debe eliminar el clúster de AKS cuando termine para evitar cargos inesperados. No quite el clúster si piensa seguir usándola.

> [!WARNING]
> Los pasos siguientes destruye el clúster de AKS, lo que elimina el clúster de macrodatos de SQL Server. Si tiene datos de HDFS que desea mantener ni las bases de datos, copia esos datos de seguridad antes de eliminar el clúster.

Ejecute el siguiente comando de CLI de Azure para quitar el clúster de macrodatos y el servicio AKS en Azure (reemplace `<resource group name>` con el **grupo de recursos de Azure** que especificó en el script de implementación):

```azurecli
az group delete -n <resource group name>
```

## <a name="next-steps"></a>Pasos siguientes

El script de implementación había configurado en Azure Kubernetes Service y también implementa un clúster de macrodatos de SQL Server 2019. También puede personalizar las futuras implementaciones a través de las instalaciones manuales. Para aprender más acerca de cómo macrodatos se implementan clústeres, así como la personalización de las implementaciones, consulte [de clústeres de cómo implementar grandes de datos de SQL Server en Kubernetes](deployment-guidance.md).

Ahora que está implementado el clúster de macrodatos de SQL Server, puede cargar datos de ejemplo y explore los tutoriales:

> [!div class="nextstepaction"]
> [Tutorial: Cargar datos de ejemplo en un clúster de macrodatos de SQL Server 2019](tutorial-load-sample-data.md)