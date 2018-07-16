---
title: Agregar o reemplazar un testigo de creación de reflejo de la base de datos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], establishing
- database mirroring [SQL Server], witness
ms.assetid: 4b5ecffd-f025-4ab7-b69d-8958c6477127
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0960274d83f50bfe1781bdfb72e5a482dcfef9c4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200145"
---
# <a name="add-or-replace-a-database-mirroring-witness-sql-server-management-studio"></a>Agregar o reemplazar un testigo de creación de reflejo de la base de datos (SQL Server Management Studio)
  Si los extremos de la creación de reflejo de la base de datos usan la Autenticación de Windows, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para agregar o reemplazar un testigo. Cuando se agrega un testigo en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , se cambia también el modo de operación al modo de alta seguridad con conmutación automática por error.  
  
> [!NOTE]  
>  Es muy recomendable que el testigo se encuentre en otro equipo de alguno de los asociados. La cuenta de servicio que usa el testigo debe estar en el mismo dominio que las cuentas de servicio que usan las instancias del servidor principal y del servidor reflejado, o bien debe estar en un dominio de confianza.  
  
### <a name="to-add-or-replace-a-witness"></a>Para agregar o reemplazar un testigo  
  
1.  Después de conectarse a la instancia del servidor principal, en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol del servidor.  
  
2.  Expanda **Bases de datos**y seleccione la base de datos principal de la sesión en la que desee agregar o reemplazar un testigo.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, luego, haga clic en **Reflejado**. Así se abre la página **Creación de reflejo** del cuadro de diálogo **Propiedades de la base de datos** .  
  
4.  Haga clic en **Configurar seguridad**.  
  
5.  Cuando aparezca la pantalla de bienvenida del **Asistente para la configuración de seguridad de la creación de reflejo de bases de datos** , seleccione **Siguiente**.  
  
6.  En el cuadro de diálogo **Incluir servidor testigo** , haga clic en **Sí**y, después, en **Siguiente**.  
  
7.  En el cuadro de diálogo **Elegir los servidores para configurar** , se marcará automáticamente la casilla **Instancia del servidor testigo** . Haga clic en **Siguiente**.  
  
8.  En el cuadro de diálogo **Instancia del servidor principal** , conserve las opciones existentes de puerto y extremos. Haga clic en **Siguiente**.  
  
9. En el cuadro de diálogo **Instancia del servidor testigo** , haga clic en **Conectar**.  
  
10. En el cuadro de diálogo **Conectar al servidor** , especifique la instancia del servidor testigo en el campo **Nombre del servidor** y use la Autenticación de Windows (opción predeterminada). Haga clic en **Conectar**.  
  
11. Una vez que se haya establecido una conexión, en el cuadro de diálogo **Instancia del servidor testigo** se mostrará el puerto de escucha y el extremo de la creación de reflejo de la base de datos de la instancia del servidor testigo. Haga clic en **Siguiente**.  
  
12. El cuadro de diálogo **Cuentas de servicio** contiene campos para las cuentas de servicio de dominio de las instancias del servidor reflejado, principal y testigo.  
  
    -   Si todas las instancias del servidor utilizan la misma cuenta de servicio, deje los campos en blanco.  
  
    -   Si la instancia del servidor testigo usa una cuenta de servicio diferente de las de los asociados, llene los campos **Principal**, **Reflejado**y **Testigo** con el nombre de la cuenta:  
  
         *DOMAINNAME* **\\** *username*  
  
         El nombre de dominio debe estar en mayúsculas.  
  
     Haga clic en **Siguiente**.  
  
13. Si lo desea, en la pantalla de resumen **Finalización del asistente** , compruebe la configuración del testigo y haga clic en **Finalizar**.  
  
14. Cuando finalice, el asistente volverá al cuadro de diálogo **Propiedades de la base de datos** , donde en el campo **Testigo** se mostrará la dirección de red del servidor del testigo. Además, se seleccionará automáticamente **Modo de alta seguridad con conmutación por error automática (sincrónica)**, que es necesario con un testigo.  
  
     Para habilitar el testigo y cambiar la sesión al modo de alta seguridad con conmutación por error automática, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Testigo de creación de reflejo de la base de datos](database-mirroring-witness.md)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Propiedades de la base de datos &#40;página Creación de reflejo&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)   
 [Testigo de creación de reflejo de la base de datos](database-mirroring-witness.md)  
  
  
