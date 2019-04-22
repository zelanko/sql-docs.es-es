---
title: Conceptos de seguridad
titleSuffix: SQL Server big data clusters
description: En este artículo se describe los conceptos de seguridad de clúster de macrodatos de 2019 de SQL Server (versión preliminar). Esto incluye la descripción de los puntos de conexión del clúster y la autenticación del clúster.
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ebe1ef0a9a0337af29a09018bcc2e0150d676879
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860116"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>Conceptos de seguridad para los clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Un clúster seguro macrodatos implica la compatibilidad de consistente y coherente para los escenarios de autenticación y autorización, a través de SQL Server y Spark o HDFS. La autenticación es el proceso de comprobar la identidad de un usuario o servicio y asegurarse de que es quien se afirma ser. Autorización hace referencia a conceder o denegar el acceso a recursos específicos según la identidad del usuario solicitante. Este paso se realiza después de que un usuario se identifica mediante la autenticación.

Autorización en el contexto de datos de gran tamaño normalmente se realiza a través de listas de control de acceso (ACL), que asociar las identidades de usuario con permisos específicos. HDFS admite la autorización mediante la limitación de acceso a las API del servicio, los archivos HDFS y ejecución del trabajo.

Este artículo trata los conceptos clave relacionados con la seguridad en el clúster de macrodatos.

## <a name="cluster-endpoints"></a>Puntos de conexión de clúster

Existen tres puntos de entrada para el clúster de macrodatos

* Puerta de enlace de Spark o HDFS (Knox): se trata de un punto de conexión basada en HTTPS. Otros puntos de conexión son procesadas por el proxy a través de este. Puerta de enlace de Spark o HDFS se usa para tener acceso a servicios como webHDFS y Livy. Siempre que vea referencias a Knox, esto es el punto de conexión.

* Punto de conexión de controlador - servicio de administración de clúster de macrodatos que expone las API de REST de administración del clúster. Algunas herramientas, como el portal de administración, también son accesibles a través de este punto de conexión.

* Instancia principal: extremo de TDS para herramientas de base de datos y aplicaciones para conectarse a la instancia de SQL Server Master en el clúster.

![Puntos de conexión de clúster](media/concept-security/cluster_endpoints.png)

Actualmente, no hay ninguna opción de abrir puertos adicionales para acceder al clúster desde el exterior.

### <a name="how-endpoints-are-secured"></a>¿Cómo se protegen los puntos de conexión

Protección de extremos en el clúster de macrodatos se realiza usando contraseñas que pueden ser conjunto/actualizado ya sea mediante las variables de entorno o comandos de CLI. Todas las contraseñas interna del clúster se almacenan como secretos de Kubernetes.  

## <a name="authentication"></a>Autenticación

Tras el aprovisionamiento del clúster, se crea un número de inicios de sesión.

Algunos de estos inicios de sesión son para que los servicios se comuniquen entre sí, y otros son para que los usuarios finales acceder al clúster.

### <a name="end-user-authentication"></a>Autenticación de usuario final
Tras el aprovisionamiento del clúster, un número de contraseñas de usuario final debe establecerse mediante variables de entorno. Estas son las contraseñas que los administradores de SQL y los administradores de clústeres se usan para tener acceso a servicios:

Nombre de usuario del controlador:
 + CONTROLLER_USERNAME=<controller_username>

Contraseña del controlador:  
 + CONTROLLER_PASSWORD = < controller_password >

Contraseña de SA de SQL Master: 
 + MSSQL_SA_PASSWORD=<controller_sa_password>

Contraseña para acceder al punto de conexión de Spark o HDFS:
 + KNOX_PASSWORD = < knox_password >

### <a name="intra-cluster-authentication"></a>Autenticación dentro del clúster

Tras la implementación del clúster, se crea un número de inicios de sesión SQL:

* Se crea un inicio de sesión especial de SQL en la instancia de SQL de controlador que está administrado, con el rol de administrador del sistema por el sistema. La contraseña para este inicio de sesión se captura como un secreto K8s.

* Se crea un inicio de sesión de administrador del sistema en todas las instancias SQL en el clúster, que controlador posee y administra. Es necesario para el controlador realizar tareas administrativas, como la instalación de alta disponibilidad o la actualización, en estas instancias. Estos inicios de sesión también se usan para la comunicación dentro del clúster entre instancias SQL, como la instancia SQL maestra comunicarse con un grupo de datos.

> [!NOTE]
> En la versión actual, se admite solo la autenticación básica. Control de acceso a objetos HDFS y SQL macrodatos clúster datos y los grupos, aún no está disponible.

## <a name="intra-cluster-communication"></a>Comunicación dentro del clúster

Comunicación con los servicios que no son de SQL dentro del clúster de macrodatos, por ejemplo, Livy Spark o Spark para el grupo de almacenamiento, se protege mediante certificados. Todos los SQL Server para la comunicación de SQL Server está protegida mediante inicios de sesión SQL.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte los siguientes recursos:

- [¿Qué son los clústeres de macrodatos de 2019 de SQL Server?](big-data-cluster-overview.md)
- [Taller: Arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
