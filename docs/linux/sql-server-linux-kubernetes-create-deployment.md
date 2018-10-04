---
title: Crear scripts de implementación de SQL Server grupo de disponibilidad AlwaysOn en Kubernetes
description: En este artículo se explica cómo crear scripts de implementación para un SQL Server grupo de disponibilidad AlwaysOn en Kubernetes
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2bc5acc2ee6f81dbdf1ce16a98fb7f75bbf6f121
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47594563"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>Crear script de implementación de SQL Server grupo de disponibilidad AlwaysOn

En este artículo se describe cómo implementar un grupo de disponibilidad en un clúster de Kubernetes en un único comando con un script de implementación de ejemplo. `deploy-ag.py` es un script de Python que crea el `.yaml` archivos para el clúster y se pueden aplicar a un clúster de Kubernetes.

Descarga de archivos desde los archivos [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script).

## <a name="before-you-start"></a>Antes de empezar

Instale las herramientas siguientes en la estación de trabajo.

* [Python](https://www.python.org/downloads/) (3.5 o 3.6)
* [PyYAML](https://pyyaml.org/) -paquetes de Python
* [Cliente de Kubernetes](https://github.com/kubernetes-client/python) -paquete de Python

Agregar rutas de acceso de python a las variables de entorno (para Windows).

### <a name="install-the-required-components"></a>Instalar los componentes necesarios

El ejemplo siguiente la anterior instala los paquetes PyYAML y cliente de Kubernetes para Python.

Después de instalar Python, descargue y extraiga la carpeta de ejemplo. 

Para configurar los archivos necesarios, ejecute el siguiente comando. Reemplace `<path>` con la ubicación de los archivos de ejemplo extraídos.

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>Crear clúster y descargue el archivo de configuración

El ejemplo siguiente crea el clúster en Azure Kubernetes Service (AKS).

Antes de ejecutar el script, actualice los valores en corchetes angulares - `<>`.

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>Grupos de disponibilidad requiere Kubernetes versión 1.11.0 o superior. El ejemplo especifica 1.11.1.

## <a name="run-the-deployment-script"></a>Ejecute el script de implementación

Los ejemplos siguientes muestran cómo ejecutar `deploy-ag.py`.

### <a name="help"></a>Ayuda

```cmd
python ./deploy-ag.py --help
```

* **uso**: `deploy-ag.py [-h] {deploy | failover} ...`
* **argumentos opcionales**:
  * `-h, --help` Mostrar este mensaje de ayuda y salir
* **subcomandos**:
  * Las acciones de agente k8s {implementar | conmutación por error}

  `deploy`

   Implementar un conjunto de servidores de SQL Server en un grupo de disponibilidad

  `failover`

   Conmutación por error a una réplica de destino.

### <a name="deploy-help"></a>Implementar la Ayuda

```cmd
python ./deploy-ag.py deploy --help
```

* **uso**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  Implementar SQL Server y los agentes k8s en namespace(AG name)

* **argumentos opcionales**:
  
  `-h, --help`
  
  Mostrar este mensaje de ayuda y salir
  
  `--verbose, -v`
  
  Nivel de detalle de salida
  
  `--ag AG`
  
  nombre del grupo de disponibilidad. Valor predeterminado = ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  nombre del espacio de nombres k8s. El valor predeterminado es el nombre de grupo de disponibilidad si no se especifica.

  `--dry-run`
  
  Crear los manifiestos, pero no se aplican.
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  los nombres de instancias de SQL Server (hasta 5, separados por espacios) Default = ['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  Contraseña de SA. Valor predeterminado = 'SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  Omitir la creación de espacio de nombres.

### <a name="failover-help"></a>Ayuda de la conmutación por error

```cmd
python ./deploy-ag.py failover --help
```
* **uso**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  Conmutación por error manual

* **los argumentos posicionales**: `target_replica`

  nombre de réplica de SQL Server de destino para la conmutación por error

* **argumentos opcionales**:

  `-h, --help`
  
  Mostrar este mensaje de ayuda y salir

  `--verbose, -v`
  
  Nivel de detalle de salida

  `--ag AG`
  
  nombre del grupo de disponibilidad. Valor predeterminado = ag1

  `--namespace NAMESPACE`

  nombre del espacio de nombres k8s. El valor predeterminado es el nombre de grupo de disponibilidad si no se especifica

  `--dry-run`
  
  Crear, pero no se aplican los manifiestos.

### <a name="create-the-manifests---dont-apply"></a>Creación de los manifiestos: no se aplican

El siguiente script crea los archivos de manifiesto, pero no es aplicable.

```cmd
python ./deploy-ag.py deploy --dry-run
```

El ejemplo siguiente crea los manifiestos de un grupo de disponibilidad en el espacio de nombres `AG1` con tres réplicas. Antes de ejecutar el script, reemplace `<MyC0m91exP@55w0r!>` con una contraseña compleja.

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

El comando anterior genera el directorio de archivos de ejemplo yaml.

En este caso, la salida del comando muestra donde se crean los archivos de manifiesto.

![salida del script](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>Los manifiestos de crear y aplicar

El ejemplo siguiente crea los manifiestos de un grupo de disponibilidad en el espacio de nombres `ag1` con tres réplicas y se aplica a su clúster de Kubernetes. El clúster, a continuación, creará el grupo de disponibilidad. Antes de ejecutar el script, reemplace `<MyC0m91exP@55w0r!>` con una contraseña compleja.

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

Una vez finalizada la secuencia de comandos, el operador de Kubernetes crea el almacenamiento, las instancias de SQL Server, los servicios de equilibrador de carga. Puede supervisar la implementación con [panel de Kubernetes](http://docs.microsoft.com/azure/aks/kubernetes-dashboard).

Después de que Kubernetes crea los contenedores de SQL Server:

1. [Conectar](sql-server-linux-kubernetes-connect.md) a una instancia de SQL Server en el clúster.

1. Crear una base de datos.

1. Realizar copia de seguridad de la base de datos para iniciar la cadena de registros una completa.

1. Agregue la base de datos al grupo de disponibilidad.

Se crea el grupo de disponibilidad con propagación automática, por lo que SQL Server creará automáticamente las bases de datos secundaria en las réplicas adecuadas.

### <a name="manually-failover"></a>Conmutación por error manual

El ejemplo siguiente se conmuta por error la réplica principal.

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>Pasos siguientes

[Grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)
