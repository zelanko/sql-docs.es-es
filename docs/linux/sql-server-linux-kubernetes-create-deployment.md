---
title: Creación de scripts de implementación para un grupo de disponibilidad Always On de SQL Server en Kubernetes
description: En este artículo se explica cómo crear scripts de implementación para un grupo de disponibilidad Always On de SQL Server en Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 181773a19e87c34a1931cae05f5a329aedbc1239
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000133"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>Creación de scripts de implementación para un grupo de disponibilidad Always On de SQL Server

En este artículo se describe cómo implementar un grupo de disponibilidad en un clúster de Kubernetes en un único comando con un script de implementación de ejemplo. `deploy-ag.py` es un script de Python que crea los archivos `.yaml` para el clúster y puede aplicarlos a un clúster de Kubernetes.

Descargue el archivo de archivos de [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script).

## <a name="before-you-start"></a>Antes de empezar

Instale las herramientas siguientes en la estación de trabajo.

* [Python](https://www.python.org/downloads/) (3.5 o 3.6)
* [PyYAML](https://pyyaml.org/): paquetes de Python
* [Cliente de Kubernetes](https://github.com/kubernetes-client/python): paquete de Python

Agregue las rutas de acceso de Python a las variables de entorno (para Windows).

### <a name="install-the-required-components"></a>Instalar los componentes necesarios

En el ejemplo siguiente se instalan los paquetes de PyYAML y del cliente de Kubernetes para Python.

Después de instalar Python, descargue y extraiga la carpeta de ejemplo. 

Para configurar los archivos necesarios, ejecute el siguiente comando: Reemplace `<path>` por la ubicación de los archivos de ejemplo extraídos.

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>Crear un clúster y descargar el archivo de configuración

En el ejemplo siguiente se crea el clúster en Azure Kubernetes Service (AKS).

Antes de ejecutar el script, actualice los valores entre corchetes, `<>`.

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>Los grupos de disponibilidad requieren Kubernetes versión 1.11.0 o posterior. En el ejemplo se especifica 1.11.1.

## <a name="run-the-deployment-script"></a>Ejecutar el script de implementación

A continuación se incluyen ejemplos sobre cómo ejecutar `deploy-ag.py`.

### <a name="help"></a>Ayuda

```cmd
python ./deploy-ag.py --help
```

* **Uso**: `deploy-ag.py [-h] {deploy | failover} ...`
* **argumentos opcionales**:
  * `-h, --help` muestran este mensaje de ayuda y salen
* **subcomandos**:
  * Acciones en el agente k8s {deploy | failover}

  `deploy`

   Implementa un conjunto de servidores de SQL Server en un grupo de disponibilidad

  `failover`

   Conmuta por error a una réplica de destino

### <a name="deploy-help"></a>Ayuda de implementación

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

  Implementar agentes SQL Server y k8s en el espacio de nombres (nombre de AG)

* **argumentos opcionales**:
  
  `-h, --help`
  
  muestran este mensaje de ayuda y salen
  
  `--verbose, -v`
  
  nivel de detalle de la salida
  
  `--ag AG`
  
  nombre del grupo de disponibilidad Valor predeterminado = ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  nombre del espacio de nombres de k8s. Si no se especifica, el valor predeterminado es AG

  `--dry-run`
  
  crea los manifiestos, pero no los aplica
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  nombres de instancias de SQL Server (hasta 5, separadas por espacios). Valor predeterminado = ['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  contraseña de asociación de seguridad. Valor predeterminado = 'SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  omite la creación del espacio de nombres

### <a name="failover-help"></a>Ayuda de conmutación por error

```cmd
python ./deploy-ag.py failover --help
```
* **uso**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  conmutación por error manual

* **Argumentos posicionales**: `target_replica`

  nombre de la réplica de SQL Server de destino para la conmutación por error

* **argumentos opcionales**:

  `-h, --help`
  
  muestran este mensaje de ayuda y salen

  `--verbose, -v`
  
  nivel de detalle de la salida

  `--ag AG`
  
  nombre del grupo de disponibilidad Valor predeterminado = ag1

  `--namespace NAMESPACE`

  nombre del espacio de nombres de k8s. Si no se especifica, el valor predeterminado es AG

  `--dry-run`
  
  crea los manifiestos, pero no los aplica

### <a name="create-the-manifests---dont-apply"></a>Crear los manifiestos: no aplicarlos

El script siguiente crea los archivos de manifiesto, pero no los aplica.

```cmd
python ./deploy-ag.py deploy --dry-run
```

El ejemplo siguiente crea los manifiestos para un grupo de disponibilidad en el espacio de nombres `AG1` con tres réplicas. Antes de ejecutar el script, reemplace `<MyC0m91exP@55w0r!>` por una contraseña compleja.

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

El comando anterior genera el directorio de archivos YAML de ejemplo.

En este caso, la salida del comando muestra dónde se crean los archivos de manifiesto.

![salida del script](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>Crear los manifiestos y aplicarlos

El ejemplo siguiente crea los manifiestos para un grupo de disponibilidad en el espacio de nombres `ag1` con tres réplicas y los aplica al clúster de Kubernetes. Luego el clúster creará el grupo de disponibilidad. Antes de ejecutar el script, reemplace `<MyC0m91exP@55w0r!>` por una contraseña compleja.

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

Una vez completado el script, el operador de Kubernetes crea el almacenamiento, las instancias de SQL Server y los servicios del equilibrador de carga. Puede supervisar la implementación con el [panel de Kubernetes](https://docs.microsoft.com/azure/aks/kubernetes-dashboard).

Después de que Kubernetes cree los contenedores de SQL Server:

1. [Conéctese](sql-server-linux-kubernetes-connect.md) a una instancia de SQL Server en el clúster.

1. Crear una base de datos.

1. Haga una copia de seguridad completa de la base de datos para iniciar la cadena de registros.

1. Agregue la base de datos al grupo de disponibilidad.

El grupo de disponibilidad se crea con propagación automática, de modo que SQL Server creará automáticamente las bases de datos secundarias en la réplicas apropiadas.

### <a name="manually-failover"></a>conmutación por error manual

En el ejemplo siguiente se realiza una conmutación por error de la réplica principal.

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>Pasos siguientes

[Grupo de disponibilidad Always On de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)
