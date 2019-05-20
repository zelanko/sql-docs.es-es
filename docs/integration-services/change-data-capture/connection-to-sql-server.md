---
title: Conexión con SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a3e9f70011d96d9aa5d5068af5cddecd8f29cce9
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728991"
---
# <a name="connection-to-sql-server"></a>Conexión con SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Cuando un inicio de sesión sin un rol de base de datos que incluye el permiso de escritura (por ejemplo, el rol **db_owner**) para la base de datos MSXDBCDC intenta crear una instancia CDC de Oracle, se muestra el cuadro de diálogo Conectar con SQL Server.  
  
 En este cuadro de diálogo tiene que especificar las credenciales para un inicio de sesión que tenga permiso de escritura en la base de datos MSXDBCDC, como el rol de base de datos **db_owner** , para crear una instancia CDC de Oracle.  
  
 Escriba la información siguiente en el cuadro de diálogo Conectar con SQL Server.  
  
### <a name="server-name"></a>Nombre del servidor  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="authentication"></a>Autenticación  
 Seleccione una de las opciones siguientes:  
  
-   Autenticación de Windows  
  
-   **Autenticación de SQL Server**: si selecciona esta opción, es necesario que escriba el **inicio de sesión** y la **contraseña** del usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se va a conectar.  
  
### <a name="options"></a>Opciones  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
-   **Tiempo de espera de la conexión**: escriba el tiempo (en segundos) que el programa espera hasta que se establezca una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de generar un error de tiempo de espera. El valor predeterminado es **15**.  
  
-   **Tiempo de espera de ejecución**: escriba el tiempo (en segundos) que el programa espera hasta que finalice la ejecución de un comando SQL antes de generar un error de tiempo de espera. El valor predeterminado es **30**.  
  
-   **Cifrar conexión**: seleccione **Cifrar conexión** para asegurarse de que la conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se establece está cifrada para garantizar la privacidad.  
  
-   **Avanzadas**: Haga clic en **Avanzadas** y escriba cualquier propiedad de conexión adicional en el cuadro de diálogo Propiedades avanzadas de conexión, si es necesario.  
  
## <a name="see-also"></a>Consulte también  
 [Permisos de conexión con SQL Server necesarios para el servicio CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
