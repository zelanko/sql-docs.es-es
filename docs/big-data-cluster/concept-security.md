---
title: Conceptos de seguridad
titleSuffix: SQL Server big data clusters
description: En este artículo se describen los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]conceptos de seguridad de. Incluye la descripción de los puntos de conexión del clúster y la autenticación del clúster.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4e4441f0cc4f19d4784019408bfc5309a5734285
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652250"
---
# <a name="security-concepts-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Conceptos de seguridad para[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Un clúster de macrodatos seguro implica una compatibilidad consistente y coherente con los escenarios de autenticación y autorización, tanto en SQL Server como en HDFS/Spark. La autenticación es el proceso de comprobar la identidad de un usuario o servicio y asegurarse de que es quien dice ser. La autorización se refiere a la concesión o denegación de acceso a recursos específicos en función de la identidad del usuario que lo solicita. Este paso se realiza después de que un usuario se identifica a través de la autenticación.

La autorización en el contexto de macrodatos se suele realizar mediante listas de control de acceso (ACL), que asocian las identidades de usuario a permisos específicos. HDFS admite la autorización limitando el acceso a las API de servicio, los archivos HDFS y la ejecución de trabajos.

En este artículo se tratan los conceptos clave relacionados con la seguridad en el clúster de macrodatos.

## <a name="cluster-endpoints"></a>Puntos de conexión de clúster

Hay tres puntos de entrada al clúster de macrodatos.

* Puerta de enlace HDFS/Spark (Knox): se trata de un punto de conexión basado en HTTPS. Otros puntos de conexión se procesan en proxy a través de este. La puerta de enlace HDFS/Spark se usa para acceder a servicios como webHDFS y Livy. Siempre que vea referencias a Knox, este es el punto de conexión.

* Punto de conexión del controlador: servicio de administración de clústeres de macrodatos que expone las API REST para administrar el clúster. También se accede a algunas herramientas a través de este punto de conexión.

* Instancia maestra: punto de conexión TDS para conectar herramientas y aplicaciones de base de datos a la instancia maestra de SQL Server del clúster.

![Puntos de conexión de clúster](media/concept-security/cluster_endpoints.png)

Actualmente, no hay ninguna opción para abrir puertos adicionales para acceder al clúster desde el exterior.

### <a name="how-endpoints-are-secured"></a>Cómo se protegen los puntos de conexión

La protección de los puntos de conexión en el clúster de macrodatos se realiza mediante contraseñas que se pueden establecer o actualizar con variables de entorno o comandos de la CLI. Todas las contraseñas internas del clúster se almacenan como secretos de Kubernetes.  

## <a name="authentication"></a>Autenticación

Tras el aprovisionamiento del clúster, se crean varios inicios de sesión.

Algunos de estos inicios de sesión son para que los servicios se comuniquen entre sí y otros para que los usuarios finales accedan al clúster.

### <a name="end-user-authentication"></a>Autenticación de usuario final
Tras el aprovisionamiento del clúster, es necesario establecer una serie de contraseñas de usuario final mediante variables de entorno. Se trata de contraseñas que los administradores de SQL y los administradores de clústeres usan para acceder a los servicios:

Nombre de usuario del controlador:
 + CONTROLLER_USERNAME=<controller_username>

Contraseña del controlador:  
 + CONTROLLER_PASSWORD=<controller_password>

Contraseña de administrador del sistema de SQL Master: 
 + MSSQL_SA_PASSWORD=<controller_sa_password>

Contraseña para acceder al punto de conexión de HDFS/Spark:
 + KNOX_PASSWORD=<knox_password>

### <a name="intra-cluster-authentication"></a>Autenticación dentro de un clúster

Tras la implementación del clúster, se crean varios inicios de sesión de SQL:

* Se crea un inicio de sesión de SQL especial en la instancia de SQL del controlador que se administra en el sistema con el rol sysadmin. La contraseña de este inicio de sesión se captura como un secreto de K8s.

* Se crea un inicio de sesión de administrador del sistema en todas las instancias de SQL del clúster que el controlador posee y administra. Es necesario que el controlador realice tareas administrativas, como la configuración de alta disponibilidad o la actualización, en estas instancias. Estos inicios de sesión también se usan para la comunicación dentro del clúster entre instancias de SQL, como la instancia maestra de SQL que se comunica con un grupo de datos.

> [!NOTE]
> En la versión actual, solo se admite la autenticación básica. Todavía no está disponible el control de acceso específico a los objetos HDFS y a los grupos de datos y de proceso de clúster de macrodatos de SQL.

## <a name="intra-cluster-communication"></a>Comunicación dentro del clúster

La comunicación con servicios que no son de SQL dentro del clúster de macrodatos, como Livy con Spark o Spark con el bloque de almacenamiento, se protege mediante certificados. Todas las comunicaciones de SQL Server se protegen mediante inicios de sesión de SQL.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]de, consulte los siguientes recursos:

- [¿Qué [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]son?](big-data-cluster-overview.md)
- [Taller: Arquitectura [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] de Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
