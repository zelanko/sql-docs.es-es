---
title: Guía para la implementación
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo implementar clústeres de macrodatos de 2019 de SQL Server (versión preliminar) en Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0f2993d15cecd87879cabc50918d784a16750b30
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958417"
---
# <a name="how-to-deploy-sql-server-big-data-clusters-on-kubernetes"></a>Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Clúster de macrodatos de SQL Server se implementa como contenedores de docker en un clúster de Kubernetes. Se trata de una visión general de los pasos de instalación y configuración:

- Configurar un clúster de Kubernetes en una sola máquina virtual, clúster de máquinas virtuales o en Azure Kubernetes Service (AKS).
- Instalar la herramienta de configuración de clúster **mssqlctl** en el equipo cliente.
- Implementar un clúster de macrodatos de SQL Server en un clúster de Kubernetes.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-sql-server-2019-big-data-tools"></a>Instalar las herramientas de macrodatos de SQL Server 2019

Antes de implementar un clúster de macrodatos 2019 de SQL Server, en primer lugar [instalar las herramientas de datos de gran tamaño](deploy-big-data-tools.md):

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **Extensión de SQL Server 2019**

## <a id="prereqs"></a> Requisitos previos de Kubernetes

Clústeres de SQL Server datos de gran tamaño requieren una versión mínima de Kubernetes de al menos v1.10 para el servidor y cliente (kubectl).

