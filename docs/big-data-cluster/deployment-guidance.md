---
title: Guía para la implementación
titleSuffix: SQL Server big data clusters
description: Aprenda a implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versión preliminar) en Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1520254a8a7817db612bf5e42706113495a832de
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652354"
---
# <a name="how-to-deploy-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-kubernetes"></a>Cómo realizar la [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] implementación en Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El clúster de macrodatos de SQL Server se implementa como contenedores de Docker en un clúster de Kubernetes. Esta es una introducción a los pasos de instalación y configuración:

- Configure un clúster de Kubernetes en una sola máquina virtual, un clúster de máquinas virtuales o en Azure Kubernetes Service (AKS).
- Instale la herramienta de configuración de clúster **azdata** en el equipo cliente.
- Implemente un clúster de macrodatos de SQL Server en un clúster de Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>Instalación de las herramientas de macrodatos de SQL Server 2019

Antes de implementar un clúster de macrodatos de SQL Server 2019, [instale primero las herramientas de macrodatos](deploy-big-data-tools.md):

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Extensión de SQL Server 2019**

## <a id="prereqs"></a> Requisitos previos de Kubernetes

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]requiere una versión mínima de Kubernetes de al menos v 1.10 para el servidor y el cliente (kubectl).

> [!NOTE]
> Tenga en cuenta que las versiones de Kubernetes del cliente y el servidor deben ser la versión secundaria +1 o -1. Para obtener más información, consulte [Notas de la versión de Kubernetes y directiva de SKU de sesgo de versión](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a> Configuración del clúster de Kubernetes

Si ya tiene un clúster de Kubernetes que cumple los requisitos previos anteriores, puede ir directamente al [paso de implementación](#deploy). En esta sección se da por supuesto que tiene un conocimiento básico de los conceptos de Kubernetes.  Para obtener información detallada sobre Kubernetes, consulte la [documentación de Kubernetes](https://kubernetes.io/docs/home).

Puede optar por implementar Kubernetes de tres maneras:

| Implementar Kubernetes en: | Descripción | Vínculo |
|---|---|---|
| **Azure Kubernetes Services (AKS)** | Un servicio de contenedor de Kubernetes administrado en Azure. | [Instrucciones](deploy-on-aks.md) |
| **Varias máquinas (kubeadm)** | Un clúster de Kubernetes implementado en máquinas físicas o virtuales mediante **kubeadm**. | [Instrucciones](deploy-with-kubeadm.md) |
| **Minikube** | Un clúster de Kubernetes de un solo nodo en una máquina virtual. | [Instrucciones](deploy-on-minikube.md) |

> [!TIP]
> También puede crear un script de la implementación de AKS y un clúster de macrodatos en un único paso. Para obtener más información, vea cómo realizar este procedimiento en un [script de Python](quickstart-big-data-cluster-deploy.md) o en un [cuaderno](deploy-notebooks.md) de Azure Data Studio.

### <a name="verify-kubernetes-configuration"></a>Comprobación de la configuración de Kubernetes

Ejecute el comando **kubectl** para ver la configuración del clúster. Asegúrese de que kubectl apunta al contexto de clúster correcto.

```bash
kubectl config view
```

Después de haber configurado el clúster de Kubernetes, puede continuar con la implementación de un nuevo clúster de macrodatos de SQL Server. Si va a actualizar desde una versión anterior, consulte [Cómo actualizar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deployment-upgrade.md).

## <a id="deploy"></a> Información general sobre la implementación

La mayoría de la configuración del clúster de macrodatos se define en un archivo de configuración de implementación JSON. Puede usar un perfil de implementación predeterminado para AKS, `kubeadm`o `minikube`, o bien puede personalizar su propio archivo de configuración de implementación para usarlo durante la configuración. Por motivos de seguridad, la configuración de autenticación se pasa mediante variables de entorno.

En las secciones siguientes se proporcionan más detalles sobre cómo configurar las implementaciones del clúster de macrodatos, así como ejemplos de personalizaciones comunes. Además, puede editar en todo momento el archivo de configuración de implementación personalizado con un editor (por ejemplo, VS Code).

## <a id="configfile"></a> Configuraciones predeterminadas

Las opciones de implementación del clúster de macrodatos se definen en archivos de configuración JSON. Existen tres perfiles de implementación estándar con valores de configuración predeterminados para entornos de desarrollo y pruebas:

| Perfil de implementación | Entorno de Kubernetes |
|---|---|
| **aks-dev-test** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test** | Varias máquinas (kubeadm) |
| **minikube-dev-test** | minikube |

Puede implementar un clúster de macrodatos al ejecutar **azdata bdc create**. Esto le pedirá que elija una de las configuraciones predeterminadas y después le guiará por la implementación.

La primera vez que ejecute `azdata`, debe incluir `--accept-eula=yes` para aceptar el contrato de licencia para el usuario final (CLUF).

```bash
azdata bdc create --accept-eula=yes
```

En este escenario, se le pide la configuración que no forme parte de la configuración predeterminada, como las contraseñas. 

> [!IMPORTANT]
> El nombre predeterminado del clúster de macrodatos es **mssql-cluster**. Es importante saberlo para ejecutar cualquiera de los comandos de **kubectl** que especifican el espacio de nombres de Kubernetes con el parámetro `-n`.

## <a id="customconfig"></a> Configuraciones personalizadas

También puede personalizar su propio perfil de configuración de implementación. Puede hacerlo mediante los pasos siguientes:

1. Comience con uno de los perfiles de implementación estándar que coincidan con su entorno de Kubernetes. Puede usar el comando **azdata bdc config list** para enumerarlos:

   ```bash
   azdata bdc config list
   ```

1. Para personalizar la implementación, cree una copia del perfil de implementación con el comando **azdata bdc config init**. Por ejemplo, el siguiente comando crea una copia de los archivos de configuración de implementación de **aks-dev-test** en un directorio de destino denominado `custom`:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > `--target` especifica un directorio que contiene los archivos de configuración, **cluster.json** y **control.json**, en función del parámetro `--source`.

1. Para personalizar la configuración del perfil de configuración de implementación, puede editar el archivo de configuración de implementación en una herramienta adecuada para editar archivos JSON, como VS Code. Para la automatización con scripts, también puede editar el perfil de implementación personalizado con el comando **azdata bdc config**. Por ejemplo, el comando siguiente modifica un perfil de implementación personalizado para cambiar el nombre del clúster implementado del valor predeterminado (**mssql-cluster**) a **test-cluster**:  

   ```bash
   azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
   ```
   
> [!TIP]
> También puede pasar el nombre del clúster en el momento de la implementación con el parámetro *--name* del comando *azdata create bdc*. Los parámetros del comando tienen prioridad sobre los valores de los archivos de configuración.

   > Una herramienta útil para buscar rutas de acceso JSON es [JSONPath Online Evaluator](https://jsonpath.com/).

   Además de pasar pares clave-valor, también puede proporcionar valores JSON insertados o pasar archivos de revisión JSON. Para obtener más información, vea [Configuración de opciones de implementación para clústeres de macrodatos](deployment-custom-configuration.md).

1. Después, pase el archivo de configuración personalizado a **azdata bdc create**. Tenga en cuenta que debe establecer las [variables de entorno](#env) necesarias; de lo contrario, se le pedirán los valores:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> Para obtener más información sobre la estructura de un archivo de configuración de implementación, vea la [Referencia del archivo de configuración de implementación](reference-deployment-config.md). Para consultar más ejemplos de configuración, vea [Configuración de opciones de implementación para clústeres de macrodatos](deployment-custom-configuration.md).

## <a id="env"></a> Variables de entorno

Las siguientes variables de entorno se usan para la configuración de seguridad que no se almacena en un archivo de configuración de implementación. Tenga en cuenta que la configuración de Docker, excepto las credenciales, se puede establecer en el archivo de configuración.

| Variable de entorno | Requisito |Descripción |
|---|---|---|
| **CONTROLLER_USERNAME** | Obligatorio |Nombre de usuario del administrador del clúster. |
| **CONTROLLER_PASSWORD** | Obligatorio |Contraseña del administrador del clúster. |
| **MSSQL_SA_PASSWORD** | Obligatorio |Contraseña del usuario de SA de la instancia maestra de SQL. |
| **KNOX_PASSWORD** | Obligatorio |Contraseña del usuario de Knox. |
| **ACCEPT_EULA**| Obligatorio para el primer uso de `azdata`| No requiere ningún valor. Cuando se establece como una variable de entorno, aplica el CLUF a SQL Server y `azdata`. Si no se establece como variable de entorno, puede incluir `--accept-eula` en el primer uso del comando `azdata`.|
| **DOCKER_USERNAME** | Opcional | Nombre de usuario para acceder a las imágenes de contenedor en caso de que se almacenen en un repositorio privado. Consulte el tema [Implementaciones sin conexión](deploy-offline.md) para obtener más información sobre cómo usar un repositorio privado de Docker para la implementación del clúster de macrodatos.|
| **DOCKER_PASSWORD** | Opcional |Contraseña para acceder al repositorio privado anterior. |

Estas variables de entorno se deben establecer antes de llamar a **azdata bdc create**. Si no se establece ninguna variable, se le pedirá que lo haga.

En el ejemplo siguiente se muestra cómo establecer las variables de entorno para Linux (Bash) y Windows (PowerShell):

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
```

Después de establecer las variables de entorno, debe ejecutar `azdata bdc create` para desencadenar la implementación. En este ejemplo se usa el perfil de configuración de clúster creado anteriormente:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

Tenga en cuenta las directrices siguientes:

- Asegúrese de incluir la contraseña entre comillas dobles si contiene algún carácter especial. Puede establecer **MSSQL_SA_PASSWORD** en el valor que quiera, pero asegúrese de que la contraseña sea suficientemente compleja y no use los caracteres `!`, `&` ni `'`. Tenga en cuenta que los delimitadores de comillas dobles solo funcionan en los comandos de Bash.
- El inicio de sesión de **SA** es un administrador del sistema en la instancia maestra de SQL Server que se crea durante la configuración. Después de crear el contenedor de SQL Server, la variable de entorno **MSSQL_SA_PASSWORD** especificada se reconoce mediante la ejecución de `echo $MSSQL_SA_PASSWORD` en el contenedor. Por motivos de seguridad, cambie la contraseña de administrador del sistema según los procedimientos recomendados que se documentan [aquí](../linux/quickstart-install-connect-docker.md#sapassword).

## <a id="unattended"></a> Instalación desatendida

En una implementación desatendida, debe establecer todas las variables de entorno necesarias, usar un archivo de configuración y llamar al comando `azdata bdc create` con el parámetro `--accept-eula yes`. En los ejemplos de la sección anterior se muestra la sintaxis de una instalación desatendida.

## <a id="monitor"></a> Supervisión de la implementación

Durante el arranque del clúster, la ventana de comandos del cliente generará el estado de la implementación. Durante el proceso de implementación, debería ver una serie de mensajes en los que está esperando el pod del controlador:

```output
Waiting for cluster controller to start.
```

Después de 15 a 30 minutos, se le notificará que el pod del controlador se está ejecutando:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> La implementación completa puede tardar mucho tiempo debido al tiempo necesario para descargar las imágenes de contenedor de los componentes del clúster de macrodatos. Pero no debería tardar muchas horas. Si tiene problemas con la implementación, consulte [supervisión y solución de problemas [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](cluster-troubleshooting-commands.md).

Cuando finalice la implementación, la salida le notificará que se ha realizado correctamente:

```output
Cluster deployed successfully.
```

> [!TIP]
> El nombre predeterminado del clúster de macrodatos implementado es `mssql-cluster` a menos que una configuración personalizada lo haya modificado.

## <a id="endpoints"></a> Recuperación de puntos de conexión

Una vez que el script de implementación se haya completado correctamente, puede usar los siguientes pasos para obtener las direcciones IP de los puntos de conexión externos del clúster de macrodatos.

1. Después de la implementación, busque la dirección IP del punto de conexión del controlador desde la salida estándar de la implementación o al examinar la salida de EXTERNAL-IP del siguiente comando de **kubectl**:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Si no ha cambiado el nombre predeterminado durante la implementación, use `-n mssql-cluster` en el comando anterior. **mssql-cluster** es el nombre predeterminado del clúster de macrodatos.

1. Inicie sesión en el clúster de macrodatos con [azdata login](reference-azdata.md). Establezca el parámetro **--controller-endpoint** en la dirección IP externa del punto de conexión del controlador.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique el nombre de usuario y la contraseña que ha configurado para el controlador (CONTROLLER_USERNAME y CONTROLLER_PASSWORD) durante la implementación.

1. Ejecute [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) para obtener una lista con una descripción de cada punto de conexión y los valores correspondientes de dirección IP y puerto. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   En la lista siguiente, se muestra un resultado de ejemplo de este comando:

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

También puede obtener todos los puntos de conexión de servicio implementados para el clúster si ejecuta el siguiente comando de **kubectl**:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

Si usa minikube, debe ejecutar el siguiente comando para obtener la dirección IP a la que debe conectarse. Además de la dirección IP, especifique el puerto del punto de conexión al que debe conectarse.

```bash
minikube ip
```

## <a id="status"></a> Comprobación del estado del clúster

Después de la implementación, puede comprobar el estado del clúster con el comando [azdata bdc status show](reference-azdata-bdc-status.md).

```bash
azdata bdc status show -o table
```

> [!TIP]
> Para ejecutar los comandos de estado, primero necesita iniciar sesión con el comando **azdata login**, que se ha mostrado en la sección de puntos de conexión anterior.

Este es un resultado de ejemplo de este comando:

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

Además de este estado de resumen, también puede obtener un estado más detallado con los siguientes comandos:

- [azdata bdc control status](reference-azdata-bdc-control-status.md)
- [azdata bdc pool status](reference-azdata-bdc-pool-status.md)

La salida de estos comandos contiene URL a los paneles de Kibana y Grafana para consultar un análisis más detallado.

Además de usar **azdata**, también puede utilizar Azure Data Studio para buscar información de los puntos de conexión y el estado. Para obtener más información sobre cómo ver el estado del clúster con **azdata** y Azure Data Studio, consulte [Procedimiento para ver el estado de un clúster de macrodatos](view-cluster-status.md).

## <a id="connect"></a> Conexión al clúster

Para obtener más información sobre cómo conectarse al clúster de macrodatos, consulte [Conexión a un clúster de macrodatos de SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la implementación del clúster de macrodatos, consulte los siguientes recursos:

- [Configuración de opciones de implementación para clústeres de macrodatos](deployment-custom-configuration.md)
- [Realización de una implementación sin conexión de un clúster de macrodatos de SQL Server](deploy-offline.md)
- [Taller: Arquitectura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] de Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
