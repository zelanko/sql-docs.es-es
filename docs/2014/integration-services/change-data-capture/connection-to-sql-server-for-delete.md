---
title: Conexión con SQL Server para eliminación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: acb755f8cc1e425e38714013511948f7b5b4c580
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392943"
---
# <a name="connection-to-sql-server-for-delete"></a>Conexión con SQL Server para eliminación
  Cuando un inicio de sesión sin un rol de base de datos que incluye el permiso de escritura (por ejemplo, el rol **db_owner**) para la base de datos MSXDBCDC intenta eliminar una instancia CDC de Oracle, se muestra el cuadro de diálogo Conectar con SQL Server.  
  
 En este cuadro de diálogo debe especificar las credenciales para un inicio de sesión que tenga permiso de escritura para la base de datos MSXDBCDC, como el rol de base de datos **db_owner** para eliminar la instancia CDC de Oracle.  
  
 Escriba la información siguiente en el cuadro de diálogo Conectar con SQL Server.  
  
 **Nombre de servidor**  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Autenticación**  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**  
  
-   **Autenticación de SQL Server**: Si selecciona esta opción, debe escribir el **inicio de sesión** y **contraseña** para el usuario en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se conecta.  
  
 **Opciones**  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
-   **Tiempo de espera de conexión**: Escriba el tiempo (en segundos) en el programa espera la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexión para establecerse antes de producir un error de tiempo de espera. El valor predeterminado es **15**.  
  
-   **Tiempo de espera de ejecución**: Escriba el tiempo (en segundos) que el programa espera que finalice antes de producir un error de tiempo de espera la ejecución del comando SQL. El valor predeterminado es **30**.  
  
-   **Cifrar conexión**: Seleccione **cifrar conexión** para asegurarse de que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexión que se está estableciendo está cifrada para garantizar la privacidad.  
  
-   **Avanzadas**: Haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
## <a name="see-also"></a>Vea también  
 [Permisos de conexión con SQL Server necesarios para el servicio CDC](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
