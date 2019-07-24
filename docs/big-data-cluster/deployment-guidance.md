---
title: Guía para la implementación
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo implementar clústeres de macrodatos de SQL Server 2019 (versión preliminar) en Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e6f2eefd37c45753e3051722448b80d88712df26
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419421"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Cómo implementar clústeres de macrodatos SQL Server en Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server clúster de macrodatos se implementa como contenedores de Docker en un clúster de Kubernetes. Esta es una introducción a los pasos de instalación y configuración:

- Configure un clúster de Kubernetes en una sola máquina virtual, un clúster de máquinas virtuales o en Azure Kubernetes Service (AKS).
- Instale la herramienta de configuración de clúster **azdata** en el equipo cliente.
- Implementar un clúster de macrodatos de SQL Server en un clúster de Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>Instalación de herramientas de macrodatos SQL Server 2019

Antes de implementar un clúster de Big Data SQL Server 2019, [Instale primero las herramientas de macrodatos](deploy-big-data-tools.md):

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server extensión 2019**

## <a id="prereqs"></a>Requisitos previos de Kubernetes

SQL Server los clústeres de macrodatos requieren una versión mínima de Kubernetes de al menos v 1.10 para el servidor y el cliente (kubectl).

> [!NOTE]
> Tenga en cuenta que las versiones de Kubernetes de cliente y de servidor deben estar dentro de la versión de + 1 o-1 secundaria. Para obtener más información, consulte [notas de la versión de Kubernetes y Directiva de SKU de sesgo de versión)](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a>Configuración de clúster de Kubernetes

Si ya tiene un clúster de Kubernetes que cumple los requisitos previos anteriores, puede ir directamente al [paso de implementación](#deploy). En esta sección se da por supuesto un conocimiento básico de los conceptos de Kubernetes.  Para obtener información detallada sobre Kubernetes, consulte la [documentación de Kubernetes](https://kubernetes.io/docs/home).

Puede optar por implementar Kubernetes de tres maneras:

| Implementar Kubernetes en: | Descripción | Vínculo |
|---|---|---|
| **Azure Kubernetes Services (AKS)** | Un servicio de contenedor de Kubernetes administrado en Azure. | [Las](deploy-on-aks.md) |
| **Varios equipos (kubeadm)** | Un clúster de Kubernetes implementado en máquinas físicas o virtuales mediante **kubeadm** | [Las](deploy-with-kubeadm.md) |
| **Minikube** | Un clúster de Kubernetes de un solo nodo en una máquina virtual. | [Las](deploy-on-minikube.md) |

> [!TIP]
> Para ver un script de Python de ejemplo que implementa tanto AKS como un clúster de macrodatos SQL Server en un [solo paso, consulte Inicio rápido: Implemente SQL Server clúster de Big Data en Azure Kubernetes Service (](quickstart-big-data-cluster-deploy.md)AKS).

### <a name="verify-kubernetes-configuration"></a>Comprobar la configuración de Kubernetes

Ejecute el comando **kubectl** para ver la configuración del clúster. Asegúrese de que kubectl apunta al contexto de clúster correcto.

```bash
kubectl config view
```

Después de configurar el clúster de Kubernetes, puede continuar con la implementación de un nuevo SQL Server clúster de Big Data. Si va a actualizar desde una versión anterior, consulte [Cómo actualizar](deployment-upgrade.md)los clústeres de macrodatos de SQL Server.

## <a id="deploy"></a>Información general sobre la implementación

La mayoría de la configuración del clúster de macrodatos se define en un archivo de configuración de implementación JSON. Puede usar un perfil de implementación predeterminado para AKS, `kubeadm`o `minikube` , o puede personalizar su propio archivo de configuración de implementación para usarlo durante la instalación. Por motivos de seguridad, la configuración de autenticación se pasa a través de variables de entorno.

En las secciones siguientes se proporcionan más detalles sobre cómo configurar las implementaciones de clúster de Big Data, así como ejemplos de personalizaciones comunes. Además, siempre puede editar el archivo de configuración de implementación personalizado con un editor como VS Code por ejemplo.

## <a id="configfile"></a>Configuraciones predeterminadas

Las opciones de implementación de clúster de Big Data se definen en archivos de configuración de JSON. Existen tres perfiles de implementación estándar con valores predeterminados para entornos de desarrollo y pruebas:

| Perfil de implementación | Entorno de Kubernetes |
|---|---|
| **aks-dev-test** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test** | Varios equipos (kubeadm) |
| **minikube-dev-test** | Minikube |

Puede implementar un clúster de Big Data mediante la ejecución de **azdata BDC Create**. Esto le pedirá que elija una de las configuraciones predeterminadas y, a continuación, le guiará a través de la implementación.

La primera vez que ejecute `azdata` , debe incluir `--accept-eula` para aceptar el contrato de licencia para el usuario final (CLUF).

```bash
azdata bdc create --accept-eula
```

En este escenario, se le solicitará cualquier configuración que no forme parte de la configuración predeterminada, como contraseñas. 

> [!NOTE]
> A partir de SQL Server 2019 CTP 3,2, ya no tiene que ser miembro de el [programa de adopción temprana](https://aka.ms/eapsignup) SQL Server 2019 para experimentar las versiones preliminares del clúster de Big Data.

> [!IMPORTANT]
> El nombre predeterminado del clúster de Big Data es **MSSQL-Cluster**. Es importante saber con el fin de ejecutar cualquiera de los comandos **kubectl** que especifican el espacio de nombres Kubernetes `-n` con el parámetro.

## <a id="customconfig"></a>Configuraciones personalizadas

También es posible personalizar su propio perfil de configuración de implementación. Puede hacerlo con los pasos siguientes:

1. Comience con uno de los perfiles de implementación estándar que coincidan con el entorno de Kubernetes. Puede usar el comando **azdata de configuración de BDC** para enumerarlos:

   ```bash
   azdata bdc config list
   ```

1. Para personalizar la implementación, cree una copia del perfil de implementación con el comando **azdata BDC config init** . Por ejemplo, el siguiente comando crea una copia de los archivos de configuración de implementación de **AKS-dev-test** en un `custom`directorio de destino denominado:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

   azdata
   > Especifica un directorio que contiene los archivos de configuración, **cluster. JSON** y **control. JSON**, basados en el `--source` parámetro. `--target`

1. Para personalizar la configuración del perfil de configuración de implementación, puede editar el archivo de configuración de implementación en una herramienta que sea adecuada para editar archivos JSON, como VS Code. Para la automatización con scripts, también puede editar el perfil de implementación personalizado mediante el comando **azdata de BDC** . Por ejemplo, el comando siguiente modifica un perfil de implementación personalizado para cambiar el nombre del clúster implementado del valor predeterminado (**MSSQL-Cluster**) a **Test-Cluster**:  

   ```bash
   azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
   ```

   > Una herramienta útil para buscar rutas JSON es el [evaluador en línea JSONPath](https://jsonpath.com/).

   Además de pasar pares clave-valor, también puede proporcionar valores JSON en línea o pasar archivos de revisión JSON. Para obtener más información, vea [configurar las opciones de implementación para los clústeres de Big Data](deployment-custom-configuration.md).

1. Después, pase el archivo de configuración personalizado a **azdata BDC Create**. Tenga en cuenta que debe establecer las [variables de entorno](#env)necesarias; de lo contrario, se le pedirán los valores siguientes:

   ```bash
   azdata bdc create --config-profile custom --accept-eula yes
   ```

> Para obtener más información sobre la estructura de un archivo de configuración de implementación, vea la [Referencia del archivo de configuración de implementación](reference-deployment-config.md). Para obtener más ejemplos de configuración, vea [configurar las opciones de implementación para clústeres de macrodatos](deployment-custom-configuration.md).

## <a id="env"></a>Variables de entorno

Las siguientes variables de entorno se usan para la configuración de seguridad que no se almacena en un archivo de configuración de implementación. Tenga en cuenta que la configuración de Docker, excepto las credenciales, se puede establecer en el archivo de configuración.

| Variable de entorno | Requisito |Descripción |
|---|---|---|
| **CONTROLLER_USERNAME** | Obligatorio |El nombre de usuario para el administrador de clústeres. |
| **CONTROLLER_PASSWORD** | Obligatorio |Contraseña del administrador de clústeres. |
| **MSSQL_SA_PASSWORD** | Obligatorio |La contraseña del usuario SA para la instancia maestra de SQL. |
| **KNOX_PASSWORD** | Obligatorio |Contraseña del usuario Knox. |
| **ACCEPT_EULA**| Obligatorio para el primer uso de`azdata`| No requiere ningún valor. Cuando se establece como una variable de entorno, aplica el CLUF a SQL Server `azdata`y. Si no se establece como variable de entorno, se `--accept-eula` puede incluir en el primer `azdata` uso del comando.|
| **DOCKER_USERNAME** | Opcional | El nombre de usuario para tener acceso a las imágenes de contenedor en caso de que se almacenen en un repositorio privado. Consulte el tema sobre [implementaciones sin conexión](deploy-offline.md) para más información sobre cómo usar un repositorio privado de Docker para la implementación de clúster de macrodatos.|
| **DOCKER_PASSWORD** | Opcional |La contraseña para tener acceso al repositorio privado anterior. |

Estas variables de entorno se deben establecer antes de llamar a **azdata BDC Create**. Si no se establece ninguna variable, se le pedirá.

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

Después de establecer las variables de entorno, debe `azdata bdc create` ejecutar para desencadenar la implementación. En este ejemplo se usa el perfil de configuración de clúster creado anteriormente:

```bash
azdata bdc create --config-profile custom --accept-eula yes
```

Tenga en cuenta las siguientes directrices:

- Asegúrese de que ajusta la contraseña entre comillas dobles si contiene algún carácter especial. Puede establecer el valor de **MSSQL_SA_PASSWORD** en el que desee, pero asegúrese de que la contraseña es suficientemente compleja y no `!`use `&` los `'` caracteres, o. Tenga en cuenta que los delimitadores de comillas dobles solo funcionan en comandos de Bash.
- El inicio de sesión **SA** es un administrador del sistema en la SQL Server instancia maestra que se crea durante la instalación. Después de crear el contenedor de SQL Server, la variable de entorno **MSSQL_SA_PASSWORD** que especificó se puede `echo $MSSQL_SA_PASSWORD` detectar ejecutando en el contenedor. Por motivos de seguridad, cambie la contraseña de SA según los procedimientos recomendados que se documentan [aquí](../linux/quickstart-install-connect-docker.md#sapassword).

## <a id="unattended"></a>Instalación desatendida

En una implementación desatendida, debe establecer todas las variables de entorno necesarias, usar un archivo de configuración y llamar `azdata bdc create` al comando con `--accept-eula yes` el parámetro. En los ejemplos de la sección anterior se muestra la sintaxis de una instalación desatendida.

## <a id="monitor"></a>Supervisión de la implementación

Durante el arranque del clúster, la ventana de comandos del cliente generará el estado de implementación. Durante el proceso de implementación, debería ver una serie de mensajes en los que está esperando el POD del controlador:

```output
Waiting for cluster controller to start.
```

En 15 o 30 minutos, se le notificará que el POD del controlador se está ejecutando:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> Toda la implementación puede tardar mucho tiempo debido al tiempo necesario para descargar las imágenes de contenedor de los componentes del clúster de Big Data. Sin embargo, no debería tardar varias horas. Si tiene problemas con la implementación, consulte [supervisión y solución de problemas](cluster-troubleshooting-commands.md)de clústeres de macrodatos SQL Server.

Cuando finalice la implementación, la salida le notificará que se ha realizado correctamente:

```output
Cluster deployed successfully.
```

> [!TIP]
> El nombre predeterminado para el clúster de Big Data implementado es a menos que sea `mssql-cluster` modificado por una configuración personalizada.

## <a id="endpoints"></a>Recuperación de puntos de conexión

Una vez que el script de implementación se haya completado correctamente, puede obtener las direcciones IP de los puntos de conexión externos para el clúster de Big Data siguiendo estos pasos.

1. Después de la implementación, busque la dirección IP del punto de conexión del controlador desde la salida estándar de implementación o examine la salida de IP externa del siguiente comando de **kubectl** :

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Si no cambió el nombre predeterminado durante la implementación, use `-n mssql-cluster` en el comando anterior. **MSSQL-Cluster** es el nombre predeterminado para el clúster de Big Data.

1. Inicie sesión en el clúster de Big Data con el [Inicio de sesión de azdata](reference-azdata.md). Establezca el parámetro **--Controller-Endpoint** en la dirección IP externa del punto de conexión del controlador.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique el nombre de usuario y la contraseña que configuró para el controlador (CONTROLLER_USERNAME y CONTROLLER_PASSWORD) durante la implementación.

1. Ejecute la [lista de puntos de conexión de BDC de azdata](reference-azdata-bdc-endpoint.md) para obtener una lista con una descripción de cada punto de conexión y sus valores de puerto y dirección IP correspondientes. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   En la lista siguiente se muestra la salida de ejemplo de este comando:

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

También puede obtener todos los puntos de conexión de servicio implementados para el clúster mediante la ejecución del siguiente comando de **kubectl** :

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

Si usa minikube, debe ejecutar el siguiente comando para obtener la dirección IP a la que debe conectarse. Además de la dirección IP, especifique el puerto del punto de conexión al que debe conectarse.

```bash
minikube ip
```

## <a id="status"></a>Comprobar el estado del clúster

Después de la implementación, puede comprobar el estado del clúster con el comando [azdata BDC status show](reference-azdata-bdc-status.md) .

```bash
azdata bdc status show -o table
```

> [!TIP]
> Para ejecutar los comandos de estado, primero debe iniciar sesión con el comando de **Inicio de sesión de azdata** , que se mostró en la sección puntos de conexión anteriores.

En el siguiente ejemplo se muestra la salida de este comando:

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

En este Resumen de estado, también puede obtener un estado más detallado con los siguientes comandos:

- [Estado de control de BDC de azdata](reference-azdata-bdc-control-status.md)
- [Estado del grupo de BDC de azdata](reference-azdata-bdc-pool-status.md)

La salida de estos comandos contiene las direcciones URL de los paneles Kibana y Grafana para un análisis más detallado.

Además de utilizar **azdata**, también puede usar Azure Data Studio para buscar los puntos de conexión y la información de estado. Para obtener más información sobre cómo ver el estado del clúster con **azdata** y Azure Data Studio, consulte [Cómo ver el estado de un clúster de Big Data](view-cluster-status.md).

## <a id="connect"></a>Conexión al clúster

Para más información sobre cómo conectarse al clúster de Big Data, consulte [conexión a un clúster de macrodatos de SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre la implementación de clúster de Big Data, consulte los siguientes recursos:

- [Configuración de las opciones de implementación de clústeres de Big Data](deployment-custom-configuration.md)
- [Realización de una implementación sin conexión de un clúster de macrodatos SQL Server](deploy-offline.md)
- [Taller Arquitectura de clústeres de macrodatos Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
