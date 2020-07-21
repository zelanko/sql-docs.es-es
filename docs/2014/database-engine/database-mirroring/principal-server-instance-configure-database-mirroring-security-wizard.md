---
title: Instancia de servidor principal (Asistente para la configuración de seguridad de la creación de reflejo de bases de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2632b5ffd5355065b4b5c1f905b3b6e5c5b6204d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934052"
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>Instancia de servidor principal (Asistente para la configuración de seguridad de la creación de reflejo de bases de datos)
  Utilice esta página para especificar la información acerca de la instancia de servidor de la base de datos principal. La base de datos principal es la copia de la base de datos que empieza en la sesión de creación de reflejo. Una vez que la sesión ha empezado, la base de datos principal es la copia de la base de datos que acepta los cambios del usuario. Cuando se produce una conmutación por error, los roles principales y de creación de reflejo se intercambian, de modo que es posible que la base de datos principal inicial no sea permanente.  
  
 **Para configurar la creación de reflejo de la base de datos mediante SQL Server Management Studio**  
  
-   [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar el Asistente para la configuración de seguridad de la creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opciones  
 **Instancia del servidor principal**  
 Dado que la creación de reflejo de la base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] siempre se configura desde el servidor principal, la instancia de servidor actual siempre es la instancia de servidor principal.  
  
 **Listener Port** (Puerto de escucha)  
 El comportamiento de esta opción depende de la existencia del extremo de reflejo para la instancia de servidor, del modo siguiente:  
  
-   Si el puerto de escucha no existe para esta instancia de servidor, aparecerá el número de puerto 5022 en el cuadro de texto **Puerto** . Puede escribir cualquier número de puerto disponible, como el 7022.  
  
-   Cuando ya existe el extremo de reflejo, aparecerá el número de puerto del extremo. Si necesita cambiar el puerto, use un comando ALTER ENDPOINT. Para obtener más información, vea [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).  
  
> [!NOTE]  
>  Se requiere un número de puerto.  
  
 **Nombre del punto de conexión**  
 Si el extremo de reflejo existe para esta instancia de servidor, el nombre del extremo aparecerá aquí. Si el extremo no existe, puede especificar el nombre del extremo.  
  
 **Cifrar datos enviados a través de este extremo**  
 El cifrado está habilitado de forma predeterminada. Cuando se habilita, el cifrado no solo se admite, sino que es necesario y utiliza los valores predeterminados para todas las opciones de cifrado. Para obtener más información, vea [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
 Para deshabilitar el cifrado, quite la marca de la casilla. Para volver a habilitar el cifrado, active la casilla.  
  
## <a name="see-also"></a>Consulte también  
 [El extremo de creación de reflejo de la base de datos &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Propiedades de la base de datos &#40;página creación de reflejo&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Crear un extremo de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Iniciar Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
