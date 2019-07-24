---
title: ¿Qué es el controlador?
titleSuffix: SQL Server big data clusters
description: En este artículo se describe el controlador de un clúster de macrodatos SQL Server 2019 (versión preliminar).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e984c3dced4bde713ac98d67c22481e54491cd68
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419537"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>¿Cuál es el controlador de un clúster de macrodatos SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El controlador hospeda la lógica básica para implementar y administrar un clúster de Big Data. Se encarga de todas las interacciones con Kubernetes, SQL Server instancias que forman parte del clúster y otros componentes como HDFS y Spark.

El servicio de controlador proporciona la siguiente funcionalidad básica:

- Administrar el ciclo de vida del clúster: bootstrap de clúster & eliminar, configuraciones de actualización
- Administrar instancias de SQL Server maestras
- Administración de procesos, datos y grupos de almacenamiento
- Exponer herramientas de supervisión para observar el estado del clúster
- Exponer las herramientas de solución de problemas para detectar y reparar problemas inesperados
- Administrar la seguridad del clúster:
  - Garantizar puntos de conexión de clúster seguros
  - Administrar usuarios y roles
  - Configurar credenciales para la comunicación dentro del clúster

## <a name="deploying-the-controller-service"></a>Implementación del servicio de controlador

El controlador se implementa y se hospeda en el mismo espacio de nombres de Kubernetes donde el cliente desea crear un clúster de Big Data. Un administrador de Kubernetes instala este servicio durante el arranque del clúster mediante la utilidad de línea de comandos **azdata** . Para obtener más información, consulte Introducción a los clústeres de macrodatos de [SQL Server](deploy-get-started.md).

El flujo de trabajo de buildout se presentará por encima de Kubernetes un clúster de macrodatos SQL Server totalmente funcional que incluye todos los componentes descritos en el artículo de [información general](big-data-cluster-overview.md) . El flujo de trabajo de bootstrap crea primero el servicio de controlador y, una vez implementado, el servicio de controlador coordinará la instalación y la configuración del resto de los servicios que forman parte de los grupos Master, compute, data y Storage.

## <a name="managing-the-cluster-through-the-controller-service"></a>Administrar el clúster a través del servicio de controlador

Puede administrar el clúster a través del servicio de controlador mediante los comandos **azdata** . Si implementa objetos Kubernetes adicionales como pods en el mismo espacio de nombres, el servicio del controlador no los administra ni los supervisa. También puede usar los comandos **kubectl** para administrar el clúster en el nivel de Kubernetes. Para obtener más información, consulte [supervisión y solución de problemas](cluster-troubleshooting-commands.md)de clústeres de macrodatos SQL Server.

El controlador y los objetos Kubernetes (conjuntos con estado, pods, secretos, etc.) creados para un clúster de Big Data residen en un espacio de nombres de Kubernetes dedicado. El administrador de clústeres de Kubernetes concederá permiso al servicio de controlador para administrar todos los recursos de ese espacio de nombres.  La Directiva RBAC para este escenario se configura automáticamente como parte de la implementación inicial del clúster mediante **azdata**.

### <a name="azdata"></a>azdata

**azdata** es una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar clústeres de Big Data a través de las API de REST expuestas por el servicio del controlador.

## <a name="controller-service-security"></a>Seguridad del servicio del controlador

Toda la comunicación con el servicio del controlador se realiza a través de una API de REST a través de HTTPS. Se generará automáticamente un certificado autofirmado en el momento del arranque. 

La autenticación en el extremo del servicio del controlador se basa en el nombre de usuario y la contraseña. Estas credenciales se aprovisionan en el momento de arranque del clúster mediante la entrada `CONTROLLER_USERNAME` para `CONTROLLER_PASSWORD`las variables de entorno y.

> [!NOTE]
> Debe proporcionar una contraseña que cumpla [los requisitos de SQL Server la complejidad de la contraseña](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos SQL Server, consulte los siguientes recursos:

- [¿Qué son los clústeres de macrodatos SQL Server 2019?](big-data-cluster-overview.md)
- [Taller Arquitectura de clústeres de macrodatos Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
