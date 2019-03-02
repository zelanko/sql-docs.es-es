---
title: Cómo implementar
titleSuffix: SQL Server 2019 big data clusters
description: Obtenga información sobre cómo implementar clústeres de macrodatos de 2019 de SQL Server (versión preliminar) en Kubernetes.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 4aba7c8bbe7af361dc118111c8502546c83dd61c
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2019
ms.locfileid: "57227207"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes

Clúster de macrodatos de SQL Server se puede implementar como contenedores de docker en un clúster de Kubernetes. Se trata de una visión general de los pasos de instalación y configuración:

- Configuración de clúster de Kubernetes en una sola máquina virtual, clúster de máquinas virtuales o en Azure Kubernetes Service (AKS).
- Instalar la herramienta de configuración de clúster **mssqlctl** en el equipo cliente.
- Implementar el clúster de macrodatos de SQL Server en un clúster de Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Requisitos previos de clúster de Kubernetes

Clústeres de SQL Server datos de gran tamaño requieren una versión mínima de Kubernetes de al menos v1.10 para el servidor y cliente (kubectl).

> [!NOTE]
> Tenga en cuenta que las versiones de Kubernetes de cliente y servidor deben ser la versión secundaria + 1 o -1. Para obtener más información, consulte [Kubernetes admite versiones y componente sesgo](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

## <a id="kubernetes"></a> Instalación de clúster de Kubernetes

Si ya tiene un clúster de Kubernetes que se cumple por encima de los requisitos previos, puede ir directamente a la [paso de implementación](#deploy). En esta sección se da por supuesto un conocimiento básico de los conceptos de Kubernetes.  Para obtener información detallada sobre Kubernetes, consulte el [documentación de Kubernetes](https://kubernetes.io/docs/home).

Puede elegir implementar Kubernetes en cualquiera de estas tres maneras:

| Implementación de Kubernetes en: | Descripción | Vínculo |
|---|---|---|
| **Minikube** | Un clúster de Kubernetes de nodo único en una máquina virtual. | [Instrucciones](deploy-on-minikube.md) |
| **Azure Kubernetes Service (AKS)** | Un servicio de contenedor de Kubernetes administrado en Azure. | [Instrucciones](deploy-on-aks.md) |
| **Varias máquinas** | Un clúster de Kubernetes implementado en máquinas físicas o virtuales con **kubeadm** | [Instrucciones](deploy-with-kubeadm.md) |
  
> [!TIP]
> Para un script de python de ejemplo que implementa el clúster de macrodatos AKS y SQL Server, vea [implementar un clúster de macrodatos en Azure Kubernetes Service (AKS) de SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

## <a name="deploy-sql-server-2019-big-data-tools"></a>Implementar herramientas de datos de gran tamaño de SQL Server 2019

Antes de implementar el clúster de SQL Server 2019 datos de gran tamaño, en primer lugar [instalar las herramientas de datos de gran tamaño](deploy-big-data-tools.md):
- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **Extensión de SQL Server 2019**

## <a id="deploy"></a> Implementar el clúster de macrodatos de SQL Server

Después de haber configurado el clúster de Kubernetes, puede continuar con la implementación de clúster de macrodatos de SQL Server. 

> [!NOTE]
> Si va a actualizar desde una versión anterior, consulte el [actualizar la sección de este artículo](#upgrade).

Para implementar un clúster de macrodatos en Azure con todas las configuraciones predeterminadas para un entorno de desarrollo y pruebas, siga las instrucciones de este artículo:

[Inicio rápido: Implementar el clúster de macrodatos de SQL Server en Kubernetes](quickstart-big-data-cluster-deploy.md)

Si desea personalizar la implementación de clúster de macrodatos según la carga de trabajo necesita, siga las instrucciones en el resto de este artículo.

## <a name="verify-kubernetes-configuration"></a>Comprobar la configuración de kubernetes

Ejecute el **kubectl** comando para ver la configuración del clúster. Asegúrese de que kubectl apunta al contexto de clúster correcto.

```bash
kubectl config view
```

## <a id="env"></a> Definir variables de entorno

La configuración del clúster puede personalizarse mediante un conjunto de variables de entorno que se pasan a la `mssqlctl create cluster` comando. La mayoría de las variables de entorno es opcional con los valores predeterminados como se indica a continuación. Tenga en cuenta que hay variables de entorno como las credenciales que requieren intervención del usuario.

| Variable de entorno | Obligatorio | Valor predeterminado | Descripción |
|---|---|---|---|
| **ACCEPT_EULA** | Sí | N/D | Acepte el contrato de licencia de SQL Server (por ejemplo, 'Yes').  |
| **CLUSTER_NAME** | Sí | N/D | El nombre del espacio de nombres para implementar SQLServer agrupar datos de gran tamaño en Kubernetes. |
| **CLUSTER_PLATFORM** | Sí | N/D | La plataforma que se implementa el clúster de Kubernetes. Puede ser `aks`, `minikube`, `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | No | 1 | El número de réplicas del grupo de proceso para elaborar. En CTP 2.3 solo con valores permitido es 1. |
| **CLUSTER_DATA_POOL_REPLICAS** | No | 2 | El número de datos de grupo de réplicas para elaborar. |
| **CLUSTER_STORAGE_POOL_REPLICAS** | No | 2 | El número de réplicas de grupo de almacenamiento para elaborar. |
| **DOCKER_REGISTRY** | Sí | TBD | El registro privado donde se almacenan las imágenes se usan para implementar el clúster. |
| **DOCKER_REPOSITORY** | Sí | TBD | El repositorio privado en el registro anterior donde se almacenan las imágenes.  Se requiere para la duración de la versión preliminar pública validada. |
| **DOCKER_USERNAME** | Sí | N/D | El nombre de usuario para tener acceso a las imágenes de contenedor en caso de que se almacenan en un repositorio privado. Se requiere para la duración de la versión preliminar pública validada. |
| **DOCKER_PASSWORD** | Sí | N/D | La contraseña para acceder al repositorio privado anterior. Se requiere para la duración de la versión preliminar pública validada.|
| **DOCKER_IMAGE_TAG** | No | Más reciente | La etiqueta utilizada para etiquetar las imágenes. |
| **DOCKER_IMAGE_POLICY** | No | Always | Fuerce siempre una extracción de las imágenes.  |
| **DOCKER_PRIVATE_REGISTRY** | Sí | N/D | El período de tiempo de la versión preliminar pública validada, debe establecer este valor en "1". |
| **CONTROLLER_USERNAME** | Sí | N/D | El nombre de usuario para el Administrador de clústeres. |
| **CONTROLLER_PASSWORD** | Sí | N/D | La contraseña para el Administrador de clústeres. |
| **KNOX_PASSWORD** | Sí | N/D | La contraseña de usuario de Knox. |
| **MSSQL_SA_PASSWORD** | Sí | N/D | La contraseña del usuario SA para la instancia principal de SQL. |
| **USE_PERSISTENT_VOLUME** | No | true | `true` Para usar notificaciones de volumen persistente de Kubernetes para el almacenamiento de pod.  `false` uso del almacenamiento efímero host para el almacenamiento de pod. Consulte la [persistencia de datos](concept-data-persistence.md) artículo para obtener más detalles. Si implementa SQL Server datos de gran tamaño de clúster de minikube y USE_PERSISTENT_VOLUME = true, debe establecer el valor de `STORAGE_CLASS_NAME=standard`. |
| **STORAGE_CLASS_NAME** | No | predeterminados | Si `USE_PERSISTENT_VOLUME` es `true` indica el nombre de la clase de almacenamiento de Kubernetes para usar. Consulte la [persistencia de datos](concept-data-persistence.md) artículo para obtener más detalles. Si implementa un clúster de macrodatos en minikube de SQL Server, el nombre de clase de almacenamiento predeterminada es diferente y se debe invalidar estableciendo `STORAGE_CLASS_NAME=standard`. |
| **CONTROLLER_PORT** | No | 30080 | El puerto TCP/IP que escucha el servicio del controlador de la red pública. |
| **MASTER_SQL_PORT** | No | 31433 | El puerto TCP/IP que escucha la instancia SQL maestra de la red pública. |
| **KNOX_PORT** | No | 30443 | El puerto TCP/IP que Knox Apache escucha en la red pública. |
| **PROXY_PORT** | No | 30777 | El puerto TCP/IP que escucha el servicio de proxy de la red pública. Este es el puerto utilizado para calcular el portal de dirección URL. |
| **GRAFANA_PORT** | No | 30888 | El puerto TCP/IP que escucha la aplicación de supervisión de Grafana de la red pública. |
| **KIBANA_PORT** | No | 30999 | El puerto TCP/IP que escucha la aplicación de búsqueda de registro de Kibana en la red pública. |


> [!IMPORTANT]
>1. Durante la duración de la versión preliminar privada limitada, le proporcionará las credenciales para el registro privado de Docker para usted tras la clasificación de su [registro EAP](https://aka.ms/eapsignup).
>1. Para un clúster local integrada con **kubeadm**, el valor de variable de entorno `CLUSTER_PLATFORM` es `kubernetes`. También, cuando `USE_PERSISTENT_VOLUME=true`, debe aprovisionar previamente una clase de almacenamiento de Kubernetes y pasarlo a través del uso del `STORAGE_CLASS_NAME`.
>1. Asegúrese de que incluir las contraseñas en las comillas dobles si contiene algún carácter especial. Puede establecer el MSSQL_SA_PASSWORD que prefiera, pero asegúrese de que son lo suficientemente complejos y no utilizar la `!`, `&` o `'` caracteres. Tenga en cuenta que los delimitadores de comillas dobles solo funcionan en los comandos de bash.
>1. El nombre del clúster debe ser solo alfanuméricos caracteres en minúsculas, sin espacios en blanco. Todos los artefactos de Kubernetes (contenedores, pods, conjuntos con estado, los servicios) para el clúster se creará en un espacio de nombres con el mismo nombre que el clúster de nombre especificado.
>1. El **SA** cuenta es un administrador del sistema en la instancia maestra de SQL Server que se crea durante la instalación. Después de crear el contenedor de SQL Server, la variable de entorno MSSQL_SA_PASSWORD especificada es detectable mediante la ejecución de eco MSSQL_SA_PASSWORD $ en el contenedor. Por motivos de seguridad, cambiar la contraseña de SA según los procedimientos recomendados que se documentan [aquí](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Establecer las variables de entorno necesarias para implementar un clúster de macrodatos es diferente dependiendo de si se utiliza el cliente de Windows o Linux.  Elija los pasos siguientes, dependiendo del sistema operativo que esté utilizando.

Inicializar las variables de entorno siguientes, son necesarios para implementar el clúster:

### <a name="windows"></a>Windows

Con una ventana CMD (no PowerShell), configure las siguientes variables de entorno. No utilice comillas alrededor de los valores.

```cmd
SET ACCEPT_EULA=yes
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linux"></a>Linux

Inicialice las variables de entorno siguientes. En bash, puede usar comillas alrededor de cada valor.

```bash
export ACCEPT_EULA=yes
export CLUSTER_PLATFORM=<minikube or aks or kubernetes>

export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="minikube-settings"></a>Configuración de Minikube

Si está implementando en minikube y `USE_PERSISTENT_VOLUME=true` (valor predeterminado), también debe invalidar el valor predeterminado de `STORAGE_CLASS_NAME` variable de entorno.

Use el siguiente comando en Windows para las implementaciones de minikube:

```cmd
SET STORAGE_CLASS_NAME=standard
```

Use el siguiente comando en Linux para las implementaciones de minikube:

```bash
export STORAGE_CLASS_NAME=standard
```

Como alternativa, puede suprimir con volúmenes persistentes en minikube estableciendo `USE_PERSISTENT_VOLUME=false`.

### <a name="kubadm-settings"></a>Configuración de Kubadm

Si va a implementar con kubeadm en sus propias máquinas físicas o virtuales, debe aprovisionar previamente una clase de almacenamiento de Kubernetes y pasarlo a través del uso del `STORAGE_CLASS_NAME`. Como alternativa, puede suprimir con volúmenes persistentes estableciendo `USE_PERSISTENT_VOLUME=false`. Para obtener más información sobre el almacenamiento persistente, consulte [persistencia de datos con SQL Server al clúster de macrodatos en Kubernetes](concept-data-persistence.md).

## <a name="deploy-sql-server-big-data-cluster"></a>Implementar el clúster de macrodatos de SQL Server

La API de creación de clústeres se utiliza para inicializar el espacio de nombres de Kubernetes e implementar todos los pods de aplicación en el espacio de nombres. Para implementar el clúster de macrodatos de SQL Server en el clúster de Kubernetes, ejecute el siguiente comando:

```bash
mssqlctl cluster create --name <your-cluster-name>
```

Durante el arranque del clúster, la ventana de comandos de cliente dará como resultado el estado de implementación. Durante el proceso de implementación, debería ver una serie de mensajes donde está esperando el pod del controlador:

```output
2018-11-15 15:42:02.0209 UTC | INFO | Waiting for controller pod to be up...
```

Después de 10 a 20 minutos, se debería notificar que se está ejecutando el pod del controlador:

```output
2018-11-15 15:50:50.0300 UTC | INFO | Controller pod is running.
2018-11-15 15:50:50.0585 UTC | INFO | Controller Endpoint: https://111.111.111.111:30080
```

> [!IMPORTANT]
> Toda la implementación puede tardar mucho tiempo debido al tiempo necesario para descargar las imágenes de contenedor para los componentes del clúster de macrodatos. Sin embargo, no debería tardar varias horas. Si experimenta problemas con la implementación, consulte el [solución de problemas](#troubleshoot) sección de este artículo para obtener información sobre cómo supervisar e inspeccione la implementación.

Cuando finalice la implementación, la salida le notifica de éxito:

```output
2018-11-15 16:10:25.0583 UTC | INFO | Cluster state: Ready
2018-11-15 16:10:25.0583 UTC | INFO | Cluster deployed successfully.
```

## <a id="masterip"></a> Obtener puntos de conexión de clúster de macrodatos

Después de que el script de implementación se ha completado correctamente, puede obtener la dirección IP de la instancia principal de SQL Server siguiendo los pasos descritos a continuación. Utilizará esta dirección IP y puerto número 31433 para conectarse a la instancia principal de SQL Server (por ejemplo:  **\<ip-address-of-endpoint-master-pool\>, 31433**). De forma similar, puede conectarse a SQL Server IP del clúster (puerta de enlace de Spark o HDFS) de datos de gran tamaño asociado con el **endpoint security** service.

Los siguientes comandos de kubectl para recuperar los puntos de conexión común para el clúster de macrodatos:

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc endpoint-security -n <your-cluster-name>
kubectl get svc endpoint-service-proxy -n <your-cluster-name>
```

Busque el **External-IP** valor que se asigna a cada servicio.

También se describen todos los puntos de conexión de clúster en el **los extremos de servicio** ficha en el Portal de administración de clúster. Se puede acceder al portal mediante el número de puerto y dirección IP externo para la `endpoint-service-proxy` (por ejemplo: **https://\<ip-address-of-endpoint-service-proxy\>: 30777/portal**). Las credenciales de acceso al portal de administración es los valores de `CONTROLLER_USERNAME` y `CONTROLLER_PASSWORD` variables de entorno proporcionadas anteriormente. También puede usar el Portal de administración de clúster para supervisar la implementación.

Para obtener más información sobre cómo conectar, consulte [conectar a SQL Server del clúster macrodatos con Azure Data Studio](connect-to-big-data-cluster.md).

### <a name="minikube"></a>Minikube

Si usas Minikube, deberá ejecutar el siguiente comando para obtener la dirección IP que necesita para conectarse a. Además de la dirección IP, especifique el puerto para el punto de conexión que necesita para conectarse a. Para obtener todos los extremos de servicio para 

```bash
minikube ip
```

Independientemente de la plataforma usa su clúster de Kubernetes, para obtener todos los extremos de servicio implementados para el clúster, ejecute el siguiente comando:
```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="upgrade"></a> Actualizar a una nueva versión

Actualmente, la única manera de actualizar un clúster de macrodatos a una nueva versión es quitar y volver a crear el clúster manualmente. Cada versión tiene una versión única de **mssqlctl** que no es compatible con la versión anterior. Además, si un clúster anterior había que descargar una imagen en un nodo nuevo, la imagen más reciente es posible que no sea compatible con las imágenes anteriores en el clúster. Para actualizar a la versión más reciente, siga estos pasos:

1. Antes de eliminar el clúster antiguo, realizar una copia de seguridad de los datos en la instancia principal de SQL Server y en HDFS. Para la instancia principal de SQL Server, puede usar [SQL Server backup y restore](data-ingestion-restore-database.md). HDFS, le [puede copiar los datos con **curl**](data-ingestion-curl.md).

1. Eliminar el clúster antiguo con el `mssqlctl delete cluster` comando.

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use la versión de **mssqlctl** que coincide con el clúster. No elimine un clúster anterior con la versión más reciente de **mssqlctl**.

1. Desinstale cualquier versión anterior de **mssqlctl**.

   ```bash
   pip3 uninstall mssqlctl
   ```

   > [!IMPORTANT]
   > No debe instalar la nueva versión de **mssqlctl** sin desinstalar primero las versiones anteriores.

1. Instale la versión más reciente de **mssqlctl**. 

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > Para cada versión, la ruta de acceso **mssqlctl** cambios. Incluso si anteriormente instaló **mssqlctl**, debe volver a instalar desde la ruta de acceso más reciente antes de crear el nuevo clúster.

1. Instalar la versión más reciente mediante las instrucciones de la [implementar sección](#deploy) de este artículo. 

## <a id="troubleshoot"></a> Supervisión y solución de problemas

Para supervisar o solucionar problemas de una implementación, use **kubectl** para inspeccionar el estado del clúster y para detectar posibles problemas. En cualquier momento durante la implementación, puede abrir una ventana de comandos diferentes para ejecutar las pruebas siguientes.

1. Inspeccionar el estado de los pods del clúster.

   ```cmd
   kubectl get pods -n <your-cluster-name>
   ```

   Durante la implementación, pods con un **estado** de **ContainerCreating** todavía próximamente. Si la implementación se bloquea por cualquier motivo, esto puede darle una idea donde podría ser el problema. Examine también el **listo** columna. Esto indica cuántos contenedores se han iniciado en el pod. Tenga en cuenta que las implementaciones pueden tardar treinta minutos o más dependiendo de su configuración y la red. Gran parte de este tiempo se dedica a descargar las imágenes de contenedor para los distintos componentes. La siguiente tabla muestra la salida de ejemplo que se puede editar de dos contenedores durante la implementación:

   ```output
   PS C:\> kubectl get pods -n sbdc8
   NAME                                     READY   STATUS              RESTARTS   AGE
   mssql-controller-h79ft                   4/4     Running             0          13m
   mssql-storage-pool-default-0             0/7     ContainerCreating   0          6m
   ```

1. Describir un pod individual para obtener más detalles. El siguiente comando inspecciona el `mssql-storage-pool-default-0` pod.

   ```cmd
   kubectl describe pod mssql-storage-pool-default-0 -n <your-cluster-name>
   ```

   Esto envía la información detallada sobre el pod, incluidos los eventos recientes. Si se ha producido un error, a veces pueden encontrar aquí el error.

1. Recuperar los registros de contenedores que se ejecutan en un pod. El comando siguiente recupera los registros para todos los contenedores que se ejecutan en el pod denominado `mssql-storage-pool-default-0` y la envía a un nombre de archivo `pod-logs.txt`:

   ```cmd
   kubectl logs mssql-storage-pool-default-0 --all-containers=true -n <your-cluster-name> > pod-logs.txt
   ```

1. Revise los servicios de clúster durante y después de una implementación con el siguiente comando:

   ```cmd
   kubectl get svc -n <your-cluster-name>
   ```

   Estos servicios admiten conexiones internas y externas al clúster de macrodatos. Para las conexiones externas, se usan los siguientes servicios:

   | ssNoVersion | Descripción |
   |---|---|
   | **endpoint-master-pool** | Proporciona acceso a la instancia maestra.<br/>(**EXTERNAL-IP, 31433** y **SA** usuario) |
   | **endpoint-controller** | Es compatible con las herramientas y los clientes que administran el clúster. |
   | **endpoint-service-proxy** | Proporciona acceso a la [Portal de administración de clúster](cluster-admin-portal.md).<br/>(https://**EXTERNAL-IP**:30777/portal)|
   | **endpoint-security** | Proporciona acceso a la puerta de enlace de Spark o HDFS.<br/>(**EXTERNAL-IP** y **raíz** usuario) |

1. Use la [Portal de administración de clúster](cluster-admin-portal.md) para supervisar la implementación en el **implementación** ficha. Tendrá que esperar el **proxy de servicio de punto de conexión** que se inicie antes de acceder a este portal, por lo que no estará disponible al principio de una implementación de servicio.

> [!TIP]
> Para obtener más información sobre cómo solucionar problemas del clúster, consulte [comandos Kubectl para la supervisión y solución de problemas de clústeres de SQL Server macrodatos](cluster-troubleshooting-commands.md).

## <a name="next-steps"></a>Pasos siguientes

Pruebe algunas de las nuevas capacidades y aprenda [para usar cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md).
