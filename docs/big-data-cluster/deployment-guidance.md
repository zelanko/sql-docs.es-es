---
title: Cómo implementar grandes de datos de SQL Server a clústeres de Kubernetes | Microsoft Docs
description: Obtenga información sobre cómo implementar clústeres de macrodatos de 2019 de SQL Server (versión preliminar) en Kubernetes.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/08/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: de19577b4a83bc10875bf56f4c0f2924828a00ea
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051187"
---
# <a name="how-to-deploy-sql-server-big-data-cluster-on-kubernetes"></a>Cómo implementar SQL Server al clúster de macrodatos en Kubernetes

Clúster de macrodatos de SQL Server se puede implementar como contenedores de docker en un clúster de Kubernetes. Se trata de una visión general de los pasos de instalación y configuración:

- Configuración de clúster de Kubernetes en una sola máquina virtual, clúster de máquinas virtuales o en Azure Kubernetes Service (AKS).
- Instalar la herramienta de configuración de clúster **mssqlctl** en el equipo cliente.
- Implementar el clúster de macrodatos de SQL Server en un clúster de Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="prereqs"></a> Requisitos previos de clúster de Kubernetes

Clúster de macrodatos de SQL Server requiere una versión de v1.10 mínimo de Kubernetes, de servidor y cliente. Para instalar una versión específica en el cliente kubectl, consulte [instalar kubectl binario mediante curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl).  Las versiones más recientes de minikube y AKS son menos 1.10. Para AKS, deberá usar `--kubernetes-version` parámetro para especificar una versión diferente de forma predeterminada.