> [!NOTE]
> Tenga en cuenta que las versiones de Kubernetes de cliente y servidor deben estar dentro de la versión secundaria + 1 o -1. Para obtener más información, consulte [Kubernetes admite versiones y componente sesgo](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

### <a id="kubernetes"></a> Instalación de clúster de Kubernetes

Si ya tiene un clúster de Kubernetes que cumpla los requisitos previos mencionados, a continuación, puede ir directamente a la [paso de implementación](#deploy). En esta sección se da por supuesto un conocimiento básico de los conceptos de Kubernetes.  Para obtener información detallada sobre Kubernetes, consulte el [documentación de Kubernetes](https://kubernetes.io/docs/home).

Puede elegir implementar Kubernetes en cualquiera de estas tres maneras:

| Implementación de Kubernetes en: | Descripción | Vínculo |
|---|---|---|
| **Azure Kubernetes Service (AKS)** | Un servicio de contenedor de Kubernetes administrado en Azure. | [Instrucciones](deploy-on-aks.md) |
| **Varias máquinas (kubeadm)** | Un clúster de Kubernetes implementado en máquinas físicas o virtuales con **kubeadm** | [Instrucciones](deploy-with-kubeadm.md) |
| **Minikube** | Un clúster de Kubernetes de nodo único en una máquina virtual. | [Instrucciones](deploy-on-minikube.md) |

> [!TIP]
> Para un script de python de ejemplo que implementa AKS y un clúster de macrodatos en un paso de SQL Server, vea [inicio rápido: Implementar SQL Server en Azure Kubernetes Service (AKS) del clúster de macrodatos](quickstart-big-data-cluster-deploy.md).

### <a name="verify-kubernetes-configuration"></a>Comprobar la configuración de Kubernetes

Ejecute el **kubectl** comando para ver la configuración del clúster. Asegúrese de que kubectl apunta al contexto de clúster correcto.

```bash
kubectl config view
```

Después de haber configurado el clúster de Kubernetes, puede continuar con la implementación de un nuevo clúster de macrodatos de SQL Server. Si va a actualizar desde una versión anterior, consulte [cómo actualizar clústeres de SQL Server macrodatos](deployment-upgrade.md).

## <a id="deploy"></a> Introducción a la implementación

A partir de CTP 2.5, la mayoría de los valores de clúster de macrodatos se define en un archivo de configuración de implementación de JSON. Puede usar un perfil de implementación predeterminado para AKS, kubeadm, o minikube o se puede personalizar su propio archivo de configuración de implementación para usar durante la instalación. Por motivos de seguridad, la configuración de autenticación se pasa a través de las variables de entorno.

Las secciones siguientes proporcionan más detalles sobre cómo configurar los datos de gran tamaño de clúster implementaciones, así como ejemplos de personalizaciones comunes. Además, siempre puede modificar el archivo de configuración de implementación personalizado mediante un editor como VSCode por ejemplo.

## <a id="configfile"></a> Configuraciones predeterminadas

Las opciones se definen en archivos de configuración JSON de implementación de clúster de macrodatos. Hay tres perfiles de implementación estándar con la configuración predeterminada para los entornos de desarrollo y pruebas:

| Perfil de implementación | Entorno de Kubernetes |
|---|---|
| **aks-dev-test** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test** | Varias máquinas (kubeadm) |
| **minikube-dev-test** | Minikube |

Puede implementar un clúster de macrodatos mediante la ejecución de **mssqlctl bdc crear**. Esto le pedirá que elija una de las configuraciones predeterminadas y, a continuación, le guía a través de la implementación.

```bash
mssqlctl bdc create
```

En este escenario, se solicitará cualquier configuración que no forma parte de la configuración predeterminada, como contraseñas. Tenga en cuenta que la información de Docker se proporciona a usted por Microsoft como parte de la SQL Server de 2019 [programa de adopción temprana](https://aka.ms/eapsignup).

> [!IMPORTANT]
> El nombre predeterminado del clúster de macrodatos es **mssql-cluster**. Esto es importante saber con el fin de ejecutar cualquiera de los **kubectl** comandos que especifican el espacio de nombres de Kubernetes con el `-n` parámetro.

## <a id="customconfig"></a> Configuraciones personalizadas

También es posible personalizar su propio perfil de configuración de implementación. Puede hacerlo con los pasos siguientes:

1. Comience con uno de los perfiles de implementación estándar que coinciden con el entorno de Kubernetes. Puede usar el **mssqlctl bdc config lista** comando para enumerarlas:

   ```bash
   mssqlctl bdc config list
   ```

1. Para personalizar la implementación, crear una copia del perfil de implementación con el **mssqlctl bdc config init** comando. Por ejemplo, el siguiente comando crea una copia de la **aks-dev-test** archivo de configuración de implementación en un directorio de destino denominado `custom`:

   ```bash
   mssqlctl bdc config init --source aks-dev-test --target custom
   ```

   > [!TIP]
   > El `--target` especifica un directorio que contiene el archivo de configuración según la `--source` parámetro.

1. Para personalizar la configuración en el perfil de configuración de implementación, puede editar el archivo de configuración de implementación en una herramienta que sirve para editar archivos JSON, por ejemplo, VS Code. Para la automatización con secuencias de comandos, también puede editar el perfil de implementación personalizado mediante **mssqlctl bdc config sección conjunto** comando. Por ejemplo, el comando siguiente modifica un perfil de implementación personalizado para cambiar el nombre del clúster implementado desde el valor predeterminado (**mssql-cluster**) a **test-cluster**:  

   ```bash
   mssqlctl bdc config section set --config-profile custom --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > El `--config-profile` especifica un nombre de directorio para el perfil de implementación personalizado, pero las modificaciones reales ocurrir en el archivo JSON de configuración de implementación dentro de ese directorio. Es una herramienta útil para buscar las rutas de acceso JSON el [JSONPath en línea evaluador](https://jsonpath.com/).

   Además de pasar pares de clave y valor, también puede proporcionar valores JSON de en línea o pasar archivos de revisión de JSON. Para obtener más información, consulte [configurar opciones de implementación para los clústeres de macrodatos](deployment-custom-configuration.md).

1. A continuación, pase el archivo de configuración personalizada a **mssqlctl bdc crear**. Tenga en cuenta que debe establecer los [variables de entorno](#env), en caso contrario, se le pedirá los valores:

   ```bash
   mssqlctl bdc create --config-profile custom --accept-eula yes
   ```

> [!TIP]
> Para obtener más información sobre la estructura de un archivo de configuración de implementación, consulte el [referencia del archivo de configuración de implementación](reference-deployment-config.md). Para obtener más ejemplos de configuración, consulte [configurar opciones de implementación para los clústeres de macrodatos](deployment-custom-configuration.md).

## <a id="env"></a> Variables de entorno

Las siguientes variables de entorno se usan para la configuración de seguridad que no se almacena en un archivo de configuración de implementación. Tenga en cuenta que se puede establecer la configuración de Docker, excepto las credenciales en el archivo de configuración.

| Variable de entorno | Descripción |
|---|---|---|---|
| **DOCKER_USERNAME** | El nombre de usuario para tener acceso a las imágenes de contenedor en caso de que se almacenan en un repositorio privado. |
| **DOCKER_PASSWORD** | La contraseña para acceder al repositorio privado anterior. |
| **CONTROLLER_USERNAME** | El nombre de usuario para el Administrador de clústeres. |
| **CONTROLLER_PASSWORD** | La contraseña para el Administrador de clústeres. |
| **KNOX_PASSWORD** | La contraseña de usuario de Knox. |
| **MSSQL_SA_PASSWORD** | La contraseña del usuario SA para la instancia principal de SQL. |

Estas variables de entorno se deben establecer antes de llamar a **mssqlctl bdc crear**. Si no se establece cualquier variable, se le pedirá para él.

El ejemplo siguiente muestra cómo establecer las variables de entorno para Linux (bash) y Windows (PowerShell):

```bash
export CONTROLLER_USERNAME=admin
export CONTROLLER_PASSWORD=<password>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
export DOCKER_USERNAME=<docker-username>
export DOCKER_PASSWORD=<docker-password>
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
SET DOCKER_USERNAME=<docker-username>
SET DOCKER_PASSWORD=<docker-password>
```

Después de establecer las variables de entorno, debe ejecutar `mssqlctl bdc create` para desencadenar la implementación. Este ejemplo usa el perfil de configuración de clúster que creó anteriormente:

```
mssqlctl bdc create --config-profile custom --accept-eula yes
```

Tenga en cuenta las siguientes directrices:

- En este momento, le proporcionará las credenciales para el registro privado de Docker para usted tras la clasificación de su [registro del programa de adopción temprana](https://aka.ms/eapsignup). Registro del programa de adopción temprana es necesario para probar los clústeres grandes de datos de SQL Server.
- Asegúrese de que incluir las contraseñas en las comillas dobles si contiene algún carácter especial. Puede establecer el **MSSQL_SA_PASSWORD** todo lo que le gusta, pero asegúrese de que la contraseña es suficientemente compleja y no use el `!`, `&` o `'` caracteres. Tenga en cuenta que los delimitadores de comillas dobles solo funcionan en los comandos de bash.
- El **SA** inicio de sesión es un administrador del sistema en la instancia principal de SQL Server que se crea durante la instalación. Después de crear el contenedor de SQL Server, el **MSSQL_SA_PASSWORD** variable de entorno especificada es detectable mediante la ejecución de un eco MSSQL_SA_PASSWORD $ en el contenedor. Por motivos de seguridad, cambiar la contraseña de SA según los procedimientos recomendados que se documentan [aquí](../linux/quickstart-install-connect-docker.md#sapassword).

## <a id="unattended"></a> Instalación desatendida

Para una implementación desatendida, debe establecer todas las variables de entorno necesarias, el uso de un archivo de configuración y llamada `mssqlctl bdc create` comando con el `--accept-eula yes` parámetro. Los ejemplos de la sección anterior muestran la sintaxis para una instalación desatendida.

## <a id="monitor"></a> Supervisar la implementación

Durante el arranque del clúster, la ventana de comandos de cliente dará como resultado el estado de implementación. Durante el proceso de implementación, debería ver una serie de mensajes donde está esperando el pod del controlador:

```output
Waiting for cluster controller to start.
```

En menos de 15 a 30 minutos, se debería notificar que se está ejecutando el pod del controlador:

```output
Cluster controller endpoint is available at 11.111.111.11:30080.
Cluster control plane is ready.
```

> [!IMPORTANT]
> Toda la implementación puede tardar mucho tiempo debido al tiempo necesario para descargar las imágenes de contenedor para los componentes del clúster de macrodatos. Sin embargo, no debería tardar varias horas. Si experimenta problemas con la implementación, consulte [supervisión y solución de problemas de clústeres de SQL Server macrodatos](cluster-troubleshooting-commands.md).

Cuando finalice la implementación, la salida le notifica de éxito:

```output
Cluster deployed successfully.
```

> [!TIP]
> Es el nombre predeterminado para el clúster implementado macrodatos `mssql-cluster` a menos que se modifica una configuración personalizada.

## <a id="endpoints"></a> Recuperar los puntos de conexión

Después de que el script de implementación se ha completado correctamente, puede obtener las direcciones IP de los puntos de conexión externos para el clúster de macrodatos mediante los siguientes pasos.

1. Después de la implementación, busque la dirección IP del punto de conexión de controlador echando un vistazo a la salida EXTERNAL-IP de los siguientes **kubectl** comando:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Si no cambió el nombre predeterminado durante la implementación, use `-n mssql-cluster` en el comando anterior. **MSSQL-cluster** es el nombre predeterminado para el clúster de macrodatos.

1. Inicie sesión en el clúster de macrodatos con [inicio de sesión mssqlctl](reference-mssqlctl.md). Establecer el **--punto de conexión del controlador** parámetro a la dirección IP externa del punto de conexión del controlador.

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique el nombre de usuario y contraseña que ha configurado para el controlador (CONTROLLER_USERNAME y CONTROLLER_PASSWORD) durante la implementación.

1. Ejecute [lista de puntos de conexión de bdc mssqlctl](reference-mssqlctl-bdc-endpoint.md) para obtener una lista con una descripción de cada punto de conexión y sus correspondientes valores de puerto y la dirección IP. 

   ```bash
   mssqlctl bdc endpoint list -o table
   ```

   En la lista siguiente se muestra la salida de este comando:

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

También puede obtener todos los extremos de servicio implementados para el clúster mediante la ejecución del siguiente **kubectl** comando:

```bash
kubectl get svc -n <your-big-data-cluster-name>
```

### <a name="minikube"></a>Minikube

Si usas minikube, deberá ejecutar el siguiente comando para obtener la dirección IP que necesita para conectarse a. Además de la dirección IP, especifique el puerto para el punto de conexión que necesita para conectarse a.

```bash
minikube ip
```

## <a id="status"></a> Compruebe el estado del clúster

Después de la implementación, puede comprobar el estado del clúster con el [Mostrar estado de mssqlctl bdc](reference-mssqlctl-bdc-status.md) comando.

```bash
mssqlctl bdc status show -o table
```

> [!TIP]
> Para ejecutar los comandos de estado, primero debe iniciar sesión con la **inicio de sesión mssqlctl** comando, que se mostró en la sección de puntos de conexión anterior.

A continuación muestra la salida de ejemplo de este comando:

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

Además de este resumen de estado, también puede obtener el estado más detallado con los siguientes comandos:

- [estado del control de bdc mssqlctl](reference-mssqlctl-bdc-control-status.md)
- [estado del grupo de bdc mssqlctl](reference-mssqlctl-bdc-pool-status.md)

El resultado de estos comandos contienen las direcciones URL a los paneles de Kibana y Grafana para un análisis más detallado. 

Además de usar **mssqlctl**, también puede usar Azure Data Studio para buscar los puntos de conexión y la información de estado. Para obtener más información acerca de cómo ver el estado del clúster con **mssqlctl** y Azure Data Studio, consulte [cómo ver el estado de un clúster de macrodatos](view-cluster-status.md).

## <a id="connect"></a> Conéctese al clúster

Para obtener más información sobre cómo conectarse al clúster de macrodatos, consulte [conectar a SQL Server del clúster macrodatos con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de la implementación de clúster de macrodatos, consulte los siguientes recursos:

- [Configurar opciones de implementación para los clústeres de datos de gran tamaño](deployment-custom-configuration.md)
- [Realizar una implementación sin conexión de un clúster de macrodatos de SQL Server](deploy-offline.md)
- [Taller: Arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
