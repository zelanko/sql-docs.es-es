---
title: Crear la base de datos de cambios de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b9ea9d63d2303a66e56ab38774845cee73c125a4
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728932"
---
# <a name="create-the-sql-server-change-database"></a>Crear la base de datos de cambios de SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Cuando se inicia el Asistente para nueva instancia, se abre la página Crear base de datos CDC. Use la página Crear base de datos CDC para proporcionar información sobre la nueva instancia CDC y crear una nueva base de datos Cambios.  
  
 Cuando se crea una nueva base de datos CDC, se habilita para CDC de SQL Server y esta habilitación necesita un inicio de sesión que sea miembro del rol fijo de servidor `sysadmin` .  
  
 Cuando un usuario que inicia el Asistente para crear una instancia CDC de Oracle no es miembro del rol fijo de servidor `sysadmin` , se abre el cuadro de diálogo Conectar con SQL Server y solicita las credenciales para un miembro del rol sysadmin para realizar la tarea Habilitar la base de datos para CDC de SQL Server. Cuando se crea la base de datos CDC, el inicio de sesión `sysadmin` se descarta y se reanuda el trabajo con el inicio de sesión original de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado cuando se entró en la Consola del diseñador de Oracle.  
  
> [!IMPORTANT]  
>  Para otras tareas distintas de Habilitar la base de datos para CDC de SQL Server, el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para ejecutar el Asistente para nueva instancia debe tener el rol fijo de servidor `dbcreator` y permisos UPDATE en la base de datos MSXDBCDC.  
  
 Para obtener información acerca de cómo escribir los datos en el cuadro de diálogo Conectar con SQL Server, vea [SQL Server Connection for Instance Creation](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md).  
  
## <a name="options"></a>Opciones  
 **Instancia CDC de Oracle**  
 Escriba la siguiente información sobre la instancia de CDC que está creando.  
  
-   **Nombre**: escriba un nombre para el nuevo servicio. También será el nombre de la nueva base de datos Cambios.  
  
-   **Descripción**: escriba una descripción para la nueva instancia para que le ayude a identificarla. Esto es opcional.  
  
 **Base de datos de cambios de SQL Server**  
 Esta sección se emplea para crear la base de datos.  
  
1.  **Cambiar la base de datos**: el nombre de la nueva base de datos cambiada. El nombre de la base de datos es el mismo que el que asignó a la instancia. Este campo de solo lectura muestra la ruta de acceso completa a la base de datos.  
  
2.  **Crear base de datos**: haga clic en **Crear base de datos** para crear la base de datos.  
  
     Para crear la base de datos, el inicio de sesión debe tener el rol de servidor `sysasmin` . Vea la nota de seguridad anterior para obtener más información.  
  
     Después de crear la base de datos, puede hacer clic en **Siguiente** para [Connect to an Oracle Source Database](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md).  
  
## <a name="see-also"></a>Consulte también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [El servicio CDC de Oracle](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
  