> [!NOTE]
> Tenga en cuenta que las versiones de Kubernetes de cliente y servidor deben ser la versión secundaria + 1 o -1. Para obtener más información, consulte [Kubernetes admite versiones y componente sesgo](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

## <a id="kubernetes"></a> Instalación de clúster de Kubernetes

Si ya tiene un clúster de Kubernetes que se cumple por encima de los requisitos previos, puede ir directamente a la [paso de implementación](#deploy). En esta sección se da por supuesto un conocimiento básico de los conceptos de Kubernetes.  Para obtener información detallada sobre Kubernetes, consulte el [documentación de Kubernetes](https://kubernetes.io/docs/home).

Puede elegir implementar Kubernetes en cualquiera de estas tres maneras:

| Implementación de Kubernetes en: | Descripción |
|---|---|
| **Minikube** | Un clúster de Kubernetes de nodo único en una máquina virtual. |
| **Azure Kubernetes Service (AKS)** | Un servicio de contenedor de Kubernetes administrado en Azure. |
| **Varias máquinas** | Un clúster de Kubernetes implementado en máquinas físicas o virtuales con **kubeadm** |

Para obtener instrucciones sobre cómo configurar una de estas opciones de clúster de Kubernetes para un clúster de macrodatos de SQL Server, consulte uno de los siguientes artículos:

   - [Configurar Minikube](deploy-on-minikube.md)
   - [Configuración de Kubernetes en Azure Kubernetes Service](deploy-on-aks.md)
   - [Configuración de Kubernetes en varios equipos con kubeadm](deploy-with-kubeadm.md)
   
> [!TIP]
> Para un script de python de ejemplo que implementa el clúster de macrodatos AKS y SQL Server, vea [implementar un clúster de macrodatos en Azure Kubernetes Service (AKS) de SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

## <a id="deploy"></a> Implementar el clúster de macrodatos de SQL Server

Después de haber configurado el clúster de Kubernetes, puede continuar con la implementación de clúster de macrodatos de SQL Server. Para implementar un clúster de macrodatos en Azure con todas las configuraciones predeterminadas para un entorno de desarrollo y pruebas, siga las instrucciones de este artículo:

[Inicio rápido: Implementación de clúster de macrodatos de SQL Server en Kubernetes](quickstart-big-data-cluster-deploy.md)

Si desea personalizar la configuración del clúster de macrodatos según sus necesidades de carga de trabajo, siga el siguiente conjunto de instrucciones.

## <a name="verify-kubernetes-configuration"></a>Comprobar la configuración de kubernetes

Ejecute el **kubectl** comando para ver la configuración del clúster. Asegúrese de que kubectl apunta al contexto de clúster correcto.

```bash
kubectl config view
```

## <a id="mssqlctl"></a> Instalar mssqlctl

**mssqlctl** es una utilidad de línea de comandos escrita en Python que habilita los administradores para arrancar y administrar el clúster de macrodatos mediante las API de REST de clúster. La versión de Python mínima requerida es v3.5. También debe tener `pip` que se utiliza para descargar e instalar **mssqlctl** herramienta. 

### <a name="windows-mssqlctl-installation"></a>Instalación de Windows mssqlctl

1. En un cliente de Windows, descargue el paquete de Python necesario [ https://www.python.org/downloads/ ](https://www.python.org/downloads/). Python3.5.3 y versiones posteriores, pip3 también se instala al instalar Python. 

   > [!TIP] 
   > Al instalar Python3, seleccione esta opción para agregar Python a la ruta de acceso. Si no lo hace, puede encontrar más adelante en el que se encuentra pip3 y agregarlo manualmente a la ruta de acceso.

1. Asegúrese de que tiene la versión más reciente **solicitudes** paquete.

   ```cmd
   python -m pip install requests
   python -m pip install requests --upgrade
   ```

1. Instalar **mssqlctl** con el siguiente comando:

   ```bash
   pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
   ```

### <a name="linux-mssqlctl-installation"></a>Instalación de Linux mssqlctl

En Linux, debe instalar la **python3** y **python3-pip** paquetes y, a continuación, ejecute `sudo pip3 install --upgrade pip`. Esto instala la última versión 3.5 de Python y pip. El ejemplo siguiente muestra cómo funcionaría estos comandos para Ubuntu (si usa otra plataforma, modifique los comandos para el Administrador de paquetes):

1. Instalar los paquetes de Python necesarios:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip && /
   sudo -H pip3 install --upgrade pip
   ```

1. Asegúrese de que tiene la versión más reciente **solicitudes** paquete.

   ```bash
   sudo -H python3 -m pip install requests
   sudo -H python3 -m pip install requests --upgrade
   ```

1. Instalar **mssqlctl** con el siguiente comando:

   ```bash
   pip3 install --index-url https://private-repo.microsoft.com/python/ctp-2.0 mssqlctl
   ```

## <a name="define-environment-variables"></a>Definir variables de entorno

La configuración del clúster puede personalizarse mediante un conjunto de variables de entorno que se pasan a la `mssqlctl create cluster` comando. La mayoría de las variables de entorno es opcional con los valores predeterminados como se indica a continuación. Tenga en cuenta que hay variables de entorno como las credenciales que requieren intervención del usuario.

| Variable de entorno | Obligatorio | Valor predeterminado | Descripción |
|---|---|---|---|
| **ACCEPT_EULA** | Sí | N/D | Acepte el contrato de licencia de SQL Server (por ejemplo, ' Y').  |
| **NOMBREDECLÚSTER** | Sí | N/D | El nombre del espacio de nombres para implementar SQLServer agrupar datos de gran tamaño en Kubernetes. |
| **CLUSTER_PLATFORM** | Sí | N/D | La plataforma que se implementa el clúster de Kubernetes. Puede ser `aks`, `minikube`, `kubernetes`|
| **CLUSTER_COMPUTE_POOL_REPLICAS** | no | 1 | El número de réplicas del grupo de proceso para elaborar. En CTP2.0 solo con valores permitido es 1. |
| **CLUSTER_DATA_POOL_REPLICAS** | no | 2 | El número de datos de grupo de réplicas para elaborar. |
| **CLUSTER_STORAGE_POOL_REPLICAS** | no | 2 | El número de réplicas de grupo de almacenamiento para elaborar. |
| **DOCKER_REGISTRY** | Sí | TBD | El registro privado donde se almacenan las imágenes se usan para implementar el clúster. |
| **DOCKER_REPOSITORY** | Sí | TBD | El repositorio privado en el registro anterior donde se almacenan las imágenes.  Se requiere para la duración de la versión preliminar pública validada. |
| **DOCKER_USERNAME** | Sí | N/D | El nombre de usuario para tener acceso a las imágenes de contenedor en caso de que se almacenan en un repositorio privado. Se requiere para la duración de la versión preliminar pública validada. |
| **DOCKER_PASSWORD** | Sí | N/D | La contraseña para acceder al repositorio privado anterior. Se requiere para la duración de la versión preliminar pública validada.|
| **DOCKER_EMAIL** | Sí | N/D | El correo electrónico asociado con el repositorio privado anterior. Se requiere para la duración de la versión preliminar privada validada. |
| **DOCKER_IMAGE_TAG** | no | Más reciente | La etiqueta utilizada para etiquetar las imágenes. |
| **DOCKER_IMAGE_POLICY** | no | Always | Fuerce siempre una extracción de las imágenes.  |
| **DOCKER_PRIVATE_REGISTRY** | Sí | 1 | El período de tiempo de la versión preliminar pública validada, este valor debe establecerse en 1. |
| **CONTROLLER_USERNAME** | Sí | N/D | El nombre de usuario para el Administrador de clústeres. |
| **CONTROLLER_PASSWORD** | Sí | N/D | La contraseña para el Administrador de clústeres. |
| **KNOX_PASSWORD** | Sí | N/D | La contraseña de usuario de Knox. |
| **MSSQL_SA_PASSWORD** | Sí | N/D | La contraseña del usuario SA para la instancia principal de SQL. |
| **USE_PERSISTENT_VOLUME** | no | true | `true` Para usar notificaciones de volumen persistente de Kubernetes para el almacenamiento de pod.  `false` uso del almacenamiento efímero host para el almacenamiento de pod. Consulte la [persistencia de datos](concept-data-persistence.md) artículo para obtener más detalles. Si implementa SQL Server datos de gran tamaño de clúster de minikube y USE_PERSISTENT_VOLUME = true, debe establecer el valor de `STORAGE_CLASS_NAME=standard`. |
| **STORAGE_CLASS_NAME** | no | predeterminados | Si `USE_PERSISTENT_VOLUME` es `true` indica el nombre de la clase de almacenamiento de Kubernetes para usar. Consulte la [persistencia de datos](concept-data-persistence.md) artículo para obtener más detalles. Si implementa un clúster de macrodatos en minikube de SQL Server, el nombre de clase de almacenamiento predeterminada es diferente y se debe invalidar estableciendo `STORAGE_CLASS_NAME=standard`. |
| **MASTER_SQL_PORT** | no | 31433 | El puerto TCP/IP que escucha la instancia SQL maestra de la red pública. |
| **KNOX_PORT** | no | 30443 | El puerto TCP/IP que Knox Apache escucha en la red pública. |
| **GRAFANA_PORT** | no | 30888 | El puerto TCP/IP que escucha la aplicación de supervisión de Grafana de la red pública. |
| **KIBANA_PORT** | no | 30999 | El puerto TCP/IP que escucha la aplicación de búsqueda de registro de Kibana en la red pública. |

> [!IMPORTANT]
>1. Durante la duración de la versión preliminar privada limitada, le proporcionará las credenciales para el registro privado de Docker para usted tras la clasificación de su [registro EAP](https://aka.ms/eapsignup).
>1. Para un clúster local integrada con **kubeadm**, el valor de variable de entorno `CLUSTER_PLATFORM` es `kubernetes`. También, cuando `USE_PERSISTENT_VOLUME=true`, debe aprovisionar previamente una clase de almacenamiento de Kubernetes y pasarlo a través del uso del `STORAGE_CLASS_NAME`.
>1. Asegúrese de que incluir las contraseñas en las comillas dobles si contiene algún carácter especial. Puede establecer el MSSQL_SA_PASSWORD que prefiera, pero asegúrese de que son lo suficientemente complejos y no utilizar la `!`, `&` o `‘` caracteres. Tenga en cuenta que los delimitadores de comillas dobles solo funcionan en los comandos de bash.
>1. El nombre del clúster debe ser solo alfanuméricos caracteres en minúsculas, sin espacios en blanco. Todos los artefactos de Kubernetes (contenedores, pods, conjuntos con estado, los servicios) para el clúster se creará en un espacio de nombres con el mismo nombre que el clúster de nombre especificado.
>1. El **SA** cuenta es un administrador del sistema en la instancia maestra de SQL Server que se crea durante la instalación. Después de crear el contenedor de SQL Server, la variable de entorno MSSQL_SA_PASSWORD especificada es detectable mediante la ejecución de eco MSSQL_SA_PASSWORD $ en el contenedor. Por motivos de seguridad, cambiar la contraseña de SA según los procedimientos recomendados que se documentan [aquí](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Establecer las variables de entorno necesarias para implementar un clúster de macrodatos es diferente dependiendo de si se utiliza el cliente de Windows o Linux.  Elija los pasos siguientes, dependiendo del sistema operativo que esté utilizando.

Inicializar las variables de entorno siguientes, son necesarios para implementar el clúster:

### <a name="windows"></a>Windows

Con una ventana CMD (no PowerShell), configure las siguientes variables de entorno. No utilice comillas alrededor de los valores.

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=<minikube or aks or kubernetes>

SET CONTROLLER_USERNAME=<controller_admin_name – can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password – can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password – can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your Docker email, use the username provided by Microsoft>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linux"></a>Linux

Inicialice las variables de entorno siguientes. En bash, puede usar comillas alrededor de cada valor.

```bash
export ACCEPT_EULA=Y
export CLUSTER_PLATFORM=<minikube or aks or kubernetes>

export CONTROLLER_USERNAME="<controller_admin_name – can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password – can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password – can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your Docker email, use the username provided by Microsoft>"
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
mssqlctl create cluster <name of your cluster>
```

Durante el arranque del clúster, la ventana de comandos de cliente dará como resultado el estado de implementación. También puede comprobar el estado de implementación mediante la ejecución de estos comandos en una ventana cmd diferentes:

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

Puede ver un estado y la configuración para cada pod más granulares mediante la ejecución:
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

Una vez que se está ejecutando el pod del controlador, puede aprovechar la pestaña implementación en el Portal de administración de clúster para supervisar la implementación.

## <a id="masterip"></a> Obtener la instancia de SQL Server Master y direcciones IP del clúster de macrodatos de SQL Server

Después de que el script de implementación se ha completado correctamente, puede obtener la dirección IP de la instancia principal de SQL Server siguiendo los pasos descritos a continuación. Utilizará esta dirección IP y puerto número 31433 para conectarse a la instancia principal de SQL Server (por ejemplo:  **\<ip-address\>, 31433**). De forma similar, para la IP del clúster de SQL Server datos de gran tamaño. Todos los puntos de conexión de clúster se describen en la pestaña de extremos de servicio en el Portal de administración de clúster. Puede usar el Portal de administración de clúster para supervisar la implementación. Se puede acceder al portal mediante el número de puerto y dirección IP externo para la `service-proxy-lb` (por ejemplo: **https://\<ip-address\>: 30777**). Las credenciales de acceso al portal de administración es los valores de `CONTROLLER_USERNAME` y `CONTROLLER_PASSWORD` variables de entorno proporcionadas anteriormente.

### <a name="aks"></a>AKS

Si usa AKS, Azure proporciona el servicio del equilibrador de carga de Azure. Ejecute el siguiente comando:

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
kubectl get svc service-proxy-lb -n <name of your cluster>
```

Busque el **External-IP** valor que se asigna al servicio. Después, conéctese a la instancia principal de SQL Server con la dirección IP en el puerto 31433 (p. ej.:  **\<ip-address\>, 31433**) y al extremo de clúster de macrodatos de SQL Server mediante la IP externa para `service-security-lb` service. 

### <a name="minikube"></a>Minikube

Si usas Minikube, deberá ejecutar el siguiente comando para obtener la dirección IP que necesita para conectarse a. Además de la dirección IP, especifique el puerto para el punto de conexión que necesita para conectarse a. Para obtener todos los extremos de servicio para 

```bash
minikube ip
```

Independientemente de la plataforma usa su clúster de Kubernetes, para obtener todos los extremos de servicio implementados para el clúster, ejecute el siguiente comando:
```bash
kubectl get svc -n <name of your cluster>
```

## <a name="next-steps"></a>Pasos siguientes

Después de implementar correctamente SQL Server al clúster de macrodatos a Kubernetes, [instalar las herramientas de macrodatos](deploy-big-data-tools.md) y pruebe algunas de las nuevas capacidades y aprenda [para usar cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md).
