---
title: Crear y editar una instancia de Oracle CDC Service | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 10cd612e-d8f1-4af2-97d3-a0c22e1e2326
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1b59ebbf4bb56d23009351f4a8fb7f193a59fa66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771451"
---
# <a name="create-and-edit-an-oracle-cdc-service"></a>Crear y editar un servicio CDC de Oracle
  Para crear y editar un nuevo servicio de Windows CDC de Oracle se emplea la Consola de configuración del servicio CDC.  
  
 Para crear un nuevo servicio de Windows CDC de Oracle, seleccione **Servicios CDC locales** en el panel izquierdo y, a continuación, haga clic en **Nuevo servicio** en el panel **Acciones** . También puede hacer clic con el botón derecho en **Local CDC Services** (Servicios CDC locales) y seleccionar **Nuevo servicio**. Se abrirá el cuadro de diálogo Nuevo servicio de Windows CDC de Oracle.  
  
 **OR**  
  
 Para editar las propiedades del servicio CDC, seleccione el servicio cuyas propiedades desea editar y haga clic en **Propiedades** en el panel **Acciones** . También puede hacer clic con el botón derecho en el servicio con el que está trabajando y seleccionar **Propiedades**. Se abrirá el cuadro de diálogo Propiedades del servicio CDC.  
  
 Especifique la siguiente información en los cuadros de diálogos Nuevo servicio de Windows CDC de Oracle o Propiedades del servicio CDC.  
  
 Nombre de servicio  
 Escriba el nombre del nuevo servicio de Windows CDC de Oracle. Si es posible, no debe usar nombres largos. No se pueden usar los caracteres / y \ en el nombre del servicio.  
  
> [!NOTE]  
> Esta opción no está disponible al editar el servicio. No puede cambiar el nombre de un servicio de Windows que ya existe.  
  
 **Descripción**  
 Escriba una descripción del servicio para identificarlo.  
  
 **Cuenta de servicio**  
 Seleccione una de las opciones siguientes para determinar la cuenta bajo la cual se ejecutará el servicio:  
  
-   **Cuenta de sistema local**  
  
     No se recomienda porque proporciona demasiados permisos para el servicio.  
  
-   **Esta cuenta**  
  
     En Windows Vista o Windows Server 2008, la cuenta de servicio predeterminada es SERVICIO DE RED.  
  
     En Windows 7, Windows Server 2008 R2 y versiones posteriores, la cuenta de servicio predeterminada es Servicio NT\\<nombre-servicio>.  
  
     El uso de estas cuentas le permite trabajar sin necesidad de usar contraseñas. Además, estas cuentas solo proporcionan los permisos necesarios para la ejecución del servicio CDC de Oracle.  
  
     Puede emplear una cuenta de Windows local o de dominio para la cuenta de servicio. En este caso, debe especificar la **Contraseña** para dicha cuenta. Esta cuenta puede ser para el host local o para una cuenta de dominio. Asegúrese de actualizar la contraseña cuando se cambie mediante Servicios locales en el Panel de control de Windows.  
  
 **Nombre del servidor**: seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino a la que quiera conectarse (por ejemplo, **\\\\<nombre_equipo>\\<nombre_instancia>**). De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
 **Autenticación**  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**: si selecciona esta opción, el servicio CDC de Oracle se conecta a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino con la identidad de la cuenta de servicio. Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en un equipo diferente, se debe usar la autenticación de Windows con cuentas de dominio.  
  
-   **Autenticación de SQL Server**: si selecciona esta opción, debe escribir los valores de **Nombre de usuario** y **Contraseña** del inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que quiere usar. El servicio CDC de Oracle usa estas credenciales para conectar con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 El inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado por el servicio CDC de Oracle solo necesita ser miembro del rol fijo de servidor public; no se necesita ningún otro privilegio. Una vez agregadas nuevas instancias CDC de Oracle, ese inicio de sesión recibirá acceso **db_owner** a las bases de datos CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociadas.  
  
 Para crear la definición del servicio de Windows CDC de Oracle, el programa necesita acceso de actualización a la base de datos MSXDBCDC en la instancia asociada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al hacer clic en **Aceptar**, un cuadro de diálogo pide al usuario que especifique un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un acceso de actualización para la base de datos MSXDBCDC.  
  
 Para obtener información acerca de los datos que debe escribir en el cuadro de diálogo Conectar con SQL Server, vea [Connection to SQL Server](connection-to-sql-server.md).  
  
 **Opciones**  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
-   **Tiempo de espera de la conexión**: Escriba el tiempo (en segundos) que el servicio CDC para Oracle espera una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de agotarse el tiempo de espera. El valor predeterminado es **15**.  
  
-   **Tiempo de espera de ejecución**: Escriba el tiempo (en segundos) que el servicio de Windows CDC de Oracle espera que se ejecute un comando antes de agotarse el tiempo de espera. El valor predeterminado es **30**.  
  
-   **Cifrar conexión**: seleccione **Cifrar conexión** para que la comunicación entre el servicio CDC de Oracle y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino se realice mediante una conexión cifrada.  
  
-   **Avanzadas**: escriba cualquier propiedad de conexión adicional, si es necesario.  
  
 **Contraseña maestra**  
 Escriba una contraseña que el servicio de Windows CDC de Oracle usará para proteger las credenciales de minería de registros de Oracle.  
  
 También se debe usar la misma contraseña maestra cuando otras instancias del mismo servicio estén configuradas en otros nodos de un clúster en una configuración de alta disponibilidad. Si pierde o modifica la contraseña maestra, será necesario volver a especificar todas las contraseñas de minería de registros almacenadas en bases de datos de la instancia CDC de Oracle desde la Consola del diseñador CDC.  
  
## <a name="see-also"></a>Vea también  
 [Cómo crear y editar un servicio CDC](how-to-create-and-edit-a-cdc-service.md)  
  
  
