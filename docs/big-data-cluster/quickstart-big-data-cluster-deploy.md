---
title: Implementar el clúster de macrodatos de SQL Server | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: quickstart
ms.prod: sql
ms.openlocfilehash: c25474a30ace6ed6e1ab0560f1b3746a071690ef
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51697043"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Inicio rápido: Implementación de clúster de macrodatos de SQL Server en Azure Kubernetes Service (AKS)

Instale el clúster de macrodatos de SQL Server en AKS en una configuración predeterminada adecuada para entornos de desarrollo y pruebas. Además de una instancia de SQL Master, el clúster incluye dos instancias del grupo de almacenamiento, una instancia del grupo de datos y proceso de una instancia del grupo. Datos se guardan con volúmenes persistentes de Kubernetes que usan clases de almacenamiento predeterminada AKS. Para personalizar aún más la configuración, consulte las variables de entorno en [instrucciones de implementación](deployment-guidance.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Requisitos previos

Este inicio rápido requiere que ya ha configurado un clúster de AKS con una versión mínima de v1.10. Para obtener más información, consulte el [implementar en AKS](deploy-on-aks.md) guía.

En el equipo que está usando para ejecutar los comandos para instalar el clúster de macrodatos de SQL Server, instale [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). Clúster de macrodatos de SQL Server requiere una versión de 1,10 mínima de Kubernetes, de servidor y cliente (kubectl). Para instalar kubectl, consulte [instalar kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl). 

Para instalar el **mssqlctl** herramienta CLI para administrar los datos grandes de SQL Server del clúster en el equipo cliente, primero debe instalar [Python](https://www.python.org/downloads/) v3.0 versión mínima y [pip3](https://pip.pypa.io/en/stable/installing/). `pip` ya está instalada si está utilizando una versión de Python de al menos 3.4 descargados de [python.org](https://www.python.org/).

## <a name="verify-aks-configuration"></a>Comprobar la configuración de AKS

Una vez implementado el clúster de AKS, puede ejecutar el siguiente comando kubectl para ver la configuración del clúster. Asegúrese de que kubectl apunta al contexto de clúster correcto.

```bash
kubectl config view
```

## <a name="install-mssqlctl-cli-management-tool"></a>Instalar la herramienta de administración de CLI mssqlctl

Ejecute el siguiente comando para instalar **mssqlctl** herramienta en el equipo cliente. El comando funciona desde un Windows y un cliente Linux, pero asegúrese de que se está ejecutando desde una ventana de cmd que se ejecuta con privilegios administrativos en Windows o un prefijo con `sudo` en Linux:

```
pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.1 mssqlctl  
```

> [!IMPORTANT]
> Si ha instalado una versión anterior, debe eliminar el clúster *antes* actualizar **mssqlctl** e instalar la nueva versión. Para obtener más información, consulte [actualizar a una nueva versión](deployment-guidance.md#upgrade).

> [!TIP]
> Si **mssqlctl** no se instaló correctamente, revise los requisitos previos en el artículo [instalar mssqlctl](deployment-guidance.md#mssqlctl).

## <a name="define-environment-variables"></a>Definir variables de entorno

Establecer las variables de entorno necesarias para implementar el clúster de macrodatos ligeramente es diferente dependiendo de si se utiliza el cliente de Windows o Linux y macOS.  Elija los pasos siguientes, dependiendo del sistema operativo que esté utilizando.

Antes de continuar, tenga en cuenta las siguientes directrices importantes:

- En el [ventana de comandos](https://docs.microsoft.com/visualstudio/ide/reference/command-window), se incluyen entre comillas en las variables de entorno. Si utiliza comillas para encapsular una contraseña, se incluyen las comillas en la contraseña.
- En bash, no se incluyen entre comillas en la variable. Nuestros ejemplos utilizan comillas dobles `"`.
- Puede establecer la contraseña de las variables de entorno que prefiera, pero asegúrese de que son lo suficientemente complejos y no utilizar la `!`, `&`, o `'` caracteres.
- La versión de CTP 2.1, no cambie los puertos predeterminados.
- El `sa` cuenta es un administrador del sistema en la instancia maestra de SQL Server que se crea durante la instalación. Después de crear el contenedor de SQL Server, la variable de entorno `MSSQL_SA_PASSWORD` especificada se reconoce mediante la ejecución de `echo $MSSQL_SA_PASSWORD` en el contenedor. Por motivos de seguridad, cambiar su `sa` contraseña según los procedimientos recomendados que se documentan [aquí](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Inicialice las variables de entorno siguientes.  Son necesarios para implementar un clúster de macrodatos:

### <a name="windows"></a>Windows

Mediante una ventana de comandos (no PowerShell), configure las siguientes variables de entorno:

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=aks

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

### <a name="linuxmacos"></a>Linux y macOS

Inicialice las variables de entorno siguientes:

```bash
export ACCEPT_EULA="Y"
export CLUSTER_PLATFORM="aks"

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

> [!NOTE]
> Durante la versión preliminar pública limitada, se proporcionan las credenciales de Docker para descargar las imágenes de clúster de SQL Server datos de gran tamaño a cada cliente por Microsoft. Para solicitar acceso, registrar [aquí](https://aka.ms/eapsignup)y especifique su interés para probar los clústeres grandes de datos de SQL Server.

## <a name="deploy-a-big-data-cluster"></a>Implementar un clúster de macrodatos

Para implementar un clúster de macrodatos de 2019 CTP 2.1 de SQL Server en el clúster de Kubernetes, ejecute el siguiente comando:

```bash
mssqlctl create cluster <name of your cluster>
```

> [!NOTE]
> El nombre del clúster debe ser solo alfanuméricos caracteres en minúsculas, sin espacios en blanco. Todos los artefactos de Kubernetes para el clúster de macrodatos se creará en un espacio de nombres con el mismo nombre que el clúster de nombre especificado.


La ventana de comandos o el shell devuelve el estado de implementación. También puede comprobar el estado de implementación mediante la ejecución de estos comandos en una ventana cmd diferentes:

```bash
kubectl get all -n <name of your cluster>
kubectl get pods -n <name of your cluster>
kubectl get svc -n <name of your cluster>
```

Puede ver un estado y la configuración para cada pod más granulares mediante la ejecución:
```bash
kubectl describe pod <pod name> -n <name of your cluster>
```

Una vez que se está ejecutando el pod del controlador, puede usar el Portal de administración de clúster para supervisar la implementación. Se puede acceder al portal mediante el número de puerto y dirección IP externo para la `service-proxy-lb` (por ejemplo: **https://\<ip-address\>: 30777**). Las credenciales de acceso al portal de administración es los valores de `CONTROLLER_USERNAME` y `CONTROLLER_PASSWORD` variables de entorno proporcionadas anteriormente.

Puede obtener la dirección IP del servicio de proxy de servicio de equilibrador de carga, ejecute este comando en una ventana cmd o bash:

```bash
kubectl get svc service-proxy-lb -n <name of your cluster>
```

> [!NOTE]
> Verá una advertencia de seguridad al obtener acceso a la página web, puesto que estamos usando certificados SSL generados automáticamente. En futuras versiones, se proporcionará la capacidad para proporcionar sus propios certificados autofirmados.
 

## <a name="connect-to-the-big-data-cluster"></a>Conéctese al clúster de macrodatos

Después de que el script de implementación se ha completado correctamente, puede obtener la dirección IP de la instancia principal de SQL Server y los puntos de conexión de Spark o HDFS siguiendo los pasos descritos a continuación. Todos los puntos de conexión de clúster se muestran en la sección de puntos de conexión de servicio en el Portal de administración de clúster, así como para facilitar su consulta.

Azure proporciona el servicio del equilibrador de carga de Azure en AKS. Ejecute el siguiente comando en una ventana de símbolo o ventana de bash:

```bash
kubectl get svc service-master-pool-lb -n <name of your cluster>
kubectl get svc service-security-lb -n <name of your cluster>
```

Busque el **External-IP** valor que se asigna a los servicios. Conectarse a la instancia principal de SQL Server con la dirección IP para el `service-master-pool-lb` en el puerto 31433 (p. ej.:  **\<ip-address\>, 31433**) y para el punto del clúster de macrodatos de SQL Server con la IP externa para el `service-security-lb` servicio.   Que el punto final de clúster de macrodatos es donde puede interactuar con HDFS y enviar trabajos de Spark a través de Knox.

## <a name="sample-deployment-script"></a>Script de implementación de ejemplo

Para un script de python de ejemplo que implementa el clúster de macrodatos AKS y SQL Server, vea [implementar un clúster de macrodatos en Azure Kubernetes Service (AKS) de SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

## <a name="next-steps"></a>Pasos siguientes

Ahora que está implementado el clúster de macrodatos de SQL Server, pruebe algunas de las nuevas capacidades:

> [!div class="nextstepaction"]
> [Uso de cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md)
