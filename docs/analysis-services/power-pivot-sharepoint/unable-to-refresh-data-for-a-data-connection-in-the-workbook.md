---
title: No se puede actualizar los datos de una conexión de datos en el libro | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1fabd45d3b9858114e48e3bdde258ed6ccc8362
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook"></a>No se pueden actualizar los datos para la conexión de datos del libro
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Para libros de Excel que contienen datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Excel Services devuelve este error si envía una solicitud de conexión a un servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y se produce un error en la solicitud.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a:|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Ver más abajo.|  
|Texto del mensaje|No pueden actualizar los datos de una conexión de datos del libro. Vuelva a intentarlo o póngase en contacto con el administrador del sistema. No se pudieron actualizar las siguientes conexiones: datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
  
## <a name="explanation-and-resolution"></a>Explicación y resolución  
 Excel Services no puede conectar con los datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o cargarlos. Este error puede producirse por alguna de las condiciones siguientes:  
  
 **Escenario 1: el servicio no se inicia**  
  
 La instancia de SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) no se inicia. Una contraseña caducada hará que el servicio deje de funcionar. Para obtener más información acerca de cómo cambiar la contraseña, vea [Configurar las cuentas de servicio Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md) y [Iniciar o detener un servidor de Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md).  
  
 **Escenario 2a: abrir un libro de la versión anterior en el servidor**  
  
 El libro que intenta abrir podría haberse creado en la versión SQL Server 2008 R2 de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel. Probablemente, el proveedor de datos de Analysis Services que se especifica en la cadena de conexión de datos no está presente en el equipo que controla la solicitud.  
  
 Si este es el caso, encontrará este mensaje en el registro de ULS: "Error al actualizar '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]datos t' en el libro '\<dirección URL al libro >'", seguido de "No se puede establecer una conexión".  
  
 Para determinar la versión del libro, ábralo en Excel y compruebe qué proveedor de datos se especifica en la cadena de conexión. Un libro de SQL Server 2008 R2 usa MSOLAP.4 como su proveedor de datos.  
  
 Para evitar este problema, puede actualizar el libro. Como alternativa, puede instalar bibliotecas de cliente de la versión SQL Server 2008 R2 de Analysis Services en los equipos físicos mediante la ejecución de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o Excel Services: [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
 **Escenario 2b: Excel Services se ejecuta en un servidor de aplicaciones que tiene una versión incorrecta de las bibliotecas de cliente**  
  
 De forma predeterminada, SharePoint Server 2010 instala la versión SQL Server 2008 del proveedor OLE DB de Analysis Services en los servidores de aplicaciones que ejecutan Excel Services. En una granja de servidores que admite el acceso a datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , todos los servidores físicos que ejecutan aplicaciones que solicitan datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , por ejemplo, Excel Services y [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, deben usar una versión posterior del proveedor de datos.  
  
 Los servidores que ejecutan [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint obtienen el proveedor de datos OLE DB actualizado automáticamente. Otros servidores, como los que ejecutan una instancia independiente de Excel Services sin [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en el mismo equipo, deben aplicar una revisión para usar las bibliotecas de cliente más recientes. Para más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
 **Escenario 3: el controlador de dominio no está disponible**  
  
 La causa podría ser que un controlador de dominio no está disponible para validar la identidad del usuario. Notificaciones del servicio de token de Windows requiere un controlador de dominio para autenticar al usuario de SharePoint en cada conexión. Notificaciones del servicio de token de Windows no utiliza las credenciales almacenadas en memoria caché. Valida la identidad del usuario para cada conexión.  
  
 Puede confirmar la causa de este error en el archivo de registro de SharePoint. Si los registros de SharePoint incluyen el mensaje "No se puede obtener WindowsIdentity de IClaimsIdentity", la identidad del usuario no se pudo autenticar.  
  
 Para evitar este problema, una el equipo al mismo dominio del servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o instale un controlador de dominio en el equipo local. La segunda solución, instalar el controlador de dominio, le exigirá que cree cuentas de dominio locales para todos los servicios y usuarios. Tendrá que configurar cuentas de servicio y permisos de SharePoint para las cuentas que defina.  
  
 La instalación de un controlador de dominio en el equipo resulta útil si desea utilizar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en un estado sin conexión. Para obtener instrucciones detalladas sobre cómo usar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sin conexión, vea la entrada del blog "toma la [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] servidor fuera de la red" en [ http://www.powerpivotgeek.com ](http://go.microsoft.com/fwlink/?LinkId=184241).  
  
 **Escenario 4: servidor inestable**  
  
 Uno o más servicios pueden estar en un estado incoherente. En algunos casos, al ejecutar IISRESET, se resolverá el problema.  
  
  
