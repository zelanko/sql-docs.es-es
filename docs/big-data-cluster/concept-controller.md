---
title: ¿Qué es el controlador?
titleSuffix: SQL Server big data clusters
description: En este artículo se describe el controlador de un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: jroth
manager: jroth
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 115809307b430a9e5079de4db71180cca4766dac
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783173"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>¿Qué es el controlador en un clúster de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El controlador hospeda la lógica básica para implementar y administrar un clúster de macrodatos. Se encarga de todas las interacciones con Kubernetes, las instancias de SQL Server que forman parte del clúster y otros componentes, como HDFS y Spark.

El servicio del controlador proporciona la funcionalidad siguiente:

- Administrar el ciclo de vida del clúster: arranque del clúster y eliminar, actualizar las configuraciones
- Administrar instancias de SQL Server principales
- Administración de grupos de proceso, datos y almacenamiento
- Exponer las herramientas de supervisión para observar el estado del clúster
- Exponer las herramientas de solución de problemas para detectar y reparar problemas inesperados
- Administrar seguridad del clúster:
  - Asegúrese de puntos de conexión del clúster seguro
  - Administrar usuarios y roles
  - Configurar las credenciales para la comunicación dentro del clúster

## <a name="deploying-the-controller-service"></a>Implementar el servicio de controlador

El controlador está implementado y hospedado en el mismo espacio de nombres de Kubernetes donde el cliente desea crear un clúster de macrodatos. Este servicio se instala un administrador de Kubernetes durante clúster bootstrap, utilizando el **mssqlctl** utilidad de línea de comandos. Para obtener más información, consulte [empezar a trabajar con clústeres grandes de datos de SQL Server](deploy-get-started.md).

El flujo de trabajo buildout preparará sobre Kubernetes un clúster de macrodatos totalmente funcional de SQL Server que incluye todos los componentes descritos en la [Introducción](big-data-cluster-overview.md) artículo. El flujo de trabajo de bootstrap crea primero el servicio de controlador y una vez implementado, el servicio de controlador coordinará la instalación y configuración del resto de la parte de los servicios de grupos de almacenamiento, proceso, datos y master.

## <a name="managing-the-cluster-through-the-controller-service"></a>Administración del clúster a través del servicio de controlador

Puede administrar el clúster exclusivamente a través del servicio de controlador mediante `mssqlctl` API o el portal de administración de clúster que se hospeda dentro del clúster. Si implementa objetos adicionales de Kubernetes como pods en el mismo espacio de nombres, no están administrados ni supervisados por el servicio del controlador.

El controlador y los objetos de Kubernetes (conjuntos con estado, pods, secretos, etc.) creados para un clúster de macrodatos residen en un espacio de nombres de Kubernetes dedicado. El servicio del controlador se concederá permiso por el Administrador de clústeres de Kubernetes para administrar todos los recursos dentro de ese espacio de nombres.  La directiva de RBAC para este escenario se configura automáticamente como parte de la implementación de clúster inicial con `mssqlctl`. 

### <a name="mssqlctl"></a>mssqlctl

`mssqlctl` es una utilidad de línea de comandos escrita en Python que permite a los administradores de clúster arrancar y administrar clústeres de macrodatos a través de las API de REST expuestas por el servicio del controlador.

### <a name="cluster-administration-portal"></a>Portal de administración de clúster

Una vez que el servicio de controlador está en funcionamiento, puede usar el Administrador de clústeres el [Portal de administración de clúster](cluster-admin-portal.md) para supervisar el progreso de la implementación, detectar y solucionar problemas con los servicios dentro del clúster.

## <a name="controller-service-security"></a>Seguridad de servicio de controlador

Todas las comunicaciones con el servicio del controlador se lleva a cabo a través de una API de REST a través de HTTPS. Un certificado autofirmado se generará automáticamente para usted en tiempo de arranque. 

Autenticación en el punto de conexión de servicio de controlador se basa en el nombre de usuario y contraseña. Estas credenciales se aprovisionan en el momento de bootstrap del clúster mediante la entrada para las variables de entorno `CONTROLLER_USERNAME` y `CONTROLLER_PASSWORD`.

> [!NOTE]
> Debe proporcionar una contraseña que está en conformidad con [los requisitos de complejidad de contraseña de SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte los siguientes recursos:

- [¿Qué son los clústeres de macrodatos de 2019 de SQL Server?](big-data-cluster-overview.md)
- [Taller: Arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
