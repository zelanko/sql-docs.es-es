---
title: Guía para la implementación
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo implementar clústeres de macrodatos de 2019 de SQL Server (versión preliminar) en Kubernetes.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a2ace569180006f54461631848ecbf5342b2c1e3
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472041"
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
| **aks-dev-test.json** | Azure Kubernetes Service (AKS) |
| **kubeadm-dev-test.json** | Varias máquinas (kubeadm) |
| **minikube-dev-test.json** | minikube |

Puede implementar un clúster de macrodatos mediante la ejecución de **de creación del clúster mssqlctl**. Esto le pedirá que elija una de las configuraciones predeterminadas y, a continuación, le guía a través de la implementación.

```bash
mssqlctl cluster create
```

> [!TIP]
> En este ejemplo, se solicitará cualquier configuración que no forma parte de la configuración predeterminada, como contraseñas. Tenga en cuenta que la información de Docker se proporciona a usted por Microsoft como parte de la SQL Server de 2019 [programa de adopción temprana](https://aka.ms/eapsignup).

## <a id="customconfig"></a> Configuraciones personalizadas

También es posible personalizar su propio archivo de configuración de implementación. Puede hacerlo con los pasos siguientes:

1. Comience con uno de los perfiles de implementación estándar que coinciden con el entorno de Kubernetes. Puede usar el **lista de configuración de clúster mssqlctl** comando para enumerarlas:

   ```bash
   mssqlctl cluster config list
   ```

1. Para personalizar la implementación, crear una copia del perfil de implementación con el **mssqlctl cluster config init** comando. Por ejemplo, el siguiente comando crea una copia de la **aks-dev-test.json** archivo de configuración de implementación en el directorio actual:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

1. Para personalizar la configuración en el archivo de configuración de implementación, puede editar en una herramienta que sirve para editar documentos json como VS Code. Para la automatización con secuencias de comandos, puede editar el archivo de configuración personalizada mediante **conjunto de sección de configuración de clúster mssqlctl** comando. Por ejemplo, el comando siguiente modifica un archivo de configuración personalizado para cambiar el nombre del clúster implementado desde el valor predeterminado (**mssql-cluster**) a **test-cluster**:  

   ```bash
   mssqlctl cluster config section set --config-file custom.json --json-values "metadata.name=test-cluster"
   ```

   > [!TIP]
   > Es una herramienta útil para buscar las rutas de acceso JSON el [JSONPath en línea evaluador](https://jsonpath.com/).

   Además de pasar pares de clave y valor, también puede proporcionar valores JSON de en línea o pasar archivos de revisión de JSON. Para obtener más información, consulte [configurar opciones de implementación para los clústeres de macrodatos](deployment-custom-configuration.md).

1. A continuación, pase el archivo de configuración personalizada a **de creación del clúster mssqlctl**. Tenga en cuenta que debe establecer los [variables de entorno](#env), en caso contrario, se le pedirá los valores:

   ```bash
   mssqlctl cluster create --config-file custom.json --accept-eula yes
   ```

> [!TIP]
> Para obtener más información sobre la estructura de un archivo de configuración de implementación, consulte el [referencia del archivo de configuración de implementación](reference-deployment-config.md). Para obtener más ejemplos de configuración, consulte [configurar opciones de implementación para los clústeres de macrodatos](deployment-custom-configuration.md).

## <a id="env"></a> Variables de entorno

Las siguientes variables de entorno se usan para la configuración de seguridad que no se almacena en un archivo de configuración de implementación.

| Variable de entorno | Descripción |
|---|---|---|---|
| **DOCKER_REGISTRY** | El registro privado donde se almacenan las imágenes se usan para implementar el clúster. |
| **DOCKER_REPOSITORY** | El repositorio privado en el registro anterior donde se almacenan las imágenes. |
| **DOCKER_USERNAME** | El nombre de usuario para tener acceso a las imágenes de contenedor en caso de que se almacenan en un repositorio privado. |
| **DOCKER_PASSWORD** | La contraseña para acceder al repositorio privado anterior. |
| **DOCKER_IMAGE_TAG** | La etiqueta utilizada para etiquetar las imágenes. El valor predeterminado es **más reciente**, pero se recomienda usar la etiqueta correspondiente a la versión para evitar problemas de incompatibilidad de versiones. |
| **CONTROLLER_USERNAME** | El nombre de usuario para el Administrador de clústeres. |
| **CONTROLLER_PASSWORD** | La contraseña para el Administrador de clústeres. |
| **KNOX_PASSWORD** | La contraseña de usuario de Knox. |
| **MSSQL_SA_PASSWORD** | La contraseña del usuario SA para la instancia principal de SQL. |

Estas variables de entorno se deben establecer antes de llamar a **de creación del clúster mssqlctl**. Si no se establece cualquier variable, se le pedirá para él.

El ejemplo siguiente muestra cómo establecer las variables de entorno para Linux (bash) y Windows (PowerShell):

```bash
export CONTROLLER_USERNAME=<controller_user>
export CONTROLLER_PASSWORD=<password>
export DOCKER_REGISTRY=<docker-registry>
export DOCKER_REPOSITORY=<docker-repository>
export MSSQL_SA_PASSWORD=<password>
export KNOX_PASSWORD=<password>
export DOCKER_USERNAME=<docker-username>
export DOCKER_PASSWORD=<docker-password>
export DOCKER_IMAGE_TAG=ctp2.5
```

```PowerShell
SET CONTROLLER_USERNAME=admin
SET CONTROLLER_PASSWORD=<password>
SET DOCKER_REGISTRY=<docker-registry>
SET DOCKER_REPOSITORY=<docker-repository>
SET MSSQL_SA_PASSWORD=<password>
SET KNOX_PASSWORD=<password>
SET DOCKER_USERNAME=<docker-username>
SET DOCKER_PASSWORD=<docker-password>
SET DOCKER_IMAGE_TAG=ctp2.5
```

Tras establecer las variables de entorno, debe ejecutar `mssqlctl cluster create` para desencadenar la implementación. En este ejemplo se usa el archivo de configuración de clúster que creó anteriormente:

```
mssqlctl cluster create --config-file custom.json --accept-eula yes
```

Tenga en cuenta las siguientes directrices:

- En este momento, le proporcionará las credenciales para el registro privado de Docker para usted tras la clasificación de su [registro del programa de adopción temprana](https://aka.ms/eapsignup). Registro del programa de adopción temprana es necesario para probar los clústeres grandes de datos de SQL Server.
- Asegúrese de que incluir las contraseñas en las comillas dobles si contiene algún carácter especial. Puede establecer el **MSSQL_SA_PASSWORD** todo lo que le gusta, pero asegúrese de que la contraseña es suficientemente compleja y no use el `!`, `&` o `'` caracteres. Tenga en cuenta que los delimitadores de comillas dobles solo funcionan en los comandos de bash.
- El **SA** inicio de sesión es un administrador del sistema en la instancia principal de SQL Server que se crea durante la instalación. Después de crear el contenedor de SQL Server, el **MSSQL_SA_PASSWORD** variable de entorno especificada es detectable mediante la ejecución de un eco MSSQL_SA_PASSWORD $ en el contenedor. Por motivos de seguridad, cambiar la contraseña de SA según los procedimientos recomendados que se documentan [aquí](../linux/quickstart-install-connect-docker.md#sapassword).
- El **DOCKER_IMAGE_TAG** en este ejemplo controla qué versión se va a instalar. En este ejemplo, es la versión 2.5 de CTP.

## <a id="unattended"></a> Instalación desatendida

Para una implementación desatendida, debe establecer todas las variables de entorno necesarias, el uso de un archivo de configuración y llamada `mssqlctl cluster create` comando con el `--accept-eula yes` parámetro. Los ejemplos de la sección anterior muestran la sintaxis para una instalación desatendida.

## <a id="monitor"></a> Supervisar la implementación

Durante el arranque del clúster, la ventana de comandos de cliente dará como resultado el estado de implementación. Durante el proceso de implementación, debería ver una serie de mensajes donde está esperando el pod del controlador:

```output
2019-04-12 14:40:10.0129 UTC | INFO | Waiting for controller pod to be up...
```

En menos de 15 a 30 minutos, se debería notificar que se está ejecutando el pod del controlador:

```output
2019-04-12 15:01:10.0809 UTC | INFO | Waiting for controller pod to be up. Checkthe mssqlctl.log file for more details.
2019-04-12 15:01:40.0861 UTC | INFO | Controller pod is running.
2019-04-12 15:01:40.0884 UTC | INFO | Controller Endpoint: https://<ip-address>:30080
```

> [!IMPORTANT]
> Toda la implementación puede tardar mucho tiempo debido al tiempo necesario para descargar las imágenes de contenedor para los componentes del clúster de macrodatos. Sin embargo, no debería tardar varias horas. Si experimenta problemas con la implementación, consulte [supervisión y solución de problemas de clústeres de SQL Server macrodatos](cluster-troubleshooting-commands.md).

Cuando finalice la implementación, la salida le notifica de éxito:

```output
2019-04-12 15:37:18.0271 UTC | INFO | Monitor and track your cluster at the Portal Endpoint: https://<ip-address>:30777/portal/
2019-04-12 15:37:18.0271 UTC | INFO | Cluster deployed successfully.
```

Tenga en cuenta la dirección URL de la **punto de conexión del Portal** en la salida anterior para su uso en la sección siguiente.

> [!TIP]
> Es el nombre predeterminado para el clúster implementado macrodatos `mssql-cluster` a menos que se modifica una configuración personalizada.

## <a id="endpoints"></a> Recuperar los puntos de conexión

Después de que el script de implementación se ha completado correctamente, puede obtener las direcciones IP de los puntos de conexión externos para el clúster de macrodatos mediante los siguientes pasos.

1. En la salida de la implementación, copie el **punto de conexión del Portal** y quitar el `/portal/` al final. Se trata de la dirección URL del Proxy de administración (por ejemplo, `https://<ip-address>:30777`).

   > [!TIP]
   > Si no tiene el resultado de la implementación, puede obtener la dirección IP del proxy de administración echando un vistazo a la salida EXTERNAL-IP de los siguientes **kubectl** comando:
   >
   > ```bash
   > kubectl get svc mgmtproxy-svc-external -n <your-cluster-name>
   > ```

1. Inicie sesión en el clúster de macrodatos con **inicio de sesión mssqlctl**. Establecer el **--punto de conexión** parámetro para el Proxy de administración.

   ```bash
   mssqlctl login --endpoint https://<ip-address>:30777
   ```

   Especifique el nombre de usuario y contraseña que ha configurado para el controlador (CONTROLLER_USERNAME y CONTROLLER_PASSWORD) durante la implementación.

1. Ejecute **lista de puntos de conexión de clúster mssqlctl** para obtener una lista con una descripción de cada punto de conexión y sus correspondientes valores de puerto y la dirección IP. Por ejemplo, la siguiente muestra la salida para el punto de conexión del Portal de administración:

   ```output
   {
     "description": "Management Portal",
     "endpoint": "https://<ip-address>:30777/portal",
     "ip": "<ip-address>",
     "name": "portal",
     "port": 30777,
     "protocol": "https"
   },
   ```

1. También se describen todos los puntos de conexión de clúster en el **los extremos de servicio** ficha en el Portal de administración de clúster. Se puede acceder al portal mediante el punto de conexión del Portal de administración en el paso anterior (por ejemplo, `https://<ip-address>:30777/portal`). Las credenciales de acceso al portal de administración son los valores para el nombre de usuario del controlador y la contraseña que especificó durante la implementación. También puede usar el Portal de administración de clúster para supervisar la implementación.

### <a name="minikube"></a>Minikube

Si usas minikube, deberá ejecutar el siguiente comando para obtener la dirección IP que necesita para conectarse a. Además de la dirección IP, especifique el puerto para el punto de conexión que necesita para conectarse a.

```bash
minikube ip
```

Independientemente de la plataforma usa su clúster de Kubernetes, para obtener todos los extremos de servicio implementados para el clúster, ejecute el siguiente comando:

```bash
kubectl get svc -n <your-cluster-name>
```

## <a id="connect"></a> Conéctese al clúster

Para obtener más información sobre cómo conectarse al clúster de macrodatos, consulte [conectar a SQL Server del clúster macrodatos con Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de la implementación de clúster de macrodatos, consulte los siguientes recursos:

- [Configurar opciones de implementación para los clústeres de datos de gran tamaño](deployment-custom-configuration.md)
- [Realizar una implementación sin conexión de un clúster de macrodatos de SQL Server](deploy-offline.md)
- [Taller: Arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
