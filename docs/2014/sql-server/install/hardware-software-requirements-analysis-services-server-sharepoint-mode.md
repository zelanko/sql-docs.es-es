---
title: Requisitos de hardware y software para Analysis Services Server en modo de SharePoint (SQL Server 2014) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 425639d6e22491028f552bc97990267b2b33e799
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637811"
---
# <a name="hardware-and-software-requirements-for-analysis-services-server-in-sharepoint-mode-sql-server-2014"></a>Requisitos de hardware y software para el servidor de Analysis Services en modo de SharePoint (SQL Server 2014)

[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] admite SharePoint 2010 y SharePoint 2013. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 se ejecuta fuera de la granja de servidores de SharePoint aunque se puede instalar en servidores de SharePoint. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 se ejecuta en servidores de aplicaciones en una granja de SharePoint 2010 y utiliza las características e infraestructura de SharePoint para admitir operaciones del servidor. Para instalar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para cualquier versión de SharePoint, utilice el asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Después de la instalación, haga lo siguiente:  
  
- Ejecute la versión adecuada de la herramienta de configuración de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para la versión de SharePoint.  
  
- En el caso de SharePoint 2013, instale [o desinstale el complemento de PowerPivot para SharePoint &#40;de SharePoint&#41;2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013).  

##  <a name="bkmk_sqleditions"></a> Requisitos de edición de SQL Server  
 No todas las características de Business Intelligence están disponibles en todas las ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [características compatibles con las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md) y [ediciones y componentes de SQL Server 2014](../editions-and-components-of-sql-server-2016.md).  
  
 Las notas de la versión actuales se pueden encontrar en [Microsoft SQL Server notas](https://go.microsoft.com/fwlink/?LinkID=296445)de la versión de 2014.  
  

  
##  <a name="bkmk_sqllicense"></a>Licencias de SQL Server  
 Para obtener más información acerca de las licencias de SQL Server, vea lo siguiente:  
  
-   [Hoja de SQL Server de licencias de 2014](https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf) (https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf).  
  
-   [Cómo comprar: compatibilidad con modelos de licencias de SQL Server](https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2) (https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2).  
  
##  <a name="bkmk_ssas__sharepoint_2013"></a>Analysis Services instala en SharePoint 2013  
 Si instala el servidor de Analysis Services en modo de SharePoint en un servidor independiente, los requisitos mínimos del sistema se basan en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en lugar de basarse en los requisitos de SharePoint Server.  
  
 [Requisitos de hardware y software para instalar SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint funciona mejor en los servidores empresariales de nueva generación que proporcionan umbrales de RAM más altos y más capacidad de procesamiento. Se usa mucha RAM para almacenar datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en memoria. El RAM admite la posibilidad de adaptarse a cambios estructurales. Los procesadores adicionales admiten exámenes largos de datos sin formato y sin agregados. Los datos suponen que su estructura está en un entorno dinámico, como respuesta a un análisis de datos controlado por el usuario iniciado mediante una interfaz cliente o front-end de Excel.  
  
> [!TIP]  
>  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa memorias caché L2 y L3. Para mejorar el rendimiento, considere la posibilidad de usar procesadores con memorias caché L2 y L3 mayores.  
  
 En la tabla siguiente se describen la configuración de hardware mínima y recomendada para un servidor independiente de [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] que no forma parte de la granja de servidores de SharePoint:  
  
|Componente|Mínima|Se recomienda|  
|---------------|-------------|-----------------|  
|Procesador|Procesador de dos núcleos de 64 bits a 3 gigahercios.|16 núcleos|  
|RAM|8 gigabytes de RAM|64 gigabytes de RAM|  
|Storage|80 gigabytes de almacenamiento|80 gigabytes o más|  
  
 Si instala el servidor de Analysis Services en modo de SharePoint en una granja de servidores de SharePoint, puede ver los requisitos mínimos del sistema para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y para SharePoint Server en los vínculos siguientes:  
  
-   [Requisitos de hardware y software para instalar SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Requisitos de hardware y software para SharePoint 2013](https://technet.microsoft.com/library/cc262485\(office.15\).aspx).  
  
 Las recomendaciones de software y hardware estándar para SharePoint 2013 son adecuadas para una solución de administración de documentos basada en web para un grupo de trabajo o un equipo. Como el procesamiento de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa muchos datos, la recomendación estándar es adecuada si la carga de trabajo general es pequeña, por ejemplo de menos de 100 usuarios o libros. Una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] mayor necesita capacidad de proceso adicional.  
  
##  <a name="bkmk_ssas__sharepoint_2010"></a>Analysis Services instalados en un servidor de SharePoint 2010  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 se ejecuta en servidores de aplicaciones en una granja de SharePoint 2010 y utiliza las características e infraestructura de SharePoint para admitir operaciones del servidor. En la tabla siguiente se resumen los requisitos relacionados con las implementaciones de SharePoint 2010:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Versión de SharePoint|SharePoint 2010 Enterprise, con Excel Services, Servicio de almacenamiento seguro y las Notificaciones del servicio de token de Windows configurados en la misma granja de servidores.<br /><br /> SharePoint se debe instalar usando la opción de servidor de granja del programa de instalación de SharePoint (no se admite la opción de instalación independiente de SharePoint). [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] requiere la infraestructura de la granja de servidores para admitir acceso a datos y administrativo. La instalación independiente no proporciona estos servicios.<br /><br /> La edición para desarrolladores, que se ejecuta en Windows 7 o Windows Vista, no se admite para las instalaciones de servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|  
|Service Pack|Se requiere SharePoint Server 2010 Service Pack 1 (SP1).<br /><br /> SharePoint 2010 Service Pack 1 se requiere para las características de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].<br /><br /> Se requiere la actualización acumulativa de SharePoint 2010 de agosto de 2010 o posterior al actualizar desde una versión anterior de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Se debe instalar la actualización acumulativa de agosto de 2010 o posterior después de instalar SharePoint Service Pack 1. Una nueva instalación de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] no requiere la actualización acumulativa. Para obtener más información, consulte la [actualización acumulativa de agosto de 2010 para SharePoint](http://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx).|  
|Aplicación web de SharePoint|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010 solo admite las aplicaciones web de SharePoint configuradas para la autenticación en modo clásico. Si va a agregar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint a una granja de servidores existente, asegúrese de que la aplicación web con la que piensa utilizarlo esté configurada para usar la autenticación en modo clásico. Para obtener instrucciones sobre cómo comprobar el modo de autenticación, vea la sección "comprobar que la aplicación Web usa la autenticación de modo clásico" en [implementar soluciones de PowerPivot en SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint).|  
|Proveedores de datos necesarios para la actualización de datos del lado servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|La actualización de datos del lado servidor repite los mismos pasos de recuperación de datos que se usan para importar originalmente los datos. Esto significa que los proveedores de datos utilizados para importar datos en una estación de trabajo cliente deben estar presentes también en el servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.<br /><br /> Además, el uso de fuentes de distribución de datos en un servidor de SharePoint requiere ADO.NET Data Services. El programa instalador de requisitos previos de SharePoint no instala este software automáticamente. El software siguiente se debe instalar manualmente.<br /><br /> Los ensamblados en tiempo de ejecución de ADO.NET Data Services 3.5 SP1, que se usaban para exportar una lista de SharePoint como una fuente de distribución de datos. Descargue e instale la versión que coincida con su sistema operativo:<br /><br /> En Windows Server 2008 R2, use [ADO.NET Data Services Update para .NET Framework 3,5 SP1 para Windows 7 y Windows Server 2008 R2](https://www.microsoft.com/download/details.aspx?id=2343). Windows Server 2008 R2 **SP1** ya contiene el proveedor actualizado.<br /><br /> En Windows Server 2008, use [ADO.NET Data Services Update para .NET Framework 3,5 SP1 para windows 2000, Windows server 2003, Windows XP, Windows Vista y Windows server 2008 (https://go.microsoft.com/fwlink/?LinkId=158125)](https://www.microsoft.com/download/details.aspx?id=22734).|  
  
 [Determinar los requisitos de hardware y software (SharePoint 2010) (https://go.microsoft.com/fwlink/?LinkId=169734)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
## <a name="additional-information"></a>Información adicional  

Para obtener información sobre los cambios de SharePoint, vea [cambios de sharepoint 2010 a sharepoint 2013](https://technet.microsoft.com/library/ff607742\(office.15\).aspx) (https://technet.microsoft.com/library/ff607742(office.15).aspx).