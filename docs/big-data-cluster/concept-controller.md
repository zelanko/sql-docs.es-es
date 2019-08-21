---
title: ¿Qué es el controlador?
titleSuffix: SQL Server big data clusters
description: En este artículo se describe el controlador [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]de un.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 643cb2b4e252e1818940bda2be54917c23cefe06
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652284"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>¿Qué es el controlador de un clúster de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El controlador hospeda la lógica básica para implementar y administrar un clúster de macrodatos. Se encarga de todas las interacciones con Kubernetes, las instancias de SQL Server que forman parte del clúster y otros componentes como HDFS y Spark.

El servicio del controlador proporciona la siguiente funcionalidad básica:

- Administración del ciclo de vida del clúster: arranque y eliminación del clúster, configuraciones de actualización.
- Administración de las instancias maestras de SQL Server.
- Administración de procesos, datos y bloques de almacenamiento.
- Exposición de las herramientas de supervisión para observar el estado del clúster.
- Exposición de las herramientas de solución de problemas para detectar y reparar problemas inesperados.
- Administración de la seguridad del clúster:
  - Garantía de que los puntos de conexión son seguros.
  - Administración de los usuarios y los roles.
  - Configuración de las credenciales para la comunicación dentro del clúster.

## <a name="deploying-the-controller-service"></a>Implementación del controlador del servicio

El controlador se implementa y se hospeda en el mismo espacio de nombres de Kubernetes en el que el cliente quiere crear un clúster de macrodatos. Un administrador de Kubernetes instala este servicio durante el arranque del clúster mediante la utilidad de línea de comandos **azdata**. Para obtener más información, consulte Introducción [a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](deploy-get-started.md).

El flujo de trabajo de creación diseñará sobre Kubernetes un clúster de macrodatos de SQL Server totalmente funcional que incluye todos los componentes que se describen en el artículo de [introducción](big-data-cluster-overview.md). El flujo de trabajo de arranque crea primero el servicio del controlador y, una vez implementado, el servicio del controlador coordinará la instalación y la configuración del resto de los servicios que forman parte de los grupos maestro, de proceso, de datos y de almacenamiento.

## <a name="managing-the-cluster-through-the-controller-service"></a>Administración del clúster mediante el servicio del controlador

Puede administrar el clúster mediante el servicio del controlador con los comandos de **azdata**. Si implementa objetos de Kubernetes adicionales como pods en el mismo espacio de nombres, el servicio del controlador no los administra ni los supervisa. También puede usar los comandos de **kubectl** para administrar el clúster en el nivel de Kubernetes. Para obtener más información, consulte [supervisión y [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]solución de problemas ](cluster-troubleshooting-commands.md).

El controlador y los objetos de Kubernetes (conjuntos con estado, pods, secretos, etc.) creados para un clúster de macrodatos residen en un espacio de nombres de Kubernetes dedicado. El administrador de clústeres de Kubernetes concederá permiso al servicio del controlador para administrar todos los recursos de ese espacio de nombres.  La directiva de RBAC de este escenario se configura automáticamente como parte de la implementación inicial del clúster mediante **azdata**.

### <a name="azdata"></a>azdata

**azdata** es una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar clústeres de macrodatos mediante las API REST que expone el servicio del controlador.

## <a name="controller-service-security"></a>Seguridad del servicio del controlador

Toda la comunicación con el servicio del controlador se realiza mediante una API REST a través de HTTPS. Se generará automáticamente un certificado autofirmado en el momento del arranque. 

La autenticación en el punto de conexión de servicio del controlador se basa en el nombre de usuario y la contraseña. Estas credenciales se aprovisionan en el momento de arranque del clúster mediante la entrada de las variables de entorno `CONTROLLER_USERNAME` y `CONTROLLER_PASSWORD`.

> [!NOTE]
> Debe proporcionar una contraseña que cumpla los [requisitos de complejidad de las contraseñas de SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]de, consulte los siguientes recursos:

- [¿Qué [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]son?](big-data-cluster-overview.md)
- [Taller: Arquitectura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] de Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
