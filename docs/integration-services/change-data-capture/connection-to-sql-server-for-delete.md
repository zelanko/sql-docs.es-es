---
title: Conexión con SQL Server para eliminación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c2db76002be78fba04d324036b3eb5af1b81585a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916291"
---
# <a name="connection-to-sql-server-for-delete"></a>Conexión con SQL Server para eliminación

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Cuando un inicio de sesión sin un rol de base de datos que incluye el permiso de escritura (por ejemplo, el rol **db_owner** ) para la base de datos MSXDBCDC intenta eliminar una instancia CDC de Oracle, se muestra el cuadro de diálogo Conectar con SQL Server.  
  
 En este cuadro de diálogo debe especificar las credenciales para un inicio de sesión que tenga permiso de escritura para la base de datos MSXDBCDC, como el rol de base de datos **db_owner** para eliminar la instancia CDC de Oracle.  
  
 Escriba la información siguiente en el cuadro de diálogo Conectar con SQL Server.  
  
 **Nombre de servidor**  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Autenticación**  
 Seleccione uno de los siguientes:  
  
-   **Autenticación de Windows**  
  
-   **Autenticación de SQL Server**: si selecciona esta opción, es necesario que escriba el **Inicio de sesión** y la **Contraseña** del usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se conecta.  
  
 **Opciones**  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
-   **Tiempo de espera de la conexión**: escriba el tiempo (en segundos) que el programa espera hasta que se establezca una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de producir un error de tiempo de espera. El valor predeterminado es **15**.  
  
-   **Tiempo de espera de ejecución**: escriba el tiempo (en segundos) que el programa espera hasta que finalice la ejecución de un comando SQL antes de producir un error de tiempo de espera. El valor predeterminado es **30**.  
  
-   **Cifrar conexión**: seleccione **Cifrar conexión** para asegurarse de que la conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se establece está cifrada para garantizar la privacidad.  
  
-   **Avanzadas**: haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
## <a name="see-also"></a>Consulte también  
 [Permisos de conexión con SQL Server necesarios para el servicio CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
